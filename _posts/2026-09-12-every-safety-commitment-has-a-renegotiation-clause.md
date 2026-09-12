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

One of these companies spent years pointing at a single promise as proof it would hold the line against market pressure. It would not train a model past a certain capability threshold unless it could establish in advance that its safety measures were adequate. That commitment was the load-bearing pillar of its scaling policy and a large part of its public identity.

It dropped the commitment in February and said so on the record. The stated reasoning was that unilateral restraint stops making sense when competitors keep moving, and that halting its own training would help nobody.

The replacement policy adds transparency commitments, published safety roadmaps, and periodic risk reports. An outside evaluator who reviewed an early draft called the change understandable, then warned that removing the tripwire invites a slow ramp in danger with no single moment loud enough to trigger a response.

Read the stated reason again. The pledge held right up until holding it carried a competitive cost. That was the entire test, and everyone now has the answer.

A commitment that lasts until it costs something was a preference.

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

All three of those failures happened upstream of you. You didn't write the corporate charter, sign the government contract, or run the evaluation that got loose. You inherit the results regardless.

Integration is how you inherit them. Every system you connect, every dataset you expose, every workflow you route through a model deepens your dependence on commitments held by other people, under pressures you can't see and don't influence. That dependence is the exposure. It grows every time you integrate, and it grows quietly, because integration gets counted as progress.

So the request from those two CEOs has a version that belongs to everyone else, and it has nothing to do with training runs.

Integrate only where the value outruns the exposure. Slow down everywhere else.

Most organizations are still experimenting with this technology. That's reasonable. Nobody has a settled answer on where it pays for itself, and the honest ones say so. What's harder to defend is deepening the integration while the value question stays open. Exposure lands immediately. Value arrives late, if it arrives.

So be deliberate about the trade. Four questions, asked before the next expansion of scope:

**If we turned it off tomorrow, what gets worse?** The strongest value test available, because it measures dependence instead of enthusiasm. If nothing gets worse, you're carrying exposure for no return and the integration should come out. If something critical breaks, you've just discovered a production dependency on a commitment held by someone else.

**Who checks the output, and how long does that take?** Verification cost is the line item missing from most AI business cases. If a human reviews every result, the hours saved may round to zero while the exposure stays at full price. Measure the review time before you approve the expansion.

**What are we granting, and can we take it back?** Credentials revoke. Data you've already handed over does not. That distinction decides whether the pilot runs read-only, whether it runs on synthetic data, and whether deletion terms go into the contract before signature.

**Is this a hard problem or a tedious one?** Both are legitimate uses carrying different risk. A tedious task with bounded input and a reviewable output is a clean trade. A hard problem handed to an autonomous agent holding production credentials is a different transaction, and the controls should reflect that.

None of that requires anyone to slow anything down on your behalf.

## Where This Lands

The pacing proposal is a real structural change, and independent oversight inside these labs deserves to succeed.

Sit with what prompted it, though. The people closest to these systems just told the public they've lost some visibility into how their own models behave under pressure. They said it about controlled environments, staffed by researchers, running deliberate evaluations. Your environment has none of that.

Notice the shape of it. A unilateral pledge got dropped in February because no coordination existed to make it worth keeping. In September, coordination is the ask.

Corporate structure. Scaling policy. Evaluation guardrails. Three unrelated commitments, each one standing between capability and deployment, each one renegotiated the moment holding it cost something.

The one commitment nobody can renegotiate for you is how much of your environment you hand over, and how quickly.

Slow that down.

---

### Sources

- [BBC: AI safety timeline](https://www.bbc.com/news/articles/c14dpgm0rg4o)
- [Congressional Research Service, IN12669](https://www.congress.gov/crs-product/IN12669)
- [TIME: Exclusive — Anthropic Drops Flagship Safety Pledge](https://time.com/7380854/exclusive-anthropic-drops-flagship-safety-pledge/)
- [OpenAI: Hugging Face Incident and the Road Ahead](https://openai.com/index/hugging-face-incident-and-the-road-ahead/)
- [Hugging Face: Agent Intrusion Technical Timeline](https://huggingface.co/blog/agent-intrusion-technical-timeline)
- [Dark Reading: Hundreds of OpenAI Agents Invaded Hugging Face Servers](https://www.darkreading.com/cyberattacks-data-breaches/hundreds-openai-agents-invaded-hugging-face-servers)
- [Ballard Spahr: AI Gone Rogue — What Recent OpenAI and Anthropic AI Incidents Could Mean for CFAA Liability](https://www.ballardspahr.com/insights/alerts-and-articles/2026/08/ai-gone-rogue-what-recent-openai-and-anthropic-ai-incidents-could-mean-for-cfaa-liability)

---

*Shanief Webb is a CISO with experience across the FBI, Google, Meta, Okta, and Dropbox. He writes about security leadership, AI governance, and building organizations that operate under pressure.*
