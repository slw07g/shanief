---
layout: page
title: About Shanief
---

<div class="about-container">
  
  <section class="bio-section">
    <p class="lead-text">
      I am a security practitioner who refuses to choose between <strong>offensive precision</strong> and <strong>defensive resilience</strong>.
    </p>
    
    <div class="bio-content">
      <p>
        Too often, the security industry is divided into silos: Red Teams who break things and Blue Teams who fix them. My career has been dedicated to shattering that barrier. With a deep background in <strong>Explotation, Malware Analysis, and Digital Forensics</strong>, I build security strategies that are grounded in the adversarial reality.
      </p>
      <p>
        My journey has taken me from the trenches of incident response to driving security engineering efforts at well-known government agencies and technology companies, including US Postal Service Office of Inspector General, Federal Bureau of Investigation, Google, Cox Communications, IBM, Slack, Drobox, and Okta. I don't just theorize about "secure by design" — I have reverse-engineered the threats that dismantle those designs. 
      </p>
      <p>
        Today, my focus is twofold: <strong>Technical Excellence</strong> and <strong>Human Capital</strong>. I construct high-assurance cloud infrastructures that can withstand modern attacks, and I mentor the next generation of engineers to do the same... because security is not just a technical problem - it is a discipline of continuous learning, strategy, and adaptation.
      </p>
    </div>
  </section>

  <hr class="glass-divider">

  <section class="certs-section">
    <h2>Arsenal & Qualifications</h2>
    <p class="section-subtitle">A multidisciplinary skillset validation across the security spectrum.</p>
    <div class="certs-grid">
      <div class="cert-card red-team">
        <span class="cert-type">OFFENSE</span>
        <span class="cert-title">GXPN</span>
        <span class="cert-desc">Exploit Researcher & Adv. Penetration Tester</span>
      </div>
      <div class="cert-card red-team">
        <span class="cert-type">OFFENSE</span>
        <span class="cert-title">OSCP</span>
        <span class="cert-desc">Offensive Security Certified Professional</span>
      </div>
      <div class="cert-card red-team">
        <span class="cert-type">OFFENSE</span>
        <span class="cert-title">GPEN</span>
        <span class="cert-desc">GIAC Penetration Tester</span>
      </div>
      <div class="cert-card red-team">
        <span class="cert-type">OFFENSE</span>
        <span class="cert-title">GMOB</span>
        <span class="cert-desc">Mobile Device Security Analyst</span>
      </div>
      
      <div class="cert-card blue-team">
        <span class="cert-type">DEFENSE</span>
        <span class="cert-title">GREM</span>
        <span class="cert-desc">Reverse Engineering Malware</span>
      </div>
      <div class="cert-card blue-team">
        <span class="cert-type">DEFENSE</span>
        <span class="cert-title">GCFA</span>
        <span class="cert-desc">Advanced Forensic Analyst</span>
      </div>
      <div class="cert-card blue-team">
        <span class="cert-type">DEFENSE</span>
        <span class="cert-title">GNFA</span>
        <span class="cert-desc">Network Forensic Analyst</span>
      </div>
      <div class="cert-card blue-team">
        <span class="cert-type">DEFENSE</span>
        <span class="cert-title">GCIH</span>
        <span class="cert-desc">Certified Incident Handler</span>
      </div>
    </div>
  </section>
  
  <section class="connect-section">
    <h2>Connect</h2>
    <div class="social-links-large">
      <a href="https://linkedin.com/in/shanief" class="social-btn-large">
        <span>LinkedIn</span>
      </a>
      <a href="https://github.com/slw07g" class="social-btn-large">
        <span>GitHub</span>
      </a>
      <a href="https://twitter.com/feinahs" class="social-btn-large">
        <span>Twitter</span>
      </a>
    </div>
  </section>

</div>

<style>
  .lead-text {
    font-size: 1.6rem;
    font-family: var(--font-display);
    font-weight: 600;
    line-height: 1.4;
    color: var(--text-main);
    margin-bottom: 2rem;
    background: linear-gradient(135deg, var(--text-main) 0%, var(--accent-primary) 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  
  .bio-content p {
    font-size: 1.15rem;
    line-height: 1.8;
    color: #475569;
    margin-bottom: 1.5rem;
  }
  
  .glass-divider {
    border: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(129, 140, 248, 0.3), transparent);
    margin: 4rem 0;
  }

  /* Certifications Grid */
  .certs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 2.5rem;
  }

  .cert-card {
    position: relative;
    background: rgba(255, 255, 255, 0.5);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.6);
    padding: 2rem;
    border-radius: 20px;
    transition: all 0.3s ease;
    overflow: hidden;
  }

  .cert-card:hover {
    transform: translateY(-5px);
    background: white;
    box-shadow: 0 15px 30px rgba(0,0,0,0.05);
  }
  
  /* Indicators for Red/Blue team */
  .cert-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 4px;
    height: 100%;
  }
  
  .cert-card.red-team::before { background: #f43f5e; } /* Red/Pink */
  .cert-card.blue-team::before { background: #3b82f6; } /* Blue */

  .cert-type {
    display: block;
    font-size: 0.7rem;
    font-weight: 800;
    letter-spacing: 2px;
    margin-bottom: 0.5rem;
  }
  
  .red-team .cert-type { color: #f43f5e; }
  .blue-team .cert-type { color: #3b82f6; }

  .cert-title {
    display: block;
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 1.8rem;
    color: var(--text-main);
    margin-bottom: 0.25rem;
  }

  .cert-desc {
    font-size: 0.95rem;
    color: var(--text-muted);
  }
  
  .section-subtitle {
    font-size: 1.1rem;
    color: var(--text-muted);
    margin-bottom: 1rem;
  }

  /* Social Buttons */
  .social-links-large {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    margin-top: 2rem;
  }

  .social-btn-large {
    padding: 1rem 2.5rem;
    background: var(--sidebar-bg);
    color: white;
    border-radius: 12px;
    font-weight: 600;
    text-decoration: none;
    transition: all 0.3s ease;
    border: 1px solid transparent;
  }

  .social-btn-large:hover {
    transform: translateY(-2px);
    background: white;
    color: var(--sidebar-bg);
    border-color: var(--sidebar-bg);
    box-shadow: 0 5px 15px rgba(30, 27, 75, 0.1);
  }
</style>
