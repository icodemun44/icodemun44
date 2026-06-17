<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mun Khatiwada – Frontend Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg:       #0a0e1a;
    --surface:  #111827;
    --border:   #1e293b;
    --accent:   #38bdf8;
    --accent2:  #818cf8;
    --green:    #34d399;
    --text:     #e2e8f0;
    --muted:    #64748b;
    --card:     #131c2e;
  }

  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Grotesk', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── STAR FIELD ── */
  #stars {
    position: fixed; inset: 0; pointer-events: none; z-index: 0;
    overflow: hidden;
  }
  .star {
    position: absolute;
    border-radius: 50%;
    background: white;
    animation: twinkle var(--dur) ease-in-out infinite alternate;
    opacity: 0;
  }
  @keyframes twinkle { 0% { opacity: 0; transform: scale(0.8); } 100% { opacity: var(--op); transform: scale(1.2); } }

  /* ── LAYOUT ── */
  .wrap { position: relative; z-index: 1; max-width: 900px; margin: 0 auto; padding: 0 1.5rem 5rem; }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column; justify-content: center;
    padding-top: 3rem;
    position: relative;
  }

  .hero-eyebrow {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.78rem;
    color: var(--accent);
    letter-spacing: 0.18em;
    text-transform: uppercase;
    margin-bottom: 1.2rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.2s ease forwards;
  }

  .hero-name {
    font-size: clamp(2.6rem, 8vw, 5.5rem);
    font-weight: 700;
    line-height: 1.0;
    letter-spacing: -0.03em;
    margin-bottom: 1rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.4s ease forwards;
  }

  .hero-name span {
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-role {
    font-size: 1.15rem;
    color: var(--muted);
    font-weight: 400;
    margin-bottom: 1.8rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.6s ease forwards;
  }

  .hero-role em { color: var(--text); font-style: normal; font-weight: 500; }

  .hero-bio {
    max-width: 560px;
    line-height: 1.75;
    color: #94a3b8;
    font-size: 0.97rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.8s ease forwards;
    margin-bottom: 2.5rem;
  }

  .hero-links {
    display: flex; flex-wrap: wrap; gap: 0.75rem;
    opacity: 0;
    animation: fadeUp 0.7s 1s ease forwards;
  }

  .btn {
    display: inline-flex; align-items: center; gap: 0.45rem;
    padding: 0.6rem 1.2rem;
    border-radius: 6px;
    font-size: 0.85rem;
    font-weight: 500;
    text-decoration: none;
    cursor: pointer;
    border: none;
    transition: transform 0.18s, box-shadow 0.18s, background 0.18s;
  }
  .btn-primary {
    background: var(--accent);
    color: #0a0e1a;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(56,189,248,0.35); }

  .btn-ghost {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
  }
  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

  /* scroll indicator */
  .scroll-hint {
    position: absolute; bottom: 2.5rem; left: 0;
    display: flex; align-items: center; gap: 0.5rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    color: var(--muted);
    opacity: 0;
    animation: fadeIn 1s 1.8s ease forwards;
  }
  .scroll-arrow { animation: bounce 1.4s ease-in-out infinite; }
  @keyframes bounce { 0%,100%{transform:translateY(0)} 50%{transform:translateY(5px)} }

  /* ── SECTION ── */
  .section { margin-bottom: 5rem; }
  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    color: var(--accent);
    letter-spacing: 0.16em;
    text-transform: uppercase;
    margin-bottom: 2rem;
    display: flex; align-items: center; gap: 0.75rem;
  }
  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* ── SKILLS ── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 0.6rem;
  }

  .skill-chip {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 0.55rem 0.9rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.78rem;
    color: var(--text);
    text-align: center;
    transition: border-color 0.2s, color 0.2s, transform 0.2s, box-shadow 0.2s;
    cursor: default;
  }
  .skill-chip:hover {
    border-color: var(--accent2);
    color: var(--accent2);
    transform: translateY(-2px);
    box-shadow: 0 4px 16px rgba(129,140,248,0.15);
  }

  /* ── EXPERIENCE ── */
  .timeline { display: flex; flex-direction: column; gap: 0; }

  .job {
    position: relative;
    padding: 0 0 2.5rem 2rem;
    border-left: 1px solid var(--border);
  }
  .job:last-child { border-left-color: transparent; }
  .job::before {
    content: '';
    position: absolute;
    left: -5px; top: 6px;
    width: 9px; height: 9px;
    border-radius: 50%;
    background: var(--accent);
    box-shadow: 0 0 0 3px rgba(56,189,248,0.15);
  }

  .job-date {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    color: var(--muted);
    margin-bottom: 0.35rem;
  }

  .job-title {
    font-size: 1.05rem;
    font-weight: 600;
    margin-bottom: 0.15rem;
  }

  .job-company {
    font-size: 0.88rem;
    color: var(--accent);
    margin-bottom: 0.8rem;
    font-weight: 500;
  }

  .job-bullets {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 0.45rem;
  }

  .job-bullets li {
    font-size: 0.88rem;
    color: #94a3b8;
    line-height: 1.6;
    padding-left: 1rem;
    position: relative;
  }
  .job-bullets li::before {
    content: '▸';
    position: absolute; left: 0;
    color: var(--accent2);
    font-size: 0.72rem;
    top: 0.15rem;
  }

  /* ── PROJECTS ── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1rem;
  }

  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 1.5rem;
    transition: border-color 0.2s, transform 0.2s, box-shadow 0.2s;
    cursor: default;
    position: relative;
    overflow: hidden;
  }
  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.3s ease;
  }
  .project-card:hover {
    border-color: rgba(56,189,248,0.3);
    transform: translateY(-3px);
    box-shadow: 0 12px 32px rgba(0,0,0,0.35);
  }
  .project-card:hover::before { transform: scaleX(1); }

  .project-top {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 0.7rem;
  }

  .project-name {
    font-size: 0.97rem;
    font-weight: 600;
  }

  .project-live {
    display: inline-flex;
    align-items: center;
    gap: 0.3rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--green);
    border: 1px solid rgba(52,211,153,0.3);
    border-radius: 20px;
    padding: 0.2rem 0.55rem;
  }
  .project-live .dot {
    width: 5px; height: 5px;
    border-radius: 50%;
    background: var(--green);
    animation: pulse 1.5s ease-in-out infinite;
  }
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.3} }

  .project-desc {
    font-size: 0.84rem;
    color: #94a3b8;
    line-height: 1.6;
    margin-bottom: 1rem;
  }

  .project-tags {
    display: flex; flex-wrap: wrap; gap: 0.4rem;
  }
  .tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    color: var(--accent2);
    background: rgba(129,140,248,0.08);
    border: 1px solid rgba(129,140,248,0.2);
    border-radius: 4px;
    padding: 0.2rem 0.5rem;
  }

  /* ── EDUCATION ── */
  .edu-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 1.5rem 1.8rem;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .edu-degree {
    font-size: 1rem;
    font-weight: 600;
    margin-bottom: 0.3rem;
  }
  .edu-school {
    font-size: 0.88rem;
    color: var(--accent);
    margin-bottom: 0.2rem;
  }
  .edu-detail {
    font-size: 0.82rem;
    color: var(--muted);
  }
  .edu-gpa {
    display: flex; flex-direction: column; align-items: flex-end;
    gap: 0.2rem;
  }
  .gpa-value {
    font-family: 'JetBrains Mono', monospace;
    font-size: 1.8rem;
    font-weight: 700;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
  }
  .gpa-label {
    font-size: 0.7rem;
    color: var(--muted);
    font-family: 'JetBrains Mono', monospace;
  }

  /* ── CERTS ── */
  .certs-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 0.6rem;
  }
  .cert-item {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 0.55rem 1rem;
    font-size: 0.82rem;
    color: var(--text);
    display: flex; align-items: center; gap: 0.5rem;
  }
  .cert-item span { color: var(--accent); font-weight: 600; font-size: 0.9rem; }

  /* ── CONTACT BAR ── */
  .contact-bar {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 1.5rem 1.8rem;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    gap: 1.2rem;
  }
  .contact-heading {
    font-size: 1.15rem;
    font-weight: 600;
  }
  .contact-sub {
    font-size: 0.84rem;
    color: var(--muted);
    margin-top: 0.2rem;
  }
  .contact-links {
    display: flex; flex-wrap: wrap; gap: 0.6rem;
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
  }

  .reveal {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.55s ease, transform 0.55s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: none;
  }

  /* ── FOOTER ── */
  .footer {
    text-align: center;
    padding: 3rem 0 1rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    color: var(--muted);
  }
</style>
</head>
<body>

<!-- Stars -->
<div id="stars"></div>

<div class="wrap">

  <!-- HERO -->
  <section class="hero">
    <div class="hero-eyebrow">// hello world</div>
    <h1 class="hero-name">Mun<br><span>Khatiwada</span></h1>
    <p class="hero-role"><em>Frontend Developer</em> &nbsp;·&nbsp; MERN Stack &nbsp;·&nbsp; Next.js &nbsp;·&nbsp; AI/ML Enthusiast</p>
    <p class="hero-bio">
      Junior frontend developer based in Kathmandu, Nepal — building scalable, user-friendly web applications with a focus on clean design and real-world impact. Currently studying Computer Science with a major in Artificial Intelligence.
    </p>
    <div class="hero-links">
      <a class="btn btn-primary" href="mailto:munkhatiwada@gmail.com">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/></svg>
        Say Hello
      </a>
      <a class="btn btn-ghost" href="https://github.com" target="_blank" rel="noopener">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0 1 12 6.844a9.59 9.59 0 0 1 2.504.337c1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.02 10.02 0 0 0 22 12.017C22 6.484 17.522 2 12 2z"/></svg>
        GitHub
      </a>
      <a class="btn btn-ghost" href="https://linkedin.com" target="_blank" rel="noopener">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
        LinkedIn
      </a>
    </div>
    <div class="scroll-hint">
      <span>scroll to explore</span>
      <span class="scroll-arrow">↓</span>
    </div>
  </section>

  <!-- SKILLS -->
  <section class="section reveal">
    <div class="section-label">Skills & Tools</div>
    <div class="skills-grid" id="skillsGrid"></div>
  </section>

  <!-- EXPERIENCE -->
  <section class="section reveal">
    <div class="section-label">Experience</div>
    <div class="timeline">
      <div class="job">
        <div class="job-date">July 2025 – Sept 2025</div>
        <div class="job-title">Junior Frontend Developer</div>
        <div class="job-company">Great Bear Technology · Kathmandu, Nepal</div>
        <ul class="job-bullets">
          <li>Built and deployed Next.js projects with UI/UX integration — API-driven forms, dashboards, and landing pages.</li>
          <li>Integrated Odoo APIs for data synchronization in projects including BookingDex.</li>
          <li>Contributed to the Startup Resource Hub for high-net-worth investors in the U.S. and Nepal, collaborating directly with a Senior Designer from Fusemachines.</li>
        </ul>
      </div>
      <div class="job">
        <div class="job-date">July 2024 – July 2025</div>
        <div class="job-title">Internship Trainee – Web Development</div>
        <div class="job-company">Great Bear Technology · Kathmandu, Nepal</div>
        <ul class="job-bullets">
          <li>Designed, developed, and maintained web apps using JavaScript, Node.js, Express.js, and Tailwind CSS.</li>
          <li>Delivered responsive client-facing applications, ensuring scalability and performance.</li>
        </ul>
      </div>
      <div class="job">
        <div class="job-date">May 2025 – July 2025</div>
        <div class="job-title">Participant – Social Innovation Challenge</div>
        <div class="job-company">King's College & KUSOA · Kathmandu, Nepal</div>
        <ul class="job-bullets">
          <li>Collaborated with artisans and students to design sustainable business models rooted in culture.</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section class="section reveal">
    <div class="section-label">Projects</div>
    <div class="projects-grid">
      <div class="project-card">
        <div class="project-top">
          <div class="project-name">Startup Resource Hub</div>
          <div class="project-live"><span class="dot"></span>Live</div>
        </div>
        <p class="project-desc">Full-stack investment platform serving high-net-worth investors and startups across Nepal and the U.S. — built end-to-end with professional UI/UX.</p>
        <div class="project-tags">
          <span class="tag">Next.js</span>
          <span class="tag">Tailwind</span>
          <span class="tag">Supabase</span>
          <span class="tag">API Integration</span>
        </div>
      </div>
      <div class="project-card">
        <div class="project-top">
          <div class="project-name">IoT Smart Agriculture</div>
          <a class="project-live" href="https://github.com" target="_blank" rel="noopener" style="text-decoration:none; color:var(--accent); border-color:rgba(56,189,248,0.3);">↗ GitHub</a>
        </div>
        <p class="project-desc">Solar-powered sensing panel with automatic NPK fertilizer dispenser — designed for affordability and real-world farm deployment.</p>
        <div class="project-tags">
          <span class="tag">IoT</span>
          <span class="tag">Arduino</span>
          <span class="tag">C++</span>
          <span class="tag">Sensors</span>
        </div>
      </div>
    </div>
  </section>

  <!-- EDUCATION -->
  <section class="section reveal">
    <div class="section-label">Education</div>
    <div class="edu-card">
      <div>
        <div class="edu-degree">B.Sc. Computer Science — AI Major</div>
        <div class="edu-school">Westcliff University, King's College Nepal</div>
        <div class="edu-detail">2025 – Present</div>
      </div>
      <div class="edu-gpa">
        <div class="gpa-value">4.0</div>
        <div class="gpa-label">GPA</div>
      </div>
    </div>
  </section>

  <!-- CERTIFICATES -->
  <section class="section reveal">
    <div class="section-label">Achievements & Certificates</div>
    <div class="certs-grid">
      <div class="cert-item"><span>🥈</span> Oxford Inter-College Tech Fest 2023 – 1st Runner Up</div>
      <div class="cert-item"><span>🥈</span> Coding Kickstart 2.0 Python – 1st Runner Up</div>
      <div class="cert-item"><span>🥇</span> District Science & Tech Exhibition 2024 – 1st Position</div>
      <div class="cert-item"><span>📜</span> MERN Stack – Deerwalk Training Center</div>
    </div>
  </section>

  <!-- CONTACT -->
  <section class="section reveal">
    <div class="contact-bar">
      <div>
        <div class="contact-heading">Let's build something together</div>
        <div class="contact-sub">Open to opportunities · Kathmandu, Nepal</div>
      </div>
      <div class="contact-links">
        <a class="btn btn-primary" href="mailto:munkhatiwada@gmail.com">munkhatiwada@gmail.com</a>
        <a class="btn btn-ghost" href="tel:+9779862784500">+977 986 278 4500</a>
      </div>
    </div>
  </section>

  <div class="footer">Built with HTML · CSS · a bit of JS &nbsp;·&nbsp; Mun Khatiwada © 2025</div>

</div>

<script>
// ── STARS ──
(function() {
  const container = document.getElementById('stars');
  for (let i = 0; i < 120; i++) {
    const s = document.createElement('div');
    s.className = 'star';
    const size = Math.random() * 2 + 0.5;
    s.style.cssText = `
      width:${size}px; height:${size}px;
      left:${Math.random()*100}%;
      top:${Math.random()*100}%;
      --dur:${(Math.random()*3+2).toFixed(1)}s;
      --op:${(Math.random()*0.6+0.1).toFixed(2)};
      animation-delay:${(Math.random()*4).toFixed(1)}s;
    `;
    container.appendChild(s);
  }
})();

// ── SKILLS ──
const skills = [
  'JavaScript','TypeScript','Python','Node.js','Express.js',
  'Next.js','React','Tailwind CSS','SQL/MySQL','MongoDB',
  'Supabase','Postman','Git/GitHub','Figma','Arduino',
  'SAS','DSA','Quality Assurance'
];
const grid = document.getElementById('skillsGrid');
skills.forEach((s, i) => {
  const chip = document.createElement('div');
  chip.className = 'skill-chip';
  chip.textContent = s;
  chip.style.animationDelay = `${i * 40}ms`;
  grid.appendChild(chip);
});

// ── SCROLL REVEAL ──
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); } });
}, { threshold: 0.1 });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
</script>
</body>
</html>
