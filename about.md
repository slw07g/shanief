---
layout: page
title: About Shanief
---

<div class="about-container">
  
  <section class="bio-section">
    <p class="lead-text">
      Bridging the gap between <strong>high-level security strategy</strong> and <strong>cloud infrastructure reality</strong>.
    </p>
    <p>
      I focus on the frameworks necessary to build resilient systems, foster cross-functional collaboration, and mentor the next generation of security engineers. From incident response to enterprise security architecture, my work creates the long-term vision of a secure digital future.
    </p>
    <p>
      Based in <strong>Atlanta, GA</strong>. Alum of <strong>Carnegie Mellon University</strong>.
    </p>
  </section>

  <hr class="glass-divider">

  <section class="certs-section">
    <h2>Certifications & Expertise</h2>
    <div class="certs-grid">
      <div class="cert-card">
        <span class="cert-title">OSCP</span>
        <span class="cert-desc">Offensive Security Certified Professional</span>
      </div>
      <div class="cert-card">
        <span class="cert-title">GXPN</span>
        <span class="cert-desc">GIAC Exploit Researcher & Adv. Penetration Tester</span>
      </div>
      <div class="cert-card">
        <span class="cert-title">GREM</span>
        <span class="cert-desc">GIAC Reverse Engineering Malware</span>
      </div>
      <div class="cert-card">
        <span class="cert-title">GCFA</span>
        <span class="cert-desc">GIAC Certified Forensic Analyst</span>
      </div>
      <div class="cert-card">
        <span class="cert-title">GNFA</span>
        <span class="cert-desc">GIAC Network Forensic Analyst</span>
      </div>
      <div class="cert-card">
        <span class="cert-title">GCIH</span>
        <span class="cert-desc">GIAC Certified Incident Handler</span>
      </div>
      <div class="cert-card">
        <span class="cert-title">GMOB</span>
        <span class="cert-desc">GIAC Mobile Device Security Analyst</span>
      </div>
      <div class="cert-card">
        <span class="cert-title">GPEN</span>
        <span class="cert-desc">GIAC Penetration Tester</span>
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
    font-size: 1.4rem;
    font-weight: 300;
    line-height: 1.6;
    color: var(--text-main);
    margin-bottom: 2rem;
  }
  
  .glass-divider {
    border: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(129, 140, 248, 0.3), transparent);
    margin: 4rem 0;
  }

  .certs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1.5rem;
    margin-top: 2rem;
  }

  .cert-card {
    background: rgba(255, 255, 255, 0.5);
    border: 1px solid rgba(255, 255, 255, 0.6);
    padding: 1.5rem;
    border-radius: 16px;
    text-align: center;
    transition: all 0.3s ease;
    cursor: default;
  }

  .cert-card:hover {
    transform: translateY(-5px);
    background: white;
    box-shadow: 0 10px 20px rgba(129, 140, 248, 0.15);
    border-color: var(--accent-primary);
  }

  .cert-title {
    display: block;
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 1.5rem;
    color: var(--accent-primary);
    margin-bottom: 0.5rem;
  }

  .cert-desc {
    font-size: 0.85rem;
    color: var(--text-muted);
    line-height: 1.4;
  }

  .social-links-large {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    margin-top: 2rem;
  }

  .social-btn-large {
    padding: 1rem 2rem;
    background: var(--sidebar-bg);
    color: white;
    border-radius: 12px;
    font-weight: 600;
    text-decoration: none;
    transition: transform 0.2s;
  }

  .social-btn-large:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(30, 27, 75, 0.3);
    color: white;
  }
</style>
