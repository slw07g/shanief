---
layout: page
title: "Investigations & Triage 101"
permalink: /learning/investigations-triage/
---

[← Back to Learning](/learning/)

Triage is the discipline of taking an alert, which is a claim that something bad happened, and turning it into a decision backed by evidence. Everything below is the process for doing that consistently, at speed, without guessing.

## Playbooks

A playbook is the pre-written decision tree for a specific alert type. It exists so the analyst is not designing an investigation from scratch at 2 a.m. under pressure. A usable playbook contains:

- **The trigger**: exactly what condition fired the alert and what it is supposed to detect.
- **The decision tree**: the ordered set of checks to run, each one branching based on what you find.
- **The queries**: the actual log searches, EDR queries, or API calls needed at each branch, written out and ready to run, not described in prose.
- **The escalation path**: who gets pulled in, and at what point, if the evidence points toward impact.
- **The closure criteria**: what has to be true for you to close this out with confidence.

Write the playbook before the alert fires, not during. If you are writing your decision tree while the clock is running, you are not triaging, you are researching.

## Hypothesis / Questions

Before you open a single log, state what you think happened. A working hypothesis gives your investigation direction and a way to know when you are done. Start with:

- What is the alert telling me happened, in plain language?
- What would I expect to see in the logs if that is true?
- What would I expect to see if this is legitimate activity that looks similar?
- Who is the user or asset involved, and is this behavior normal for them?
- What is the maximum possible blast radius if the worst-case version of this is true?

You are not trying to prove your first guess right. You are trying to find the evidence that would prove it wrong, because that is what actually tells you something.

## Evidence / Logs

Your evidence sources depend on the alert, but the core set an analyst pulls from repeatedly:

- **EDR telemetry**: process trees, file writes, network connections, registry changes.
- **Authentication logs**: identity provider logs (Okta, Azure AD), VPN logs, MFA event logs.
- **Network logs**: firewall, proxy, DNS.
- **Cloud audit logs**: CloudTrail, GCP Audit Logs, Azure Activity Log.
- **Email gateway logs**: headers, delivery status, click-time protection verdicts.

Two habits matter more than the source list. First, normalize timestamps to a single timezone (UTC) before you start building a timeline, or you will misorder events without realizing it. Second, preserve the raw log data you pulled, not just your notes about it, before it ages out of retention. Your conclusion has to be reproducible from the evidence, not just from memory.

## Disposition

Every investigation ends with a disposition. The standard set:

- **True Positive**: the alert correctly identified malicious or policy-violating activity.
- **False Positive**: the alert fired on activity that was not what it claims to detect.
- **Benign True Positive**: the alert correctly identified the activity, but the activity itself was authorized or expected (a pentest, an admin script).
- **Escalate to Incident**: evidence confirms actual impact, and this moves out of triage and into incident response.
- **Need More Information**: you cannot reach a confident disposition with the evidence available, and you are naming what is missing.

The disposition is not the label. It is the label plus the reasoning that produced it, written down in enough detail that someone else could review your work and reach the same conclusion.

## Alerts are security events until confirmed an incident

This is the operating principle underneath everything above. An alert is a claim, not a fact. Treating every alert as a confirmed incident burns out the team and buries real signal under noise. Treating every alert as noise until proven otherwise misses the ones that matter. The job of triage is to close that gap with evidence, fast, and only escalate the label once impact is actually confirmed: unauthorized access, data exfiltration, execution of malicious code, or a policy violation with real consequence.

## Example alerts to walk through

### User-reported phishing

1. Pull the full email headers. Check SPF, DKIM, and DMARC results, not just whether the sender name looks right.
2. Check the sending domain against known-bad and against your own historical mail flow. Is this a new domain, a lookalike domain, or a compromised legitimate account?
3. Search for the same sender or subject line across the rest of the mailbox environment. One report from one user is different from fifty reports across the org.
4. Check whether the link was clicked. Pull proxy or secure web gateway logs for the URL. If it was clicked, check EDR and identity logs for what happened immediately after: credential entry, MFA prompt, unusual login.
5. If there was an attachment, check whether it executed. Pull the hash and check it against your EDR and any available sandbox result.
6. Disposition: if no click and no execution, likely false positive or blocked benign true positive. If credentials were entered, escalate immediately, this becomes an account compromise investigation and likely an incident.

### EDR - Malware detected

1. Check the verdict detail: was it blocked pre-execution, quarantined post-execution, or allowed to run and only flagged after the fact? This changes everything downstream.
2. Pull the process tree. What spawned it? A user double-clicking a downloaded file looks very different from a process spawned by an Office macro or a scheduled task you did not create.
3. Check the file hash against threat intel and your own EDR's reputation data. Known commodity malware versus something unrecognized changes your urgency and your next steps.
4. If it executed, check for persistence: new scheduled tasks, registry run keys, new services, new local accounts.
5. Check for lateral movement from the host: new outbound connections, authentication attempts to other systems, use of built-in admin tools (PsExec, WMI, PowerShell remoting) shortly after execution.
6. Disposition: blocked pre-execution with no persistence and no lateral movement is usually a closed true positive at the endpoint level. Any confirmed execution plus persistence or lateral movement is an escalation.

### Okta suspicious activity

1. Identify exactly what triggered the detection: impossible travel, new device fingerprint, anomalous ASN, or a risk score threshold.
2. Check the MFA method used on the flagged login. Push notification approved after multiple rapid prompts (push bombing) is a very different finding than a hardware key or number-matching MFA.
3. Check what the session did after authenticating: which applications were accessed, whether any downloads occurred, whether any new MFA factors or recovery methods were registered.
4. Correlate the source IP and ASN against known VPN/proxy providers, prior logins for this user, and any threat intel hits.
5. Check whether the user actually attempted that login. Ask them directly if it is ambiguous. Do not skip this step because it feels slow, a two-minute conversation resolves a large share of these outright.
6. Disposition: a user-confirmed, geographically explainable login (new location while traveling, new device just set up) is a false positive. An unconfirmed login, a push-bombing pattern, or any post-login change to account recovery settings is an escalation.
