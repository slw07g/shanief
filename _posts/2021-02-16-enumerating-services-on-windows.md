---
layout: post
title: "Enumerating Services on Windows"
date: 2021-02-16
categories: [Knowledge, Reverse Engineering]
tags: [forensics, persistence, powershell, process hacker, services, threat hunting, windows, wmic]
---

Whether your hat is blue or red, it can be beneficial to know how to enumerate the services running on a windows host. Services can be a convenient way for an attacker to establish Persistence. Because Windows often has a lot of benign services, it can be difficult to eyeball a malicious service using the native Service Manager in Windows.

One tool I like to use to inspect services is [ProcessHacker](https://processhacker.sourceforge.io/) – it’s also very useful for basic process monitoring. If you consider using ProcessHacker, just be aware that some anti-virus signatures may classify ProcessHacker as a [hacking tool](https://www.trendmicro.com/vinfo/us/threat-encyclopedia/malware/hacktool). This doesn’t mean it’s malware – it’s just a tool that could be used to facilitate an attack.

## Enumerating Services via WMIC (wmic.exe)

Let’s just get into it…What’s interesting about services is that they execute a single command (path to an executable and arguments) persistently or on-demand; a service may start each time the system boots. An attacker can abuse this functionality to create persistent backdoor access to a compromised machine. I’ve seen malicious services on Domain Controllers configured to execute a PowerShell command that executes a download cradle. I’ll show you how to enumerate services on a Windows host, maybe in another post I’ll also show how to create a malicious service and identify it.

To get a list of all the services and their corresponding commands, you can query WMIC like so:

```cmd
wmic.exe service get name,pathname,startname
```

With this command we query all services from WMIC, only retaining the name and pathname fields.

There are other fields we could include in the results as well, such as `ServiceType`, `StartMode`, and `startname`. You can filter the output of the command by piping it to the `findstr` command. Let’s say I’m hunting for services that executing binaries residing in non-standard paths; I would want to exclude `C:\Windows\System32\*`, `C:\Program Files\*` and `C:\Program Files (x86)\*`, which should drastically minimize the results:

```cmd
wmic service get name,pathname | findstr.exe /V /I /R "C:\WINDOWS\system32" | findstr.exe /V /I /R "C:\Program Files.*" | findstr.exe /v /i "^$"
```

## Enumerating Services via WMIC (PowerShell)

Now, because we can query this information via wmic.exe, we can likely query this data using PowerShell’s `Get-WmiObject` cmdlet. This allows you to manipulate the data more directly – if you so choose to – rather than limiting you to finding patterns in the output. It turns out this is possible:

```powershell
Get-WmiObject -Query "select * from win32_service" | Format-Table -Property Name,PathName 

Get-WmiObject -Query "select * from win32_service" | Where-Object {$_.PathName -notlike "C:\WINDOWS\System32*" -and $_.PathName -notlike "C:\Program Files*"} | Format-Table -Property Name,ServiceType,StartMode,PathName,StartName
```

The first command will yield all services on the computer, while the second command excludes Services whose PathName contains the patterns `C:\Windows\System32` or `C:\Program Files`. We can see the PowerShell method yields the same results as the `wmic.exe` + `findstr.exe` method.

Note that in the filtered list of services (if I had a screenshot) a suspicious service named `EvilService`. While the command in the screenshot is truncated, from what it appears the service appears to be downloading arbitrary PowerShell code from the Internet and executing it.

## Removing Malicious Services

Once you have identified the name of a service you wish to remove, it is straightforward to use the native Services management console or ProcessHacker to remove or disable the service. If you wish to do this via command line, then it is worth noting that every service has a corresponding subkey in the registry, under `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\`. The subkey contains the configuration parameters for the Service, as shown in the screenshot below.

Using the `EvilService` as an example, I would find that registry key at `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EvilService`. To remove the Service, it is sufficient to delete the registry key and then reboot your computer. Alternatively, you can disable the service setting its start value to 4 (and reboot). More information on service start codes are [here](https://docs.microsoft.com/en-us/dotnet/api/system.serviceprocess.servicestartmode?view=dotnet-plat-ext-5.0). If done incorrectly, modifying the system registry can cause technical issues, so tread carefully.

So, there you have it: a couple of quick ways to enumerate the services on hosts. Since we know the location of services in the registry, one could also write a script (or a PowerShell one-liner) to iterate through the Services subkeys and extract the Service information. A tool that parses an offline registry hive file and extracts this information is useful in situations where you analyze artifacts from an offline host rather than interacting with a live host.

## Threat Hunting Wisdom

For the sake of illustrating how to filter services from the results, I only showed All Services and filtering out services that have `C:\Windows\System32` and `C:\Program Files` in the command line. If you are hunting for threats, it would be best to use narrower filters to reduce the possibility of filtering out real threats. Case in point – had I used `C:\Windows\System32\cmd.exe` rather than just `cmd.exe` in the `EvilService` example, it would have been excluded.

## Appendix

Here are some additional properties you can query about Services:

```
Name : TrustedInstaller 
Status : OK 
ExitCode : 0 
DesktopInteract : False 
ErrorControl : Normal 
PathName : C:\WINDOWS\servicing\TrustedInstaller.exe 
ServiceType : Own Process 
StartMode : Manual 
AcceptPause : False 
AcceptStop : False 
Caption : Windows Modules Installer 
DelayedAutoStart : False 
Description : Enables installation, modification, and removal of Windows updates and optional components. If this service is disabled, install or uninstall of Windows updates might fail for this computer. 
DisplayName : Windows Modules Installer 
Started : False 
StartName : localSystem 
State : Stopped 
SystemName : DESKTOP-2C3XXXX
```
