---
layout: post
title: "Starting a Career in Information Security"
date: 2022-07-04
categories: [Career, Education]
tags: [career, cyber, education, entry level, experience, infosec, jobs, security engineer, skills, soc analyst]
---

People often ask me how they can transition into an information security (Infosec) career. Most security positions tend to require some relevant work experience, which creates an awkward barrier to entry. I am recommending some paths to the industry given high demand and low supply of Information security professionals.

## Organizational Design and Implementation

It might be helpful to provide the typical structure of security organizations. Private sector security organizations typically consist of several teams with different focus areas, such as:

- Threat Intelligence
- Detection Engineering
- Incident Response
- Adversarial Simulations
- Application Security
- Platform/Infrastructure Security
- Risk Management

These teams typically include the following roles:

- Analysts
- Security Engineers
- Security Architects
- [Technical] Program Managers
- Engineering Managers
- Directors
- …Leadership…

## SOC Analyst

Most technical folks that begin their first Infosec role as an entry level SOC analyst. Triaging alerts and resolving them gives them visibility into the various threats that are out there. In a corporate SOC, alerts you typically pertain to potential malware infections, use of prohibited applications, user-reported phishing emails, etc… SOC analysts are the first to triage these alerts to help determine if any mitigative actions are necessary – for example if a user was phished, a SOC analyst may conclude that the user’s password needs to be rotated, and progress the incident as needed – or if the user never clicked the malicious link, then no further action is needed beyond deleting the e-mail.

Many SOCs will require 24/7 monitoring, so SOC analyst roles tend to have a variety of shifts to choose from. Some ways to make up for multiple shifts may be to hire staff in different geographical regions whose daytime hours cover the “off-hours”. Another alternative is having an on-call rotation of people who will responsible for answering pager notifications at all hours.

### How do I land a SOC analyst role?

There is a very high demand for security talent, and a short supply – allegedly. I know there are a lot of people that want to break through in the security industry, but they do not realize they have work experience that translates to a security role. A lot of times IT help desk employees move laterally into a SOC Analyst role. IT Helpdesk roles will help with growing a lot of soft and technical skills.

Once you land an entry level security role, the hard work doesn’t stop. Continue growing the necessary skills to reach the next level, or to transition into a security role more aligned with your interests.

### Okay, but what if I don’t have any IT Helpdesk experience?

If you do not have any experience, then the best way to go is demonstrating your cognitive ability. One way to do this is to pursue a certification that incorporates various security fundamentals. A certification doesn’t make you an expert, it just shows you are able to learn concepts that pertain to security. The CompTIA Security+ certification can be a good start for an entry level SOC analyst role. To get a better understanding of skills and certifications are sought after in a SOC analyst, review various job postings for such roles. That applies for any role.

### I don’t want to hit the books though

And you don’t have to! You can do some home lab and coding projects on your own that demonstrate your knowledge of security concepts. For example, you could set up some virtual machines and simulate a DNS hijacking attack. You might then stand up some additional infrastructure that allows you to detect such an attack. Afterwards, you may write a blog that highlights what you did and learned, what tools you used, and why you selected them. Ultimately, you likely will learn more by doing hands-on exercises than just taking exams. However, setting up labs and understanding the attacks, will still require a good amount of research and thought.

A more fun way to get more technical experience might be to attempt Capture-The-Flag events and challenges. [HackTheBox](https://www.hackthebox.com/) is probably one of the more popular platforms that offer this, which means if you get stuck, there’s likely a write-up or YouTube video you can reference. Working through the challenges is just part of it, but there’s additional opportunity to learn and demonstrate what you’ve learned by drafting and sharing your own write-ups explaining the steps you’re taking and why you’re taking them. Try to write about how you might detect your hacks if you were a blue teamer. There’s lots of opportunities to get coding experience by writing scripts to automate some of the hacks you do. Set a goal to write a script for each box, such that when you run it, your target will connect to your reverse shell (or you to your target’s bind shell). This is a great way to build a portfolio.

## Security Engineer

Starting in a Security Engineering role typically requires a solid understanding of various security concepts. Additionally, experience with writing code, integrating systems, and problem solving are also expected. Security Engineers need not be as great at coding as software engineers; don’t fret over Leetcode.

Some skills that are sought after in Security Engineers often include:

- **Coding**
    - Python and golang seem to be the most popular in Infosec
    - Object-oriented programming
    - Data Structures
    - Loops
- **Logs**
    - Parsing
    - Searching/Correlation
- **Working with Cloud infrastructure**
    - AWS/Azure/GCP
    - Terraform
- General understanding of cryptography
- Threat detection
- Familiarity with Linux operating systems

A personal project where you implement a virtual “home lab” can expose you to many of these skills. As engineers progress through their careers, they will find that many organizations will expect them to manage projects. So, experience breaking down into tasks and milestones and driving the project to completion/launch, is highly sought after.

## Security Architect

A security architect tends to have a high level vision of how multiple systems can be leveraged to implement a business’s desired security posture. Security architects help with defining a lot of the company-wide policies and processes that pertain to security. If there are any gaps in processes that create a weakness in the overall posture, the architect helps with reconciling those gaps.

## [Technical] Program Managers

Don’t worry if you don’t have a technical background. There are still Infosec opportunities for you! Program managers and Technical program managers do not require much hands-on technical work, they are more focused on ensuring projects are meeting deadlines and staying within budget. Program managers may help with resolving blockers – or bringing the right stakeholders to the table to resolve them. They also ensure key project tasks are being tracked and help with communicating project milestone up the chain.

## Manager, Director, etc…

Managers and higher level roles in Security are not much different than those outside of Security. Their goals are to lead with a vision that’s aligned with the companies goals. They leverage the team(s) reporting into them to implement said vision. Their goals should also include the professional development of their reports. Managers and Directors need not have a deeply technical background. However, it does help if they can navigate technical conversations with individual contributors.

## What did you do?

Each time you ask any security professional how they started their Infosec career, you will likely hear a unique story. Everyone’s path is different. But Me? I actually began my security career as a field Computer Scientist at the FBI immediately after graduate school. As for experience, I had degrees in Computer Science, Information Security Policy & Management, and some relevant security engineering experience from an internship.

As a Computer Scientist, I got to solve technical problems that hindered investigations however I saw fit. This allowed me the opportunity to learn and level-up many skills at my own pace. I worked on digital forensics, reverse-engineering malware, coding/scripting, and explaining deeply technical topics for non-technical audiences. The FBI paid for me to take SANS courses and their corresponding GIAC exams. Over a short period of time, I was able to obtain quite a few certifications this way.

After working at the FBI for a few years, I joined Google’s Security Surveillance Team. This was like a more advanced SOC with a lot of automations. It was staffed with security engineers who built and/or integrated existing stacks into their detection pipeline. And I’ve been doing blue team work – Detection Engineering, Incident Response, Threat Hunting, etc… – ever since.
