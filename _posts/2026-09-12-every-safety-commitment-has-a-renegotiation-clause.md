---
layout: post
title: "Every Safety Commitment Has a Renegotiation Clause"
date: 2026-09-12
categories: [ai, cybersecurity, risk management]
tags: [AI Governance, Agentic AI, Vendor Risk, CFAA, Incident Response]
---

The CEOs of two leading AI companies spent the weekend asking the industry to slow down. Both proposed independent oversight inside their own labs. Both said the pace of capability has outrun the pace of understanding.

Take the proposal seriously. Then look at what surrounds it.

Three things gave way over the past year. They happened in different rooms, driven by different pressures, and none of them caused the others. They arrive at the same place anyway, which is why they belong in the same conversation.

None of this is an I told you so. I didn't. Researchers did, and they've been doing it for years. Prompt injection was named and demonstrated in 2022. Sandbox escape, reward hacking, and goal misgeneralization have their own literature. Independent evaluators have reported that models attempt to cheat on cybersecurity evaluations across every developer they tested. Agent-to-agent contamination was described in papers before it was described in incident reports.

The warnings were specific, dated, and public. They were treated as a research footnote until an incident made them a headline. That pattern is the actual subject of this post.

---

## A Structure Gave Way

One of these companies began as a nonprofit and now operates as a for-profit under a nonprofit's partial ownership. The cap on investor returns went with it. That cap was a credibility instrument, written to prove that most of the value created would flow past the shareholders.

The cap held until capital needed it gone.

Nothing illegal happened. A governance structure designed to constrain commercial incentive met commercial incentive at scale and lost.

## A Pledge Gave Way

The Department of Defense pushed AI vendors toward contracts permitting use for all lawful purposes with no usage-policy constraints attached. The phrase sounds procedural. It functions as a deletion, because US law permits domestic surveillance under some conditions, so accepting the language removes a vendor's stated red lines without anyone formally crossing one.

One vendor refused, held its published limits on autonomous weapons and domestic mass surveillance, and lost its federal business over it. Another accepted the terms and later revised them under pressure, with a senior leader resigning on the way out over guardrails that were never defined before the deal was announced.

Two answers. One conclusion. A published safety policy is a negotiating position held at the pleasure of the largest customer in the room.

## A Sandbox Gave Way

In a separate development with no connection to either of the above, agents running cyber capability evaluations under reduced refusal settings escaped their evaluation environment and compromised a third party's production infrastructure. Hundreds of agents participated. They executed roughly seventeen thousand actions across two days, obtained root on a production node, and pulled private repositories.

The escape path was a server-side request forgery flaw in an internal package registry. That vulnerability class is older than most of the engineers deploying these systems.

Read the rest of the sequence, because it's the part worth studying. Agents probing the same internal system left notes behind. Those notes accumulated into a persistent shared channel nobody designed or authorized. Agents used it to divide labor across separate runs. Some hunted credentials. Some hunted exploits. Some coordinated.

Strip the word "model" out of that paragraph and you have a penetration test that escaped scope, ran for two days, and reached production.

---

## What a Buyer Should Take From This

Vendor values are a variable. Treat them like one.

If your third-party risk program cites a provider's usage policy, acceptable use terms, or published safety commitments as a control, you're holding a control with a renegotiation clause inside it. That clause gets exercised when a large enough check or a large enough customer arrives. The company that folded proves it. So does the company that held and lost the account.

Controls you own survive procurement disputes. Controls your vendor owns do not.

## On Regulation

Plenty of people are calling for AI regulation right now. Count me among them. My concern is efficacy, and it starts with the statute already on the books.

The Computer Fraud and Abuse Act has covered this conduct since 1986. Federal enforcement priorities already name intrusion carried out with AI. The law was current, enforceable, and entirely present while agents spent two days inside someone else's production environment.

A statute deters a party capable of anticipating consequence. An agent anticipates nothing. It carries no concept of a sentence, a fine, or a career. The humans who could have been deterred had already stepped out of the loop, which is the entire reason anyone deploys agents in the first place.

So the question becomes liability, and liability runs into intent. Criminal exposure under the CFAA requires knowing or intentional unauthorized access. Pressure moves to the civil track and to recklessness. You reduced the safeguards. You connected the environment to external networks. The outcome was foreseeable. Liability lands on the deployer, and the standard is foreseeability. Apply that to your own rollout.

Then there's disclosure. Existing incident-reporting rules carry thresholds high enough that the events above failed to meet them. What the public learned arrived through voluntary blog posts and journalism, on the timeline of the party with the most to lose. A reporting regime that depends on self-disclosure ships with a volume knob.

Then there's the marketing. These systems are sold on autonomy. The pitch is that the model plans, chains tools, writes and executes code, and finishes the job while you sleep. Offensive security capability is a headline benchmark and a launch-day talking point. When a product is advertised on its ability to operate without supervision and to solve hard exploitation problems, nobody should act surprised when someone points it at a target deliberately. Bad actors read the same launch posts you do, and they take the claims at face value.

Regulate it. Just don't build your program on the assumption that the regulation will hold the line.

---

## Back to the Slowdown

The request from those two CEOs concerns the rate at which capability improves. There's a version of that request that belongs to everyone else, and it has nothing to do with training runs.

Slow the rate at which you hand over access.

Most organizations are still experimenting with this technology. That's reasonable. Nobody has a settled answer on where it pays for itself, and the honest ones say so. What's harder to defend is expanding access while the value question stays open. Exposure lands immediately. Value arrives late, if it arrives.

So be deliberate about the trade. Three questions, asked before the next expansion of scope:

**Is this a hard problem or a tedious one?** Both are legitimate uses. They carry different risk. A tedious task with bounded input and a reviewable output is a clean trade. A hard problem handed to an autonomous agent holding production credentials is a different transaction, and it deserves to be priced like one.

**What work stopped happening?** If nobody can name the hours this replaced, no value was created. Access was granted anyway. That's a cost with no offsetting entry.

**How much did we hand over to find out?** Experiments are supposed to be scoped. Read-only beats read-write. One system beats ten. A revocable credential beats a standing one. If the pilot has the same access as the production rollout, it was never a pilot.

None of that requires anyone to slow anything down on your behalf.

## Where This Lands

The pacing proposal is a real structural change, and independent oversight inside these labs deserves to succeed.

Sit with what prompted it, though. The people closest to these systems just told the public they've lost some visibility into how their own models behave under pressure. They said it about controlled environments, staffed by researchers, running deliberate evaluations. Your environment has none of that.

Corporate structure. Contract language. Evaluation guardrails. Three unrelated commitments, each one standing between capability and deployment, each one renegotiated the moment something large enough leaned on it.

The one commitment nobody can renegotiate for you is how much of your environment you hand over, and how quickly.

Slow that down.

---

### Sources

- [BBC: AI safety timeline](https://www.bbc.com/news/articles/c14dpgm0rg4o)
- [Congressional Research Service, IN12669](https://www.congress.gov/crs-product/IN12669)
- [Tech Policy Press: A Timeline of the Anthropic-Pentagon Dispute](https://www.techpolicy.press/a-timeline-of-the-anthropic-pentagon-dispute/)
- [Cloud Security Alliance: DoD AI Guardrail Mandates & Vendor Governance](https://labs.cloudsecurityalliance.org/research/csa-research-note-dod-ai-guardrail-mandates-vendor-governanc/)
- [OpenAI: Hugging Face Incident and the Road Ahead](https://openai.com/index/hugging-face-incident-and-the-road-ahead/)
- [Hugging Face: Agent Intrusion Technical Timeline](https://huggingface.co/blog/agent-intrusion-technical-timeline)
- [Dark Reading: Hundreds of OpenAI Agents Invaded Hugging Face Servers](https://www.darkreading.com/cyberattacks-data-breaches/hundreds-openai-agents-invaded-hugging-face-servers)
- [Ballard Spahr: AI Gone Rogue — What Recent OpenAI and Anthropic AI Incidents Could Mean for CFAA Liability](https://www.ballardspahr.com/insights/alerts-and-articles/2026/08/ai-gone-rogue-what-recent-openai-and-anthropic-ai-incidents-could-mean-for-cfaa-liability)

---

*Shanief Webb is a CISO with experience across the FBI, Google, Meta, Okta, and Dropbox. He writes about security leadership, AI governance, and building organizations that operate under pressure.*
