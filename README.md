🔍 ScanXr Recon Tool

<p align="center">
  <strong>Python Web Reconnaissance & Security Assessment Tool</strong>
</p><p align="center">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue?logo=python" alt="Python 3.8+">
  <img src="https://img.shields.io/badge/Platform-Cross--platform-lightgrey" alt="Cross-platform">
  <img src="https://img.shields.io/badge/Use-Authorized%20Testing-red" alt="Authorized testing only">
</p>ScanXr is a Python-based web reconnaissance and security assessment tool designed to collect information about a target website and identify potential security weaknesses.

It automates several reconnaissance tasks and provides a risk score along with a JSON report to help security researchers understand the target's attack surface.

«Disclaimer: ScanXr is intended for educational purposes and authorized security testing only. Only scan websites, applications, servers, or systems that you own or have explicit permission to test.»

---

✨ Features

🔎 Reconnaissance

ScanXr collects basic information about the target:

- Domain name
- Resolved IP address
- Website title
- SSL certificate issuer
- SSL certificate expiration
- Detected web technologies

⚙️ Technology Detection

The current version attempts to identify common technologies, including:

- React
- Vue
- Angular
- Laravel
- WordPress
- Nginx
- Apache

Technology detection is based on simple signatures and may produce false positives or miss technologies.

🛡️ HTTP Security Headers

ScanXr checks for the presence of important HTTP security headers:

- "Content-Security-Policy"
- "X-Frame-Options"
- "X-Content-Type-Options"
- "Strict-Transport-Security"
- "Referrer-Policy"

Missing headers are reported as potential security findings.

🍪 Cookie Analysis

Extracts cookies returned by the target and displays:

- Cookie name
- "Secure" flag
- "HttpOnly" flag

🔐 Authentication Surface Detection

Checks the HTML source for common authentication-related keywords:

- Login
- Logout
- Password reset

These results indicate possible authentication functionality and are not vulnerabilities by themselves.

📂 Common Path Enumeration

Checks a list of common paths that may expose useful information or resources:

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

An accessible path does not automatically mean that the path is vulnerable. Results must be manually reviewed.

📜 JavaScript Analysis

Extracts JavaScript files referenced by the target and looks for indicators such as:

- Possible API keys or secrets
- GraphQL references
- WebSocket endpoints
- Source map references
- API endpoint patterns

These checks are heuristic and may generate false positives.

🔄 Reflected Parameter Checks

Sends a harmless test value through a small list of common query parameters and checks whether the value appears in the response.

A reflected value does not automatically indicate an XSS vulnerability. Context-aware validation is required.

🔍 Basic IDOR Pattern Checks

Compares responses generated with several common object identifiers.

Example identifiers:

?id=1
?id=2
?id=3
?id=10
?id=9999

The tool reports response differences, status changes, and size anomalies.

A response variation is not proof of an IDOR vulnerability. Proper IDOR testing requires authenticated accounts, authorization checks, and manual verification.

📊 JSON Report Generation

After a scan, the results are exported to:

result.json

The report can contain:

- Target URL
- Domain
- IP address
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

📋 Requirements

- Python 3.8 or newer
- pip
- Internet connection
- Python dependency: "requests"

---

🚀 Installation

1. Clone the repository

git clone https://github.com/7h3m/ScanXr.git

2. Open the project directory

cd ScanXr

3. Install dependencies

pip install -r requirements.txt

If you prefer to install the main dependency manually:

pip install requests

---

⚡ Usage

Run the tool:

python main.py

The tool will ask for the access key:

=== AUTH REQUIRED ===
Enter access key:

Then enter a target URL:

TARGET URL:

ScanXr accepts URLs with or without the protocol.

Examples:

https://example.com
http://example.com
example.com

---

🖥️ Example Output

Example of a ScanXr results display:

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
  - session (Secure=True, HttpOnly=True)

======================================================================
                         DETAILED FINDINGS
======================================================================

[MEDIUM] Missing Security Headers

Target: https://example.com

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

======================================================================

The output above is only an example. Actual results depend on the target.

---

📈 Risk Score

ScanXr starts with a score of:

100/100

The score is reduced according to several detected indicators, including:

- Reflected parameters
- Accessible paths
- Security findings
- Cookies
- JavaScript files
- Potential IDOR response differences

Risk Classification

Score| Classification
80–100| 🟢 LOW RISK
50–79| 🟠 MEDIUM RISK
0–49| 🔴 HIGH RISK

«The risk score is an internal heuristic. It should not be considered a formal security rating or a substitute for a professional security assessment.»

---

📁 Project Structure

ScanXr/
│
├── main.py
├── README.md
├── requirements.txt
├── .gitignore
└── result.json

Recommended "requirements.txt"

requests>=2.31.0

Recommended ".gitignore"

__pycache__/
*.py[cod]

.venv/
venv/
env/

result.json
.env

---

⚠️ Limitations

ScanXr is a lightweight reconnaissance tool and is not a complete vulnerability scanner.

The tool may:

- Produce false positives
- Miss vulnerabilities
- Detect public resources that are intentionally accessible
- Report response differences that are expected application behavior
- Identify JavaScript keywords that are not real secrets
- Detect technologies incorrectly

All findings should be manually validated before being reported as security vulnerabilities.

---

🔒 Security & Responsible Use

Only use ScanXr against:

- Systems you own
- Local development environments
- Security labs
- Capture-the-Flag (CTF) environments
- Applications covered by a bug bounty scope
- Targets for which you have explicit authorization

Do not use this tool to scan third-party systems without permission.

The author is not responsible for misuse or unauthorized testing.

---

🗺️ Roadmap

Possible future improvements:

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

You can contribute by:

1. Forking the repository.
2. Creating a feature branch.
3. Making your changes.
4. Testing the project.
5. Opening a pull request.

Please keep contributions focused on authorized and defensive security use.

---

📄 License

Choose and add a license before publishing the repository as an open-source project.

The MIT License is one possible option for allowing reuse, modification, and distribution.

If you choose MIT, add a "LICENSE" file containing the appropriate license text and copyright information.

---

👨‍💻 Author

Caennais

GitHub: "@7h3m" (https://github.com/7h3m)

Project: "ScanXr Recon Tool" (https://github.com/7h3m/ScanXr)

---

<p align="center">
  <strong>ScanXr Recon Tool</strong><br>
  Python Web Reconnaissance & Security Assessment Tool
</p><p align="center">
  Made with ❤️ by <strong>Caennais</strong>
</p>
