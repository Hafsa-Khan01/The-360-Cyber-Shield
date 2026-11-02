# The 360° Cyber Shield

**An Empirical Purple Teaming Framework Integrating Automated DAST, Tactical Phishing Simulations, and Real-Time SIEM Orchestration**

**Researcher:** Hafsa Khan  
**Supervisor:** Tahir Mushtaq Rana  
**Department:** Cyber Security

## Overview

The 360° Cyber Shield is a controlled, lab-oriented Purple Teaming project connecting three domains:

- **People:** security-awareness measurement and authorized phishing simulations using Gophish.
- **Process:** Dynamic Application Security Testing (DAST) using Acunetix against an isolated OWASP Juice Shop target.
- **Technology:** endpoint and application telemetry collection, analysis, and alerting through Wazuh SIEM/XDR.

The central idea is a repeatable feedback loop: conduct an authorized simulation, identify the expected telemetry, verify collection and detection, then improve the defensive configuration.

## Architecture

| Domain | Components | Role |
|---|---|---|
| People | Awareness survey, Gophish | Measure reported practices and controlled campaign interactions |
| Process | Acunetix, OWASP Juice Shop | Assess an isolated web application |
| Technology | Wazuh Agent, Manager, Indexer, Dashboard | Collect, analyze, and visualize security events |
| Threat context | MITRE ATT&CK | Describe relevant adversary behaviors |
| Offline analysis | MATLAB Signal Processing | Explore offline telemetry trends |

## Repository structure

- Research/ — research-paper draft
- Documentation/ — technical report, architecture, validation register
- Survey/ — survey methodology and reporting guidance
- SIEM/ — Wazuh pipeline and rule-validation notes
- Evidence/ — location for sanitized supporting evidence

## Research integrity and current status

The project notes supplied for this repository contain several results that still require source evidence. This repository deliberately distinguishes reported observations from independently verified findings.

- Survey percentages must be recalculated from the original response export, with a denominator for each question.
- Gophish delivery, click, and training-page submission metrics must be reported separately.
- SQL injection and XSS claims require the original Acunetix findings and validation evidence.
- The supplied descriptions conflict on whether custom Wazuh XML rules successfully generated alerts or remained blocked by parsing errors. The final report must describe the exact stage achieved.
- A reported 5.3 GB JVM heap setting is not proof by itself that indexer OOM events were resolved. Record host RAM, swap, heap settings, logs, and before/after measurements.
- MATLAB forward-backward zero-phase filtering is an offline analysis method; it should not be represented as real-time SIEM filtering without a separately evaluated streaming design.

See Documentation/Validation-and-Evidence-Register.md before making publication claims.

## Safety and authorization

Use only isolated lab targets and explicitly authorized participants and systems. Do not collect real passwords. Do not scan, phish, exploit, or monitor systems without permission. Sanitize screenshots, logs, reports, and exports. Never commit API keys, SMTP credentials, passwords, private keys, session cookies, participant identities, or sensitive target data.

## References

- Wazuh: https://documentation.wazuh.com/
- Gophish: https://getgophish.com/documentation/
- OWASP Juice Shop: https://owasp.org/www-project-juice-shop/
- OWASP Top 10: https://owasp.org/www-project-top-ten/
- MITRE ATT&CK: https://attack.mitre.org/
- NIST Cybersecurity Framework: https://www.nist.gov/cyberframework
- MathWorks filtfilt: https://www.mathworks.com/help/signal/ref/filtfilt.html

*Academic research and lab project. Product names are used for identification; their respective owners retain all rights.*
