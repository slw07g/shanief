---
layout: page
title: "Security Incident Response 101"
permalink: /learning/incident-response/
---

[← Back to Security Operations 101](/learning/security-operations/)

Triage tells you something happened. Incident response is everything that happens once you have confirmed it did.

## Incident Management vs Incident Response

These get used interchangeably, and treating them as the same function is where a lot of incidents get handled badly.

**Incident Response** is the technical work: finding the attacker's footprint, understanding scope, stopping the bleeding, removing the foothold, and recovering systems. This is done by security subject matter experts, engineers, and whoever owns the affected system.

**Incident Management** is the coordination layer above that work: running the timeline, managing communication to leadership and affected teams, making the calls that require business context rather than technical depth (do we take the payment system offline, do we notify customers, do we bring in outside counsel), and owning the incident from open to close. This is done by an Incident Commander, and it is a distinct role from any technical SME on the call.

A technically brilliant response with no one managing the incident produces chaos: duplicated work, no single source of truth, and leadership finding out from a customer instead of from you. Assign both roles explicitly at the start of every incident, even a small one.

## Incident Management Lifecycle

**Detection (Declare an incident)**
This is the moment triage's disposition becomes "escalate," and someone with the authority to declare does so. Set a clear, low-friction bar for declaration. It should always be safer to declare and stand down than to hesitate and let something spread. Define ahead of time who can declare and what the declaration actually triggers (a page, a bridge, a channel).

**Analysis**
Confirm scope. What systems, accounts, and data are actually affected, versus what is only suspected. Build a timeline of attacker activity from the evidence. Form a working root cause hypothesis, and keep updating it as evidence comes in rather than anchoring to your first theory.

**Containment**
Stop the immediate spread without destroying evidence you will need later. Short-term containment is fast and reversible: isolate a host, disable an account, block an IP or domain. Long-term containment is the more durable fix that gets you to a stable state while eradication is planned: network segmentation changes, broader credential resets, temporary access restrictions.

**Eradication**
Remove the attacker's foothold completely. This means more than deleting the malware you found: rotate every credential the attacker could have touched, close the vulnerability or misconfiguration that got them in, and hunt for secondary persistence mechanisms they may have planted as a fallback.

**Recovery**
Restore affected systems to normal operation and confirm the fix holds. Bring systems back online in a controlled sequence, monitor closely for signs of reinfection or reconnection, and get explicit sign-off from the technical lead before declaring the environment clean.

**Lessons Learned**
Run a blameless postmortem. The goal is to find every control gap that let this happen or slowed the response, and produce assigned, dated action items to close them. If the same root cause could produce a repeat incident and nothing structural changed, the lessons-learned step failed regardless of how good the writeup reads.

## Incident Command Structure

Borrowed from emergency management, and it works for the same reason: it scales, and it survives people being tired and stressed.

- **Incident Commander**: owns the incident end to end. Makes final calls, drives the timeline, is the single point of accountability. Does not need to be the most senior technical person in the room, needs to be the best coordinator.
- **Communications Lead**: owns all outbound updates, to leadership, to customers, to internal stakeholders. One person controlling the message prevents conflicting information from going out.
- **Technical Lead / Subject Matter Experts**: own the actual investigation and remediation work in their domain (network, endpoint, cloud, application).
- **Scribe**: owns the timeline in real time. Every decision, every finding, every action taken, with a timestamp. This document is what your postmortem and your executive summary get built from, so it has to be maintained live, not reconstructed afterward from memory.

Set a fixed sync cadence (every 30 minutes is a reasonable default for an active incident) so the Incident Commander is pulling status rather than chasing it down ad hoc.

## Documentation

**Executive Summary**
Written for leadership, one page, business-impact first. Lead with what happened, what was affected, what the exposure or damage was, and what is being done. Save the technical detail for an appendix or for the postmortem. If a non-technical executive cannot understand the first paragraph, rewrite it. Start from the [Security Incident Executive Summary Template](https://github.com/slw07g/shanief/blob/master/learning/templates/security-incident-executive-summary-template.md), which also walks through the breach determination and regulatory notification check with legal.

**Postmortem**
The full technical record: timeline, root cause, scope of impact, what worked in the response, what did not, and a list of action items with named owners and due dates. Treat the action items as the actual deliverable. A postmortem with a clean narrative and no completed follow-up is a story, not a fix.

**Templates**
Do not start these documents from a blank page. Adapt these to your organization before you need them, not during the incident.

- [Security Incident Executive Summary Template](https://github.com/slw07g/shanief/blob/master/learning/templates/security-incident-executive-summary-template.md): my template for the leadership summary, covering incident metadata, impact, actions taken by lifecycle phase, and a breach determination and regulatory threshold check for legal sign-off.

Lenny Zeltser also publishes free templates and cheat sheets that are a solid starting point:

- [Incident Response Report Template](https://zeltser.com/incident-response-report-template): a Word and Markdown template built around what happened and when, root cause, what was done, lessons learned, and remaining action items. It is a strong base for your postmortem.
- [How to Write Good Incident Response Reports](https://zeltser.com/good-incident-reports): guidance on writing for your reader, with a downloadable example report.
- [Initial Security Incident Questionnaire for Responders](https://zeltser.com/security-incident-questionnaire-cheat-sheet): the questions to ask in the first hour, covering background, communication, scope, and what has already been done.
- [Critical Log Review Checklist for Security Incidents](https://zeltser.com/security-incident-log-review-checklist): what to look for in Windows, Linux, network, and web server logs. Pair it with the log analysis work below.

## Security Subject Matter Expert

**Log Analysis**
The core skill is correlation: taking events from disparate sources (EDR, identity, network, cloud) and lining them up on a single timeline by timestamp to build a coherent picture of what the attacker did, in what order.

**Evidence Organization**
Keep a central, access-controlled repository for everything collected during an incident: log exports, memory captures, disk images, screenshots. Use consistent naming and note when and how each piece of evidence was collected. If this ever needs to hold up to legal or regulatory scrutiny, an undocumented chain of custody undermines it regardless of how solid the technical finding is.

**Indicators of Compromise**
File hashes, IP addresses, domains, registry keys, and YARA or Sigma rules that identify the specific threat you responded to. Extract these deliberately during the investigation, not as an afterthought, and get them into your detection tooling and threat intel platform (STIX/TAXII or your vendor's equivalent) so the same threat gets caught automatically next time.
