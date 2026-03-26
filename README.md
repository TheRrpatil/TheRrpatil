<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VAPT Roadmap</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Bebas+Neue&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #080c10;
    --surface: #0d1117;
    --border: #1a2332;
    --accent: #00ff88;
    --accent2: #00b4ff;
    --accent3: #ff4d6a;
    --accent4: #ffb700;
    --text: #c9d1d9;
    --muted: #4a5568;
    --glow: rgba(0,255,136,0.15);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
    position: relative;
  }

  /* Scanline overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.03) 2px,
      rgba(0,0,0,0.03) 4px
    );
    pointer-events: none;
    z-index: 100;
  }

  /* Grid background */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,255,136,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,136,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
  }

  .container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 60px 24px 100px;
    position: relative;
    z-index: 1;
  }

  /* Header */
  header {
    text-align: center;
    margin-bottom: 70px;
    animation: fadeDown 0.8s ease both;
  }

  .badge {
    display: inline-block;
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    letter-spacing: 3px;
    color: var(--accent);
    border: 1px solid var(--accent);
    padding: 5px 14px;
    margin-bottom: 18px;
    text-transform: uppercase;
    animation: pulse-border 2s ease-in-out infinite;
  }

  @keyframes pulse-border {
    0%, 100% { box-shadow: 0 0 0 0 rgba(0,255,136,0.3); }
    50% { box-shadow: 0 0 12px 2px rgba(0,255,136,0.2); }
  }

  h1 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(52px, 8vw, 96px);
    line-height: 0.95;
    letter-spacing: 4px;
    background: linear-gradient(135deg, #fff 0%, var(--accent) 50%, var(--accent2) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    text-shadow: none;
    margin-bottom: 16px;
  }

  .subtitle {
    font-size: 14px;
    color: var(--muted);
    font-family: 'Share Tech Mono', monospace;
    letter-spacing: 1px;
  }

  /* Phase layout */
  .phases {
    display: flex;
    flex-direction: column;
    gap: 0;
    position: relative;
  }

  /* Vertical connector line */
  .phases::before {
    content: '';
    position: absolute;
    left: 39px;
    top: 0;
    bottom: 0;
    width: 1px;
    background: linear-gradient(to bottom,
      transparent,
      var(--accent) 5%,
      var(--accent) 95%,
      transparent
    );
    opacity: 0.3;
  }

  .phase {
    display: grid;
    grid-template-columns: 80px 1fr;
    gap: 24px;
    position: relative;
    animation: fadeUp 0.6s ease both;
  }

  .phase:nth-child(1) { animation-delay: 0.1s; }
  .phase:nth-child(2) { animation-delay: 0.2s; }
  .phase:nth-child(3) { animation-delay: 0.3s; }
  .phase:nth-child(4) { animation-delay: 0.4s; }
  .phase:nth-child(5) { animation-delay: 0.5s; }
  .phase:nth-child(6) { animation-delay: 0.6s; }
  .phase:nth-child(7) { animation-delay: 0.7s; }

  .phase-index {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 28px;
  }

  .phase-dot {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border: 2px solid;
    background: var(--bg);
    flex-shrink: 0;
    position: relative;
    z-index: 2;
    transition: transform 0.3s ease;
  }

  .phase:hover .phase-dot {
    transform: scale(1.4);
  }

  .phase-dot::after {
    content: '';
    position: absolute;
    inset: -4px;
    border-radius: 50%;
    opacity: 0;
    transition: opacity 0.3s;
  }

  .phase:hover .phase-dot::after {
    opacity: 1;
  }

  .phase-line {
    flex: 1;
    width: 1px;
    min-height: 24px;
    margin-top: 6px;
    opacity: 0;
  }

  .phase-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 28px 30px;
    margin-bottom: 24px;
    position: relative;
    transition: border-color 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease;
    overflow: hidden;
  }

  .phase-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 3px;
    height: 100%;
    border-radius: 4px 0 0 4px;
  }

  .phase:hover .phase-card {
    transform: translateX(4px);
  }

  /* Color themes per phase */
  .phase-1 .phase-dot { border-color: #00ff88; }
  .phase-1 .phase-dot::after { box-shadow: 0 0 12px #00ff88; background: rgba(0,255,136,0.1); }
  .phase-1 .phase-card { --c: #00ff88; }
  .phase-1 .phase-card::before { background: #00ff88; }
  .phase-1 .phase-card:hover { border-color: rgba(0,255,136,0.4); box-shadow: 0 0 30px rgba(0,255,136,0.07); }

  .phase-2 .phase-dot { border-color: #00b4ff; }
  .phase-2 .phase-dot::after { box-shadow: 0 0 12px #00b4ff; background: rgba(0,180,255,0.1); }
  .phase-2 .phase-card { --c: #00b4ff; }
  .phase-2 .phase-card::before { background: #00b4ff; }
  .phase-2 .phase-card:hover { border-color: rgba(0,180,255,0.4); box-shadow: 0 0 30px rgba(0,180,255,0.07); }

  .phase-3 .phase-dot { border-color: #a78bfa; }
  .phase-3 .phase-dot::after { box-shadow: 0 0 12px #a78bfa; background: rgba(167,139,250,0.1); }
  .phase-3 .phase-card { --c: #a78bfa; }
  .phase-3 .phase-card::before { background: #a78bfa; }
  .phase-3 .phase-card:hover { border-color: rgba(167,139,250,0.4); box-shadow: 0 0 30px rgba(167,139,250,0.07); }

  .phase-4 .phase-dot { border-color: #ff4d6a; }
  .phase-4 .phase-dot::after { box-shadow: 0 0 12px #ff4d6a; background: rgba(255,77,106,0.1); }
  .phase-4 .phase-card { --c: #ff4d6a; }
  .phase-4 .phase-card::before { background: #ff4d6a; }
  .phase-4 .phase-card:hover { border-color: rgba(255,77,106,0.4); box-shadow: 0 0 30px rgba(255,77,106,0.07); }

  .phase-5 .phase-dot { border-color: #fb923c; }
  .phase-5 .phase-dot::after { box-shadow: 0 0 12px #fb923c; background: rgba(251,146,60,0.1); }
  .phase-5 .phase-card { --c: #fb923c; }
  .phase-5 .phase-card::before { background: #fb923c; }
  .phase-5 .phase-card:hover { border-color: rgba(251,146,60,0.4); box-shadow: 0 0 30px rgba(251,146,60,0.07); }

  .phase-6 .phase-dot { border-color: #f9e556; }
  .phase-6 .phase-dot::after { box-shadow: 0 0 12px #f9e556; background: rgba(249,229,86,0.1); }
  .phase-6 .phase-card { --c: #f9e556; }
  .phase-6 .phase-card::before { background: #f9e556; }
  .phase-6 .phase-card:hover { border-color: rgba(249,229,86,0.4); box-shadow: 0 0 30px rgba(249,229,86,0.07); }

  .phase-7 .phase-dot { border-color: #34d399; }
  .phase-7 .phase-dot::after { box-shadow: 0 0 12px #34d399; background: rgba(52,211,153,0.1); }
  .phase-7 .phase-card { --c: #34d399; }
  .phase-7 .phase-card::before { background: #34d399; }
  .phase-7 .phase-card:hover { border-color: rgba(52,211,153,0.4); box-shadow: 0 0 30px rgba(52,211,153,0.07); }

  .phase-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 16px;
    flex-wrap: wrap;
    gap: 8px;
  }

  .phase-title-group {}

  .phase-num {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    color: var(--c, var(--accent));
    margin-bottom: 4px;
    opacity: 0.8;
  }

  .phase-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 28px;
    letter-spacing: 2px;
    color: #fff;
    line-height: 1;
  }

  .phase-tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    padding: 3px 10px;
    border-radius: 2px;
    letter-spacing: 1px;
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    color: var(--muted);
    white-space: nowrap;
    align-self: flex-start;
    margin-top: 4px;
  }

  .phase-desc {
    font-size: 13.5px;
    color: #7a8694;
    line-height: 1.6;
    margin-bottom: 18px;
    max-width: 600px;
  }

  .tasks {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .task {
    display: flex;
    align-items: center;
    gap: 7px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: var(--text);
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.07);
    padding: 5px 11px;
    border-radius: 2px;
    transition: background 0.2s, border-color 0.2s;
  }

  .task:hover {
    background: rgba(255,255,255,0.07);
    border-color: rgba(255,255,255,0.15);
  }

  .task-dot {
    width: 5px;
    height: 5px;
    border-radius: 50%;
    background: var(--c, var(--accent));
    flex-shrink: 0;
  }

  /* Tools section inside card */
  .tools-row {
    margin-top: 16px;
    padding-top: 16px;
    border-top: 1px solid rgba(255,255,255,0.05);
    display: flex;
    align-items: center;
    gap: 10px;
    flex-wrap: wrap;
  }

  .tools-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 1px;
    flex-shrink: 0;
  }

  .tool-chip {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    color: var(--c, var(--accent));
    padding: 2px 8px;
    border: 1px solid;
    border-color: currentColor;
    border-radius: 2px;
    opacity: 0.7;
    transition: opacity 0.2s;
  }

  .tool-chip:hover { opacity: 1; }

  /* Footer stats */
  .stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 16px;
    margin-top: 56px;
    padding-top: 40px;
    border-top: 1px solid var(--border);
    animation: fadeUp 0.7s ease 0.8s both;
  }

  .stat {
    text-align: center;
    padding: 20px;
    border: 1px solid var(--border);
    background: var(--surface);
    border-radius: 4px;
  }

  .stat-val {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 42px;
    letter-spacing: 2px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
  }

  .stat-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--muted);
    margin-top: 4px;
  }

  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @media (max-width: 600px) {
    .phases::before { left: 29px; }
    .phase { grid-template-columns: 60px 1fr; gap: 16px; }
    .phase-card { padding: 20px; }
    .phase-title { font-size: 22px; }
  }
</style>
</head>
<body>
<div class="container">

  <header>
    <div class="badge">// Security Assessment Framework</div>
    <h1>VAPT ROADMAP</h1>
    <p class="subtitle">VULNERABILITY ASSESSMENT &amp; PENETRATION TESTING — END-TO-END LIFECYCLE</p>
  </header>

  <div class="phases">

    <!-- Phase 1 -->
    <div class="phase phase-1">
      <div class="phase-index">
        <div class="phase-dot"></div>
        <div class="phase-line"></div>
      </div>
      <div class="phase-card">
        <div class="phase-header">
          <div class="phase-title-group">
            <div class="phase-num">PHASE 01</div>
            <div class="phase-title">Pre-Engagement</div>
          </div>
          <span class="phase-tag">PLANNING</span>
        </div>
        <p class="phase-desc">Define the scope, objectives, and rules of engagement. Establish legal agreements and set testing boundaries before any technical work begins.</p>
        <div class="tasks">
          <div class="task"><span class="task-dot"></span>Scope Definition</div>
          <div class="task"><span class="task-dot"></span>NDA & Authorization</div>
          <div class="task"><span class="task-dot"></span>Rules of Engagement</div>
          <div class="task"><span class="task-dot"></span>Statement of Work</div>
          <div class="task"><span class="task-dot"></span>Risk Acceptance</div>
          <div class="task"><span class="task-dot"></span>Communication Plan</div>
        </div>
      </div>
    </div>

    <!-- Phase 2 -->
    <div class="phase phase-2">
      <div class="phase-index">
        <div class="phase-dot"></div>
        <div class="phase-line"></div>
      </div>
      <div class="phase-card">
        <div class="phase-header">
          <div class="phase-title-group">
            <div class="phase-num">PHASE 02</div>
            <div class="phase-title">Reconnaissance</div>
          </div>
          <span class="phase-tag">INTEL GATHERING</span>
        </div>
        <p class="phase-desc">Collect intelligence about the target using passive and active methods. Map the attack surface — domains, IPs, employees, technologies, and exposed services.</p>
        <div class="tasks">
          <div class="task"><span class="task-dot"></span>OSINT Collection</div>
          <div class="task"><span class="task-dot"></span>DNS Enumeration</div>
          <div class="task"><span class="task-dot"></span>WHOIS / ASN Lookup</div>
          <div class="task"><span class="task-dot"></span>Subdomain Discovery</div>
          <div class="task"><span class="task-dot"></span>Email Harvesting</div>
          <div class="task"><span class="task-dot"></span>Social Engineering Recon</div>
          <div class="task"><span class="task-dot"></span>Technology Fingerprinting</div>
        </div>
        <div class="tools-row">
          <span class="tools-label">TOOLS:</span>
          <span class="tool-chip">Shodan</span>
          <span class="tool-chip">theHarvester</span>
          <span class="tool-chip">Maltego</span>
          <span class="tool-chip">Recon-ng</span>
          <span class="tool-chip">Amass</span>
        </div>
      </div>
    </div>

    <!-- Phase 3 -->
    <div class="phase phase-3">
      <div class="phase-index">
        <div class="phase-dot"></div>
        <div class="phase-line"></div>
      </div>
      <div class="phase-card">
        <div class="phase-header">
          <div class="phase-title-group">
            <div class="phase-num">PHASE 03</div>
            <div class="phase-title">Scanning & Enumeration</div>
          </div>
          <span class="phase-tag">ACTIVE RECON</span>
        </div>
        <p class="phase-desc">Actively probe the target to identify live hosts, open ports, running services, and OS details. Enumerate users, shares, and application entry points.</p>
        <div class="tasks">
          <div class="task"><span class="task-dot"></span>Network Port Scanning</div>
          <div class="task"><span class="task-dot"></span>Service Version Detection</div>
          <div class="task"><span class="task-dot"></span>OS Fingerprinting</div>
          <div class="task"><span class="task-dot"></span>Web App Enumeration</div>
          <div class="task"><span class="task-dot"></span>Directory Bruteforce</div>
          <div class="task"><span class="task-dot"></span>SMB / LDAP Enumeration</div>
          <div class="task"><span class="task-dot"></span>SSL/TLS Analysis</div>
        </div>
        <div class="tools-row">
          <span class="tools-label">TOOLS:</span>
          <span class="tool-chip">Nmap</span>
          <span class="tool-chip">Masscan</span>
          <span class="tool-chip">Gobuster</span>
          <span class="tool-chip">Nikto</span>
          <span class="tool-chip">Enum4linux</span>
        </div>
      </div>
    </div>

    <!-- Phase 4 -->
    <div class="phase phase-4">
      <div class="phase-index">
        <div class="phase-dot"></div>
        <div class="phase-line"></div>
      </div>
      <div class="phase-card">
        <div class="phase-header">
          <div class="phase-title-group">
            <div class="phase-num">PHASE 04</div>
            <div class="phase-title">Vulnerability Assessment</div>
          </div>
          <span class="phase-tag">ANALYSIS</span>
        </div>
        <p class="phase-desc">Identify and classify vulnerabilities in the target environment using automated scanners and manual techniques. Prioritize findings by severity and exploitability.</p>
        <div class="tasks">
          <div class="task"><span class="task-dot"></span>Automated Vuln Scanning</div>
          <div class="task"><span class="task-dot"></span>CVE / NVD Correlation</div>
          <div class="task"><span class="task-dot"></span>OWASP Top 10 Testing</div>
          <div class="task"><span class="task-dot"></span>Misconfig Detection</div>
          <div class="task"><span class="task-dot"></span>Credential Weakness Audit</div>
          <div class="task"><span class="task-dot"></span>CVSS Scoring</div>
          <div class="task"><span class="task-dot"></span>False Positive Triage</div>
        </div>
        <div class="tools-row">
          <span class="tools-label">TOOLS:</span>
          <span class="tool-chip">Nessus</span>
          <span class="tool-chip">OpenVAS</span>
          <span class="tool-chip">Burp Suite</span>
          <span class="tool-chip">Nuclei</span>
        </div>
      </div>
    </div>

    <!-- Phase 5 -->
    <div class="phase phase-5">
      <div class="phase-index">
        <div class="phase-dot"></div>
        <div class="phase-line"></div>
      </div>
      <div class="phase-card">
        <div class="phase-header">
          <div class="phase-title-group">
            <div class="phase-num">PHASE 05</div>
            <div class="phase-title">Exploitation</div>
          </div>
          <span class="phase-tag">ACTIVE TESTING</span>
        </div>
        <p class="phase-desc">Attempt to exploit confirmed vulnerabilities to demonstrate real-world impact. Gain initial access and simulate an adversary's attack chain within authorized scope.</p>
        <div class="tasks">
          <div class="task"><span class="task-dot"></span>Exploit Development/Selection</div>
          <div class="task"><span class="task-dot"></span>Initial Access Attacks</div>
          <div class="task"><span class="task-dot"></span>SQL Injection</div>
          <div class="task"><span class="task-dot"></span>XSS / CSRF / SSRF</div>
          <div class="task"><span class="task-dot"></span>Auth Bypass</div>
          <div class="task"><span class="task-dot"></span>Password Cracking</div>
          <div class="task"><span class="task-dot"></span>Phishing Simulation</div>
        </div>
        <div class="tools-row">
          <span class="tools-label">TOOLS:</span>
          <span class="tool-chip">Metasploit</span>
          <span class="tool-chip">SQLmap</span>
          <span class="tool-chip">Hydra</span>
          <span class="tool-chip">BeEF</span>
          <span class="tool-chip">ExploitDB</span>
        </div>
      </div>
    </div>

    <!-- Phase 6 -->
    <div class="phase phase-6">
      <div class="phase-index">
        <div class="phase-dot"></div>
        <div class="phase-line"></div>
      </div>
      <div class="phase-card">
        <div class="phase-header">
          <div class="phase-title-group">
            <div class="phase-num">PHASE 06</div>
            <div class="phase-title">Post-Exploitation</div>
          </div>
          <span class="phase-tag">DEEP DIVE</span>
        </div>
        <p class="phase-desc">After initial compromise, assess the true blast radius. Perform privilege escalation, lateral movement, data exfiltration tests, and persistence simulation.</p>
        <div class="tasks">
          <div class="task"><span class="task-dot"></span>Privilege Esca
