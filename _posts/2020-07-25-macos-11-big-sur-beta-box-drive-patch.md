---
layout: post
title: "Box Drive on macOS 11 Big Sur (beta)"
date: 2020-07-25
categories: [Reverse Engineering, macOS]
tags: [beta, big sur, box, box drive, macos, macos 11, py2app, python, reverse-engineering, uncompyle, uncompyle6]
---

Because Box has opted not to early-release a patch for Box Drive that is compatible with macOS Big Sur beta, I decided to reverse-engineer the app and patch it myself. Using uncompyle6 and learning a bit about py2app, I was able to get Box Drive functioning again on Big Sur. ([see solution on github](https://github.com/slw07g/boxdrive-patch))

## Getting Started

To attempt to get more information about what was causing Box Drive to fail to launch, I tried executing the Box binary directly via the command line. The error output indicated there was some python in play. Based on the output, it appeared the Box app had trouble loading the CoreServices Framework. Hmm let’s see what that about?

```bash
%> /Applications/Box.app/Contents/MacOS/Box 
Traceback (most recent call last): 
File "/Applications/Box.app/Contents/Resources/__boot__.py", line 98, in <module> _run() 
File "/Applications/Box.app/Contents/Resources/__boot__.py", line 82, in _run exec(compile(source, path, 'exec'), globals(), globals()) 
File "/Applications/Box.app/Contents/Resources/bfd_main.py", line 21, in <module> from box.app.sync_app_delegate import SyncAppDelegate 
File "box/app/sync_app_delegate/__init__.pyc", line 9, in <module> 
File "box/app/sync_app_delegate/mac_sync_app_delegate.pyc", line 13, in <module> 
File "LaunchServices/__init__.pyc", line 9, in <module> 
File "CoreServices/__init__.pyc", line 15, in <module> 
File "CoreServices/LaunchServices/__init__.pyc", line 17, in <module> 
File "objc/_dyld.pyc", line 122, in pathForFramework 
File "objc/_dyld.pyc", line 117, in dyld_find 
File "objc/_dyld.pyc", line 88, in dyld_framework 
ImportError: Framework CoreServices could not be found 
2020-06-28 23:44:47.787 Box[18421:1504317] Box Error
```

## The root cause

In macOS 11, shared dynamic libraries (frameworks) have been moved into a cache file, so checks to see if they exist on the file system will fail because – well, they don’t exist on the file system anymore. However, to load them from the cache, one must still specifying their paths as if they still existed on the file system. Confusing right? `dlopen()` just knows what to do. The following is from the macOS 11 beta release notes:

> New in macOS Big Sur 11 beta, the system ships with a built-in dynamic linker cache of all system-provided libraries. As part of this change, copies of dynamic libraries are no longer present on the filesystem. Code that attempts to check for dynamic library presence by looking for a file at a path or enumerating a directory will fail. Instead, check for library presence by attempting to `dlopen()` the path, which will correctly check for the library in the cache. (62986286)

[https://developer.apple.com/documentation/macos-release-notes/macos-big-sur-11-beta-release-notes](https://developer.apple.com/documentation/macos-release-notes/macos-big-sur-11-beta-release-notes)

It’s good to know that `dlopen()` will handle loading the dynamic libraries from the cache, because the `LoadLibrary` method from Python’s `ctypes.cdll` module utilizes `dlopen()`. This will work to our advantage later.

## Slight tangent – Reverse-engineering py2app bundles

The Box application (`/Applications/Box.app/Contents/MacOS/Box`) was a mach-o binary, not python. The `.pyc` files listed in error output were not present anywhere in the Box app’s subfolders. So, then my goal became finding out how the Box app was packaged from Python source code; this would help me understand how to get to the python modules. After reviewing some information on freezing python code, I identified possible tools that could have been used to “freeze” Box.

I came across the [py2app](https://py2app.readthedocs.io/en/latest/) bundler. When I used grep to search for the keyword py2app, there was a hit on the Box mach-o binary. So, then I continued on the assumption that I was working with a py2app bundled application. After reading further into py2app, I learned I should find what I was looking for (the compiled python modules) in a zip archive located in the `<app_root>/Content/Resources/lib/` directory, namely `/Applications/Box.app/Content/Resources/lib/python37.zip`. Once I copied the zip to a staging location and unzipped it, I could see all the `.pyc` files I was looking for.

## The Patching Methodology (py2app)

It might be helpful to some if I describe the general process I’ll be following.

1.  Decompile the offending file(s) such as `objc/_dyld.pyc` as referenced in the error output.
2.  Modify the python code
3.  Recompile the modified python code
4.  Overwrite the original `.pyc` file(s)
5.  Zip up all the `.pyc` files
6.  Replace the original `python37.zip` with mine.
7.  Test the Box app to see if any new errors arise.
8.  Repeat if necessary

## Applying the Methodology

I used [uncompyle6](https://pypi.org/project/uncompyle6/) to decompile the `.pyc` files I was interested in, modified the code accordingly, and used the command `python3.7 -m compileall <filepath>` to recompile the modified code. Then, I overwrote the original `.pyc` file with my new one and zipped up the staging directory and replaced the original `python37.zip` with mine. Once I worked out all the Frameworks issues, the Box app still encountered some run-time issues; the app would launch, the Box Drive file system would mount, but there was also an error dialog box that popped up and Box Drive would eventually crash. To troubleshoot these issues, I had to use the Box app’s logging capabilities, and identify errors in the output. It turned out there was additional code that needed patching. Here’s a summary of shell commands I used to accomplish what I mentioned above, including replacing `python37.zip`, and launching the Box app with verbose logging:

```bash
uncompyle6 -o /tmp objc/_dyld.pyc
vi /tmp/_dyld.py # modify python code
python3.7 -m compileall /tmp/_dyld.py
cp /tmp/__pycache__/_dyld.pyc objc/_dyld.pyc
zip -r ../python37_.zip . # While in the staging directory where python37.zip was unzipped
sudo mv ../python37_.zip /Applications/Box.app/Contents/Resources/lib/python37.zip; /Applications/Box.app/Contents/MacOS/Box -c -v -lf /tmp/box.log
```

I’ve done this work already and made the replacement `python37.zip` available along with the a script that copies it to the appropriate path. You can find these at my github repo [https://github.com/slw07g/boxdrive-patch](https://github.com/slw07g/boxdrive-patch).

### Nuances

-   The 37 in `python37.zip` refers to the major and minor version of Python that compiled the python code. Thus, one would need to use Python 3.7 to compile the patched code (or alternatively decompile and recompile every file with your preference of python version)
-   The Box Fuse Kernel extension also doesn’t load automatically on Big Sur. I describe this manual step in the README file located in my [github repo](https://github.com/slw07g/boxdrive-patch).
