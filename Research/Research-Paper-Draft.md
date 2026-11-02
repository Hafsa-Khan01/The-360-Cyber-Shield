# The 360° Cyber Shield: An Empirical Purple Teaming Framework Integrating Automated DAST, Tactical Phishing Simulations, and Real-Time SIEM Orchestration

**Hafsa Khan¹, Tahir Mushtaq Rana¹**  
¹Department of Cyber Security  
Emails: hf857707@gmail.com; tahirmushtaqrana@gmail.com

> **Draft status:** This manuscript is based on the project material supplied by the authors. Reported figures and technical outcomes have not been independently verified in this repository. Original survey exports, campaign reports, scanner evidence, Wazuh logs, and system measurements must be reviewed before submission.

## Abstract

Traditional enterprise security architectures often separate offensive validation from defensive monitoring. This separation can make it difficult to determine whether simulated attack activity is visible to monitoring infrastructure. This paper presents The 360° Cyber Shield, a lab-oriented Purple Teaming framework connecting controlled phishing-awareness exercises, dynamic web-application security testing, and centralized security telemetry. The workflow uses Gophish for authorized phishing simulations, Acunetix for Dynamic Application Security Testing (DAST) against an isolated OWASP Juice Shop instance, and Wazuh for endpoint and application log collection, analysis, and visualization. A human-awareness survey is included to establish a baseline of reported security practices. The project also documents integration challenges involving custom Wazuh decoders and rules, indexer memory pressure, and offline analysis of telemetry using zero-phase filtering. The supplied project notes report a survey sample of 50 participants and several risk percentages; these values require confirmation against the original response export and a documented calculation method. Claims about successful custom alert generation, vulnerability confirmation, and stabilization after a 5.3 GB JVM heap adjustment likewise require supporting evidence. The framework's contribution is a practical workflow for linking controlled offensive tests to defensive validation while recording the evidence and operational conditions needed to assess detection effectiveness.

**Index Terms—** Purple Teaming, Security Operations Center, Wazuh, Gophish, Acunetix, DAST, OWASP Juice Shop, security awareness, telemetry, MITRE ATT&CK.

## I. Introduction

Organizations depend on interconnected applications, endpoints, identities, and cloud services. Defensive controls such as endpoint monitoring, access control, firewalls, and vulnerability management are essential, but their effectiveness cannot be assessed solely by confirming that each tool is installed. Security teams also need to determine whether relevant activity is collected, interpreted, correlated, and surfaced in a form that supports investigation.

A common operational weakness is the separation of offensive testing from defensive monitoring. Vulnerability scans may produce findings that are not connected to monitoring priorities, while SIEM alerts may be configured without being tested against representative behaviors. Purple Teaming addresses this gap by coordinating controlled simulation with defensive detection engineering. Each authorized test is associated with a defensive question: what telemetry should be generated, where should it be collected, which detection logic should evaluate it, and what evidence demonstrates that the expected alert was produced?

This paper describes The 360° Cyber Shield, organized around People, Process, and Technology. The People domain measures security-awareness practices and supports approved phishing-awareness exercises. The Process domain assesses an isolated web application using DAST. The Technology domain collects host and application telemetry through Wazuh and provides a basis for detection validation.

## II. Problem Statement and Objectives

### A. Problem statement

Offensive assessments, awareness exercises, and defensive monitoring are frequently conducted as separate activities. This fragmentation makes it difficult to trace a simulated action from execution to the resulting endpoint or application event and then to a validated SIEM alert. A missing alert may result from absent telemetry, incorrect log collection, decoder errors, rule logic, indexing delays, or resource exhaustion.

### B. Objectives

1. Establish a controlled lab environment for authorized security testing.
2. Measure selected security-awareness practices using a documented survey methodology.
3. Conduct approved phishing-awareness simulations using Gophish without retaining real user passwords.
4. Assess an isolated OWASP Juice Shop target using Acunetix DAST.
5. Configure Wazuh agents to collect relevant host and application telemetry.
6. Develop and validate decoders and detection rules for selected test events.
7. Map test scenarios to relevant MITRE ATT&CK behaviors where justified.
8. Record operational constraints, including SIEM resource consumption and configuration errors.
9. Define a feedback process for improving detection coverage and user awareness.

## III. Related Work and Technical Background

Wazuh provides agent-based collection, security analytics, file integrity monitoring, and host monitoring capabilities. Gophish provides campaign management for authorized phishing-awareness exercises. Acunetix provides automated web-application security testing. OWASP Juice Shop is a deliberately insecure application suitable for security training and controlled testing. MITRE ATT&CK provides a knowledge base for describing adversary tactics and techniques.

The project combines these capabilities in a single test workflow. Its emphasis is operational: the relevant question is not only whether a scanner identifies a weakness or an endpoint generates a log, but whether the event can be traced through collection, parsing, rule evaluation, indexing, and analyst presentation.

A final publication should expand this section with specific peer-reviewed studies and official technical documentation. General product descriptions alone are not a sufficient literature review.

## IV. Framework Architecture

### A. People: awareness baseline and phishing simulation

A structured awareness survey measures selected self-reported practices, such as interaction with unverified links, password reuse, use of unsecured public wireless networks, postponement of security updates, use of untrusted removable media, and multi-factor authentication adoption.

Gophish is used for approved simulations. Campaign metrics should be reported separately: messages attempted and delivered; opens where reliable tracking is enabled; links clicked; data submitted to a controlled training landing page; and report-phishing actions, if measured.

A campaign must not collect actual passwords. The survey measures stated or recalled behavior, whereas a campaign measures observed behavior under a specific simulation. These measures must not be merged into one statistic.

### B. Process: automated application assessment

Acunetix DAST assesses an isolated OWASP Juice Shop deployment. Record the target build/version, scan profile, authentication configuration, date, and scope.

Potential findings such as SQL injection and cross-site scripting must be reported only when supported by the actual scan report and appropriate validation. Each finding should include its scanner identifier, severity, affected component, evidence summary, and validation status. Sensitive payloads and target details must be sanitized in public artifacts.

### C. Technology: centralized telemetry and SOC monitoring

Wazuh agents are configured on monitored lab endpoints to collect selected system and application logs. Relevant events are forwarded to the Wazuh Manager and Indexer for analysis and visualization.

A complete custom-decoder and rule validation chain should preserve: the original sanitized log event; proof that the agent collected and forwarded it; decoder output or wazuh-logtest result; matching rule identifier and severity; resulting alert document or dashboard record; and timestamps sufficient to correlate each stage.

A dashboard screenshot alone is not enough to prove the entire pipeline.

## V. Threat Modeling and MITRE ATT&CK Mapping

The supplied material associates phishing simulation with Initial Access and references technique T1566. The exact sub-technique should be selected only when the simulation scenario supports it.

| Test scenario | ATT&CK mapping | Expected telemetry | Defensive validation |
|---|---|---|---|
| Phishing link delivery | T1566 family, if scenario-appropriate | Campaign delivery and interaction records | Campaign event captured and reviewed |
| Web input attack simulation | Map only to a technique supported by actual behavior | Application access/error logs | Decoder/rule test and alert evidence |
| Unauthorized file modification in lab | Select a technique only if tested behavior matches it | File integrity event | Wazuh FIM alert evidence |
| Suspicious process or login activity | Map after documenting exact behavior | Endpoint process/authentication log | Rule match and alert record |

ATT&CK mappings are analytical labels, not proof that a complete adversary technique or intrusion chain was reproduced.

## VI. Research Methodology

### A. Environment and scope

Testing is intended for an isolated virtualized lab. The web application target is an OWASP Juice Shop container. The final paper should identify the host operating system, virtualization platform, network mode, CPU and memory allocation, container image/version, and relevant tool versions.

### B. Survey methodology

The supplied project material reports a survey sample of 50 participants. Before publication, document recruitment method, participant eligibility, survey period, question wording, consent/privacy process, response completeness, and denominator for each percentage.

For a question with x responses out of N valid responses:

P = (x / N) × 100

The denominator may differ by question if responses are missing. Recalculate percentages from the source export rather than copying values without verification.

### C. Phishing simulation methodology

Document campaign scope, approval, audience handling, template description, landing-page behavior, delivery configuration, and event definitions. Record only controlled training data. Report delivery, click, and submission rates separately, each with its denominator.

### D. DAST methodology

Record target scope, scan date, scan profile, authentication status, crawler coverage, and exported findings. Triage and safely validate findings in the isolated target. Distinguish scanner output from manually confirmed vulnerabilities.

### E. SIEM validation methodology

Use known test events and a documented expected result. Syntax-check and test custom decoder and rule files before deployment. For each event, preserve sanitized raw input, test output, rule ID, alert record, and timestamp correlation.

### F. Offline telemetry analysis

The project notes describe using MATLAB filtfilt for forward-backward, zero-phase filtering of telemetry series. This is an offline analytical technique that can help visualize trends without the phase shift associated with a one-pass filter. It does not establish a real-time SIEM filtering capability. Document sampling interval, selected filter, cutoff frequencies, filter order, treatment of missing values, and limitations at signal boundaries.

## VII. Results and Observations

> **Evidence required:** Values below are transcribed from supplied project notes. They are provisional and must be recalculated from original survey and tool exports before publication.

### A. Human-awareness survey

The supplied notes report the following values for N = 50:

| Risk indicator | Reported percentage | Arithmetic count if denominator is 50 |
|---|---:|---:|
| Immediate interaction with unverified phishing links | 24% | 12 |
| Password reuse | 20% | 10 |
| Connection to unsecured public Wi-Fi | 46% | 23 |
| Postponement of critical security updates | 48% | 24 |
| Willingness to insert untrusted USB media | 20% | 10 |
| No multi-factor authentication enabled | 14% | 7 |

These counts are arithmetic equivalents only, not verified participant counts. The original export must confirm the denominator, exact wording, and whether each item was a yes/no response or a derived category. Survey responses must not be interpreted as observed compromise or actual phishing campaign performance.

### B. DAST observations

The supplied material describes SQL injection and cross-site scripting findings from an Acunetix assessment of OWASP Juice Shop. Exact finding IDs, severity labels, affected endpoints, scanner evidence, and manual validation records were not included in the manuscript text. These are therefore reported observations pending evidence review, not independently confirmed results.

### C. Wazuh telemetry and decoder validation

The project material describes application log collection and custom XML decoder/rule development. However, the source descriptions conflict: one states that custom decoders successfully produced high-priority alerts, while another reports XML parsing errors in local_rules.xml and incomplete rule deployment. The final result must distinguish stages that worked from those that failed or remained unverified.

### D. Indexer resource pressure

The supplied notes report Linux kernel Out-Of-Memory termination of the Wazuh Indexer during high-volume testing and describe setting JVM heap boundaries to 5.3 GB. This value is not a universal recommended setting. Host physical RAM, swap, other services, heap configuration, indexer logs, and before/after memory measurements are required to establish whether the change resolved the issue.

### E. Zero-phase filtering

MATLAB filtfilt is described as an offline method for examining smoothed telemetry trends without phase delay. No numerical comparison, filter specification, input dataset, or performance measurement was supplied. Accordingly, no quantitative improvement claim is made.

## VIII. Discussion

The framework demonstrates the value of connecting offensive test scenarios with defensive observability. A scanner finding can inform monitoring priorities; a controlled simulation can produce a known event; and the SIEM pipeline can then be tested against that event. This creates a practical feedback loop that is more informative than operating each tool independently.

The integration also exposes dependencies that can be overlooked in high-level architecture diagrams. An endpoint event must be generated, collected, transported, parsed, evaluated, indexed, and displayed. Failure at any stage can prevent an analyst from seeing the expected alert. Resource exhaustion can interrupt indexing, while malformed XML can prevent custom detection logic from loading.

Human-risk measurements provide additional context, but survey data has limitations. Self-reported behavior may differ from actual behavior, and a small institutional sample should not be generalized to all organizations. Controlled phishing exercises also require careful governance, explicit authorization, and privacy safeguards.

## IX. Limitations and Threats to Validity

1. Survey values require confirmation from the original response export and question-level denominators.
2. Original Gophish campaign metrics and delivery evidence were not supplied with the manuscript text.
3. Acunetix findings require scan exports and validation records.
4. Wazuh decoder/rule success claims conflict across the supplied project descriptions.
5. The 5.3 GB heap setting lacks host and before/after measurements to establish causality.
6. MATLAB filtering discussion lacks data and parameters needed for reproducibility.
7. A single isolated lab does not represent the diversity of production enterprise environments.
8. The supplied material does not provide a controlled baseline demonstrating reduced detection or response time.

## X. Recommendations and Future Work

- Automate a test-event-to-alert validation checklist.
- Maintain versioned Wazuh decoder and rule tests.
- Measure event loss, ingestion delay, indexing health, and alert latency under controlled load.
- Add repeatable scan configurations and sanitized Acunetix exports.
- Report Gophish campaign outcomes with explicit denominators and privacy controls.
- Expand survey methodology and publish anonymized aggregate data where consent permits.
- Map each simulation to a justified ATT&CK technique and specific telemetry source.
- Evaluate SOAR case-management integration as a separate future phase.
- Explore cloud-native monitoring and security-awareness feedback workflows.

Any proposed integration with TheHive or automated remediation must be labeled future work until implemented and tested.

## XI. Conclusion

The 360° Cyber Shield presents a practical Purple Teaming approach connecting human-awareness assessment, automated web-application testing, and centralized security monitoring. Its central idea is to use controlled offensive activity to test defensive visibility and then use the resulting evidence to improve detection engineering. The project notes also highlight operational realities such as malformed detection configuration and indexer memory pressure. A credible final evaluation depends on preserving the distinction between intended design, implemented configuration, successful tests, partial tests, and proposed enhancements. With the underlying survey exports, scanner reports, sanitized telemetry, rule-test output, and system measurements attached, the framework can be evaluated more rigorously and reproduced by other researchers.

## References

[1] Wazuh, Wazuh Documentation. https://documentation.wazuh.com/

[2] Gophish, Gophish Documentation. https://getgophish.com/documentation/

[3] OWASP, OWASP Juice Shop Project. https://owasp.org/www-project-juice-shop/

[4] OWASP, OWASP Top 10. https://owasp.org/www-project-top-ten/

[5] MITRE, MITRE ATT&CK. https://attack.mitre.org/

[6] National Institute of Standards and Technology, Cybersecurity Framework. https://www.nist.gov/cyberframework

[7] MathWorks, filtfilt — Zero-phase digital filtering. https://www.mathworks.com/help/signal/ref/filtfilt.html

[8] Invicti Security, Acunetix Documentation. Add the exact product documentation page and version consulted.

> Before submission, verify bibliographic metadata, publication dates, versions, and access dates. Replace generic product references with the exact primary sources actually used.
