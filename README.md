🛡️ ScanXr Recon Tool

<p align="center">
  <strong>Python Web Reconnaissance & Security Assessment Tool</strong>
</p><p align="center">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Version-4.0-purple?style=for-the-badge" alt="Version">
  <img src="https://img.shields.io/badge/Platform-Windows%20%7C%20Linux-lightgrey?style=for-the-badge" alt="Platform">
  <img src="https://img.shields.io/badge/Purpose-Security%20Research-red?style=for-the-badge" alt="Purpose">
</p>---

📌 Overview

ScanXr Recon Tool is a Python-based web reconnaissance and security assessment tool developed by Caennais.

Designed for authorized security testing, ScanXr automates basic reconnaissance tasks and identifies potential security weaknesses in web applications.

The tool combines multiple reconnaissance techniques into a single lightweight Python script.

⚡ Key Capabilities

- 🌐 Target IP resolution
- 🔒 SSL certificate inspection
- 🧩 Technology detection
- 🛡️ HTTP security header analysis
- 🍪 Cookie inspection
- 🔑 Authentication surface discovery
- 📜 JavaScript extraction and analysis
- 📂 Common path enumeration
- 🔍 Reflected parameter checks
- 🔐 Basic IDOR response comparison
- 📊 Risk score calculation
- 📁 JSON report generation

«⚠️ Disclaimer: ScanXr is intended exclusively for educational purposes and authorized security assessments. Only test systems you own or have explicit permission to assess.»

---

🚀 Features

🌐 1. Reconnaissance

Collects basic information about the target:

- Domain name
- Resolved IP address
- Website title
- SSL certificate issuer
- SSL certificate expiration
- Detected web technologies

🧩 2. Technology Detection

Attempts to identify common web technologies:

Technology| Detection
React| Frontend framework
Vue| Frontend framework
Angular| Frontend framework
Laravel| PHP framework
WordPress| CMS
Nginx| Web server
Apache| Web server

Detection relies on basic signatures and may produce false positives.

🛡️ 3. Security Header Analysis

Checks for the presence of important HTTP security headers:

- "Content-Security-Policy"
- "X-Frame-Options"
- "X-Content-Type-Options"
- "Strict-Transport-Security"
- "Referrer-Policy"

Missing headers are reported as potential security weaknesses.

🍪 4. Cookie Analysis

Extracts cookies returned by the target and displays:

- Cookie name
- Secure flag
- HttpOnly flag

🔑 5. Authentication Surface Detection

Identifies common authentication-related keywords:

- Login
- Logout
- Password reset

These indicators help identify authentication functionality but do not automatically represent vulnerabilities.

📂 6. Common Path Enumeration

Checks a predefined list of common website paths:

/robots.txt
/sitemap.xml
/.env
/.git/HEAD
/admin
/login
/api
/graphql
/swagger.json
/backup
/debug
/.DS_Store

Accessible paths must be manually reviewed before being considered security issues.

📜 7. JavaScript Analysis

Extracts JavaScript files and searches for indicators such as:

- Possible API keys or secrets
- GraphQL references
- WebSocket endpoints
- Source map references
- API endpoint patterns

🔍 8. Reflected Parameter Checks

Tests common query parameters using a harmless test value.

Examples:

?id=TESTX
?user=TESTX
?page=TESTX
?search=TESTX
?redirect=TESTX

A reflected value is not proof of an XSS vulnerability.

🔐 9. Basic IDOR Pattern Checks

Compares HTTP responses using several object identifiers.

Example:

?id=1
?id=2
?id=3
?id=10
?id=9999

The tool identifies response variations and anomalies that may require manual investigation.

«A response difference does not prove an IDOR vulnerability. Proper authorization testing and manual verification are required.»

📊 10. JSON Reporting

Scan results are automatically exported to:

result.json

The report can contain:

- Target URL
- Domain and IP
- Cookies
- JavaScript files
- Discovered paths
- Reflected parameters
- Potential IDOR indicators
- Detected technologies
- SSL information
- Security findings
- Risk score

---

⚙️ Requirements

Before installing ScanXr, make sure you have:

- Python 3.8 or newer
- pip
- Internet connection
- The "requests" Python package

---

📥 Installation

1. Clone the repository

git clone https://github.com/Caennais/ScanXr-Recon.git

2. Enter the project directory

cd ScanXr-Recon

3. Install dependencies

pip install -r requirements.txt

Or install Requests directly:

pip install requests

---

▶️ Usage

Start the tool:

python scanxr.py

The program will request an access key:

=== AUTH REQUIRED ===
Enter access key:

After authentication, enter the target URL:

TARGET URL: https://example.com

Supported formats:

https://example.com
http://example.com
example.com

Only use authorized targets.

---

🖥️ Example Output

======================================================================
CAENNAIS SCAN RESULTS
======================================================================

Domain: example.com
IP: 93.184.216.34
Risk Score: 82/100
Classification: LOW RISK

Technologies:
 - Nginx

Cookies:
 - session (Secure=True HttpOnly=True)

======================================================================
DETAILED FINDINGS
======================================================================

[MEDIUM] Missing Security Headers

Target:
https://example.com

Details:
CSP missing

Description:
Important HTTP security headers are missing.

Impact:
Can increase exposure to XSS, clickjacking, or MIME attacks.

CWE:
CWE-693

Recommendation:
Add recommended HTTP security headers.

The output above is illustrative. Actual results depend on the target.

---

📈 Risk Scoring

ScanXr starts with an initial score of:

100/100

The score is reduced according to detected indicators:

- Reflected parameters
- Accessible paths
- Security findings
- Cookies
- JavaScript files
- Potential IDOR response differences

Risk Classification

Score| Classification
🟢 80–100| LOW RISK
🟠 50–79| MEDIUM RISK
🔴 0–49| HIGH RISK

«The risk score is a basic internal heuristic, not a formal security rating or proof that a website is secure.»

---

📁 Project Structure

ScanXr-Recon/
│
├── scanxr.py
├── README.md
├── requirements.txt
├── .gitignore
└── result.json

requirements.txt

requests>=2.31.0

.gitignore

__pycache__/
*.py[cod]
.venv/
venv/
env/
result.json
.env

---

⚠️ Limitations

ScanXr is a lightweight reconnaissance tool, not a complete vulnerability scanner.

Potential limitations include:

- False-positive findings
- Missed vulnerabilities
- Incorrect technology detection
- Expected application responses being flagged as anomalies
- Public resources being incorrectly interpreted as security weaknesses
- JavaScript keywords being mistaken for actual secrets

All findings must be manually validated before being reported as vulnerabilities.

---

🔒 Security & Responsible Use

ScanXr must only be used against:

- Systems you own
- Local development environments
- Security laboratories
- Capture The Flag (CTF) environments
- Bug bounty targets within their authorized scope
- Systems for which you have explicit permission

Unauthorized testing of third-party systems is not permitted.

The author is not responsible for misuse or unauthorized security testing.

---

🗺️ Roadmap

Potential future improvements:

- [ ] Command-line arguments
- [ ] Custom wordlists
- [ ] Configurable request timeout
- [ ] Configurable request rate
- [ ] HTML report generation
- [ ] CSV report export
- [ ] Improved technology fingerprints
- [ ] Better cookie security checks
- [ ] Redirect analysis
- [ ] HTTP method analysis
- [ ] Improved JavaScript endpoint extraction
- [ ] More accurate risk scoring
- [ ] Unit tests
- [ ] Docker support

---

🤝 Contributing

Contributions are welcome!

To contribute:

1. Fork the repository.
2. Create a feature branch.
3. Implement your changes.
4. Test your modifications.
5. Open a Pull Request.

Please keep all contributions focused on defensive security and authorized testing.

---

📜 License

This project is intended to use the MIT License.

Before publishing, add a "LICENSE" file containing the official MIT License text and your preferred copyright attribution.

MIT License

Copyright (c) 2026 Caennais

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files, to deal in the Software
without restriction, including without limitation the rights to use, copy,
modify, merge, publish, distribute, sublicense, and/or sell copies.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.

---

👨‍💻 Author

<p align="center">
  <strong>Caennais</strong>
  <br>
  Developer of ScanXr Recon Tool
</p><p align="center">
  <strong>ScanXr Recon Tool v4.0</strong>
  <br>
  Python Web Reconnaissance & Security Assessment
</p><p align="center">
  ⭐ If you find this project useful, consider giving it a star on GitHub!
</p>---

<p align="center">
  <sub>Developed by Caennais · 2026</sub>
</p>
