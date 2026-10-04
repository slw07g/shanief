---
layout: page
title: Learning
permalink: /learning/
redirect_from:
  - /learning/security-operations/
description: >-
  Free, practical security training written the way the work actually happens. Built for everyone, from people just getting curious about security to working practitioners and leaders.
---

<div class="learning-hub">

  <section class="bio-section">
    <p class="lead-text">
      Practical security knowledge, written the way the work actually happens.
    </p>

    <div class="bio-content">
      <p>
        Most security training teaches the textbook version. This is the version from the alert queue, the incident bridge, and the box that would not give up root. Each track is built around how the work is actually done: the decisions, the order you make them in, and the mistakes that cost the most time.
      </p>
      <p>
        Everything here is free, and every track stands on its own. Read it, then go apply it. That second step is where the learning happens.
      </p>
    </div>
  </section>

  <hr class="glass-divider">

  <section class="audience-section">
    <h2>Who It's For</h2>
    <p class="section-subtitle">Everyone. Security is a team sport, and every seat on the team needs a different part of the playbook.</p>

    <div class="audience-grid">
      <div class="audience-card">
        <span class="audience-title">New to security</span>
        <p>Students, career changers, and the curious. Each track starts from the fundamentals, so start at the beginning and work through in order.</p>
      </div>
      <div class="audience-card">
        <span class="audience-title">Security practitioners</span>
        <p>Analysts and engineers already in the field. Jump straight to the page you need and use the frameworks and walkthroughs as a reference.</p>
      </div>
      <div class="audience-card">
        <span class="audience-title">Engineers and IT</span>
        <p>The people who own the systems. Learn what a security team needs from you when an alert fires or an incident is declared, and why.</p>
      </div>
      <div class="audience-card">
        <span class="audience-title">Leaders and non-technical readers</span>
        <p>Managers, executives, and partners in legal, comms, and HR. Learn how the work is run, who makes which calls, and what good looks like.</p>
      </div>
    </div>
  </section>

  <hr class="glass-divider">

  <section class="tracks-section">
    <h2>Tracks</h2>
    <p class="section-subtitle">Each track stands on its own. If you are new to the field, take them in order. If you already have ground under you, jump straight to the one you need.</p>

    <div class="track-card defense">
      <span class="track-level">Defense</span>
      <a class="track-title" href="{{ '/learning/investigations-triage/' | relative_url }}">Investigations &amp; Triage</a>
      <p class="track-desc">How alerts get worked: from a claim that something bad happened to a decision backed by evidence.</p>
      <ul class="track-topics">
        <li>Playbooks and the questions to ask before you touch a single log</li>
        <li>Where the evidence lives and how to land on a disposition</li>
        <li>Walkthroughs: user-reported phishing, EDR malware detection, Okta suspicious activity</li>
      </ul>
      <a class="track-cta" href="{{ '/learning/investigations-triage/' | relative_url }}">Start the track &rarr;</a>
    </div>

    <div class="track-card defense">
      <span class="track-level">Defense</span>
      <a class="track-title" href="{{ '/learning/incident-response/' | relative_url }}">Security Incident Response</a>
      <p class="track-desc">What happens once triage confirms impact, and how to run it so the response holds up under pressure.</p>
      <ul class="track-topics">
        <li>Incident management vs incident response, and why they are different roles</li>
        <li>The lifecycle from declaration to lessons learned, and the incident command structure</li>
        <li>Executive summaries and postmortems, with templates</li>
      </ul>
      <a class="track-cta" href="{{ '/learning/incident-response/' | relative_url }}">Start the track &rarr;</a>
    </div>

    <div class="track-card offense">
      <span class="track-level">Offense</span>
      <a class="track-title" href="{{ '/learning/offensive-security/' | relative_url }}">Offensive Security</a>
      <p class="track-desc">The attacker's side of the same problem. Understanding it is what makes triage and incident response sharper.</p>
      <ul class="track-topics">
        <li>Attack methodology from reconnaissance to root</li>
        <li>Where to practice: HackTheBox and TryHackMe</li>
        <li>Going further: automating your attack chains and publishing writeups</li>
      </ul>
      <a class="track-cta" href="{{ '/learning/offensive-security/' | relative_url }}">Start the track &rarr;</a>
    </div>

    <p class="tracks-note"><strong>How to use this material:</strong> read the track, then apply it. Triage a real alert using the disposition framework. Run a postmortem on a real incident using the templates. Root a box and write up the methodology instead of just moving to the next one. What separates people is whether they used it. More tracks are on the way.</p>
  </section>

</div>
