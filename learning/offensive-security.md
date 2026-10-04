---
layout: page
title: "Offensive Security 101"
permalink: /learning/offensive-security/
---

[← Back to Learning](/learning/)

Everything in triage and incident response exists to catch and stop what offensive security teaches you to do. Understanding the attacker's methodology is what makes both of those disciplines sharper.

## Attack Methodology

**Reconnaissance**
Gather information about the target before touching it directly where possible. Passive recon: WHOIS, DNS records, certificate transparency logs, employee and technology footprint from public sources. Active recon: port scanning, subdomain enumeration, directory brute-forcing once you have authorization to touch the target directly.

**OS/Application Fingerprinting**
Identify exactly what you are dealing with. Banner grabbing, response header analysis, and tools like `nmap -sV` for service and version detection. The specific version matters. A generic "this runs Apache" tells you nothing; "this runs Apache 2.4.49" tells you to check for a specific, well-documented path traversal vulnerability.

**Identify a vulnerability**
Match what you found in fingerprinting against known CVEs, and separately look for misconfigurations that will not show up in any CVE database: default credentials, exposed admin panels, verbose error messages leaking internal paths, overly permissive file uploads.

**Craft Exploit**
Take a public proof-of-concept and adapt it to your specific target, or write one from scratch when nothing public exists. This is where you actually learn the vulnerability, adapting a PoC forces you to understand why it works instead of just running it.

**Pwn**
Get code execution or access. This might be a shell, might be reading a file you should not have access to, might be an authentication bypass. Whatever the initial foothold is, confirm exactly what access it actually grants you.

**Repeat until root access achieved**
Initial access is rarely full access. Privilege escalation, pivoting to other hosts, and repeating the entire methodology from that new vantage point is normal, not a sign you did something wrong the first time. Full compromise is usually the result of chaining several smaller footholds together, not one clean exploit.

## Practice

**HackTheBox**
A library of intentionally vulnerable machines spanning difficulty levels. Use it to apply the methodology above against a real, unfamiliar target instead of following a tutorial. Start with easy-rated boxes, and write a full report for every one you complete: recon findings, the vulnerability, the exploit, and the privilege escalation path. The writeup is where the learning actually consolidates.

**TryHackMe**
More guided than HackTheBox, with structured learning paths that walk through a concept before putting you in a room to apply it. This is the better starting point if you are new to offensive security and need the scaffolding before working unguided.

## Beyond the practice

Clicking through a guided room or even fully rooting an unguided box gets you comfortable with the mechanics. It does not automatically get you fluent. The next step is forcing yourself past the point where a tool does the thinking for you.

**Automate your attacks end to end with scripting**
Take a box you have already rooted manually and write a script that reproduces the entire chain, recon through root, without you clicking anything. This is harder than it sounds, because a script cannot get away with the vague, half-understood steps that a human can paper over in the moment. You will hit places where you thought you understood a step and discover you only knew how to click through it. That gap is exactly what to go learn next.

**Write up how you captured the flag, and publish it**
A private report is good. A public writeup is better. Explaining how you got from recon to root for someone who has never seen the box forces you to understand every step well enough to teach it, and the places where you struggle to explain a step are the places you did not really understand it. Your perspective is also useful to other people. Someone stuck on the same box, or the same vulnerability class, may find that your explanation is the one that finally clicks.

It also builds a professional habit. A penetration test is only as good as its report: what you did, when you did it, what you found, and how someone else can reproduce it. Documenting every action as you go during a CTF is the same discipline a real engagement demands, practiced where the stakes are low. Take timestamped notes and screenshots while you work, not afterward from memory.

Check each platform's rules before you publish. HackTheBox, for example, only permits public writeups for retired machines and challenges.

**Use AI**
Use it to accelerate the parts that are pure friction, drafting exploit code, parsing dense tool output, explaining an unfamiliar vulnerability class. Do not use it as a replacement for understanding what the output does. If you cannot explain why the exploit it generated works, you have not learned the vulnerability, you have just automated your own confusion. Verify everything it gives you against the actual target and the actual documentation before you trust it.
