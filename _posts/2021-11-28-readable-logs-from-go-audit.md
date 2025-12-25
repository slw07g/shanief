---
layout: post
title: "Human-readable Auditd Logs via go-audit"
date: 2021-11-28
categories: [Knowledge, Linux Security]
tags: [auditd, go, go-audit, golang, json, linux, logging, logs]
---

Human readable go-audit (auditd) logs are here!

## TL;DR

I created a fork of Slack’s go-audit [here](https://github.com/slw07g/go-audit) that generates human readable logs.

## What is go-audit?

Go-audit is an open-source [tool](https://github.com/slackhq/go-audit) by [Slack](https://slack.com) that transforms auditd events into JSON format. The JSON logs in their current form aren’t useful unless you have [ETL](https://www.xplenty.com/blog/what-is-etl/) to make them human readable. “What is auditd,” you ask? Auditd logs syscalls and provides context around them – such as when a process spawns a new process, makes a network connection, or accesses a file.

Here’s a sample event from go-audit for the creation of a process with the command `tail go-audit.log`

```json
{ "sequence": 461256, "timestamp": "1638049196.855", "messages": [ { "type": 1300, "data": "arch=c000003e syscall=59 success=yes exit=0 a0=7ffc016f3c30 a1=7f52a5e831b8 a2=560ae0b54c40 a3=8 items=3 ppid=82570 pid=683363 auid=1000 uid=1000 gid=1000 euid=1000 suid=1000 fsuid=1000 egid=1000 sgid=1000 fsgid=1000 tty=pts3 ses=2 comm=\"tail\" exe=\"/usr/bin/tail\" subj==unconfined key=(null)" }, { "type": 1309, "data": "argc=2 a0=\"tail\" a1=\"go-audit.log\"" }, { "type": 1307, "data": "cwd=\"/home/user/go-audit\"" }, { "type": 1302, "data": "item=0 name=\"/usr/bin/tail\" inode=1001091 dev=08:01 mode=0100755 ouid=0 ogid=0 rdev=00:00 nametype=NORMAL cap_fp=0 cap_fi=0 cap_fe=0 cap_fver=0 cap_frootid=0" }, { "type": 1302, "data": "item=1 name=\"/usr/bin/tail\" inode=1001091 dev=08:01 mode=0100755 ouid=0 ogid=0 rdev=00:00 nametype=NORMAL cap_fp=0 cap_fi=0 cap_fe=0 cap_fver=0 cap_frootid=0" }, { "type": 1302, "data": "item=2 name=\"/lib64/ld-linux-x86-64.so.2\" inode=918494 dev=08:01 mode=0100755 ouid=0 ogid=0 rdev=00:00 nametype=NORMAL cap_fp=0 cap_fi=0 cap_fe=0 cap_fver=0 cap_frootid=0" }, { "type": 1327, "data": "proctitle=7461696C00676F2D61756469742E6C6F67" } ], "uid_map": { "0": "root", "1000": "user" } }
```

## Cool, but why does this matter?

So, as you can see in the sample above, each auditd event consists of multiple messages which go-audit stores in an array, nested in JSON. Each message may have its own string of key-value pairs. The JSON structured as-is makes the data easy to ingest but it is difficult to use this data without first transforming it into a more simplified structure. Other things about the structure that hinder immediate use of these logs are:
- some values are hex-encoded such as `proctitle` this sample above
- each message may have key-value pairs that need parsing
- Depending on the message type, additional transformation may be necessary after parsing certain key-value pairs
- integers represent message and syscall types rather than descriptive strings

That is, if I want to ingest these logs as-is into Splunk, Datadog, or Devo and build detections based on them, hen there would be a bit of overhead to extract meaningful information from the logs and transform them such that they are easy to understand when reviewed. There is the [Logstash filter](https://github.com/mwielgoszewski/logstash-filter-goaudit) that mwielgoszewski created which performs this [ETL](https://www.ibm.com/cloud/learn/etl) on go-audit logs, however, I could not find any similar implementations of this to do this ETL outside Logstash. So, I figured I would fork the go-audit repo and re-factor the code to do the extraction and transformation itself if an optional setting is specified. This directly produces readable logs from go-audit.

## Shameless Plug

You can find my fork of go-audit at [https://github.com/slw07g/go-audit](https://github.com/slw07g/go-audit). Here’s an example of what the transformed log looks like:

```json
{ "arch": "c000003e", "arch_name": "x86_64", "args": { "a0": "tail", "a1": "go-audit.log", "argc": "2" }, "auid": "1000", "bits": "64", "cap_fe": "0", "cap_fi": "0", "cap_fp": "0", "cap_frootid": "0", "cap_fver": "0", "comm": "tail", "cwd": "/home/user/go-audit", "dev": "08:01", "egid": "1000", "endianness": "little", "euid": "1000", "exe": "/usr/bin/tail", "exit": "0", "fsgid": "1000", "fsuid": "1000", "gid": "1000", "host": "kali-osed", "inode": "918494", "item": "2", "items": "3", "key": "(null)", "mode": "0100755", "name": "/lib64/ld-linux-x86-64.so.2", "nametype": "NORMAL", "ogid": "0", "ouid": "0", "pid": "683363", "ppid": "82570", "proctitle": "tail go-audit.log", "rdev": "00:00", "session": "2", "sgid": "1000", "success": "yes", "suid": "1000", "syscall": "59", "timestamp": "1638049196", "tty": "pts3", "type": "execve", "uid": "1000", "user": "user" }
```

As I was writing this, I noticed there’s a bug that I need to squash :D. Leave a comment if you can spot the bug!
