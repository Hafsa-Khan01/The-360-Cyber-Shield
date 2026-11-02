# The 360° Cyber Shield — Technical Project Report

**Project category:** Offensive and Defensive Security (Purple Teaming)  
**Prepared by:** Hafsa Khan  
**Supervisor:** Tahir Mushtaq Rana  
**Department:** Cyber Security

## 1. Project overview

The 360° Cyber Shield is a lab-oriented integrated security project designed to connect human-risk assessment, web-application security testing, and centralized security monitoring. The intended workflow combines Gophish, Acunetix DAST, OWASP Juice Shop, and Wazuh SIEM/XDR.

The platform is evaluated as a controlled research environment, not as a claim of complete enterprise protection.

## 2. Objectives

- Assess selected security-awareness practices through a documented survey.
- Conduct authorized phishing-awareness simulations with Gophish.
- Scan an isolated OWASP Juice Shop target using Acunetix DAST.
- Collect selected endpoint and application telemetry with Wazuh agents.
- Validate Wazuh decoders and rules against known test events.
- Map justified test behaviors to MITRE ATT&CK.
- Document integration limitations, resource constraints, and future improvements.

## 3. Technical stack

| Component | Intended role |
|---|---|
| Kali Linux | Security testing workstation, where used |
| Gophish | Authorized phishing-awareness campaign management |
| Acunetix | Dynamic web-application security testing |
| OWASP Juice Shop | Isolated deliberately vulnerable target |
| Wazuh Agent | Endpoint and application log collection |
| Wazuh Manager / Indexer / Dashboard | Central analysis, indexing, and visualization |
| Cloudflare Tunnel | Connectivity component, only where configured and documented |
| Google Forms / spreadsheet export | Survey collection and aggregate analysis |
| MATLAB | Offline telemetry signal analysis |

Record exact product versions and deployment topology in the evidence register.

## 4. Architecture and workflow

1. Define the authorized lab scope and isolate the target.
2. Collect awareness survey responses under an approved privacy process.
3. Configure a Gophish campaign using a controlled training landing page; do not collect real passwords.
4. Run Acunetix only against the approved Juice Shop target.
5. Configure Wazuh agent log collection for the relevant host and application sources.
6. Generate known test events and verify collection, parsing, rule matching, indexing, and dashboard visibility.
7. Record gaps and repeat tests after defensive changes.

## 5. Survey observations supplied in project notes

The source notes report N=50 and the following percentages: phishing-link interaction 24%; password reuse 20%; unsecured public Wi-Fi 46%; update postponement 48%; untrusted USB willingness 20%; and no MFA 14%.

These are provisional transcription values. Recalculate from the original export, record each question's valid-response denominator, and retain anonymized aggregate evidence. Do not infer actual compromise from self-reported responses.

## 6. Technical findings requiring evidence

### 6.1 Acunetix

The source notes describe SQL injection and XSS findings. Attach the sanitized scanner report, finding IDs, severity, affected component, evidence, and manual validation status before describing them as confirmed.

### 6.2 Wazuh decoders and rules

The supplied descriptions are inconsistent: one reports successful custom decoder alerts, while another reports XML parsing errors in local_rules.xml and incomplete deployment. Use wazuh-logtest and service logs to establish the actual state. Record each rule ID and a sanitized sample event.

### 6.3 Indexer memory pressure

The notes report Linux OOM termination and a 5.3 GB JVM heap adjustment. This is an environment-specific reported setting, not a universal tuning recommendation. Record total RAM, swap, heap minimum/maximum, indexer configuration, kernel OOM log, service restart history, and measurements before and after the change.

### 6.4 MATLAB analysis

Forward-backward zero-phase filtering can be used for offline trend analysis. It does not establish real-time SIEM processing. Document the data source, sampling interval, filter design, parameters, and reproducible script.

## 7. Limitations

- Hardware capacity may constrain simultaneous indexer and scanning workloads.
- Network tunneling may add latency or connectivity dependencies.
- Custom XML parsing errors can prevent rule loading.
- Survey and campaign datasets measure different things and must remain separate.
- A lab deployment does not establish production readiness.

## 8. Future enhancements

- Automated regression tests for Wazuh decoders and rules.
- Ingestion latency, event-loss, and indexer resource benchmarks.
- Repeatable DAST scans with evidence-based finding triage.
- Privacy-preserving awareness training based on campaign outcomes.
- Cloud-native telemetry coverage.
- SOAR case management integration, such as TheHive, after a separate implementation and validation phase.

## 9. Safety and ethics

All tests require explicit authorization and a controlled scope. Use synthetic accounts and data. Do not collect real credentials. Protect participant privacy and sanitize all public artifacts.
