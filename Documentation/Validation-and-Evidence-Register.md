# Validation and Evidence Register

Use this register before claiming that a project capability or result was successfully demonstrated. Store only sanitized evidence.

| Claim | Evidence required | Current status from supplied notes |
|---|---|---|
| Survey sample was 50 | Original export, recruitment details, valid response count | Reported; verify |
| Phishing interaction rate was 24% | Exact question or campaign metric, numerator, denominator | Ambiguous; separate survey and campaign |
| Password reuse was 20% | Question wording and response export | Reported; verify |
| Public Wi-Fi risk was 46% | Question wording and response export | Reported; verify |
| Update postponement was 48% | Question wording and response export | Reported; verify |
| USB risk was 20% | Question wording and response export | Reported; verify |
| MFA absence was 14% | Question wording and response export | Reported; verify |
| Acunetix found SQL injection | Sanitized scan report, finding ID, validation | Reported; evidence missing |
| Acunetix found XSS | Sanitized scan report, finding ID, validation | Reported; evidence missing |
| Wazuh decoded application attack logs | Sanitized raw event, decoder test output | Conflicting descriptions |
| Wazuh rule generated alert | Rule ID, wazuh-logtest output, indexed alert | Conflicting descriptions |
| 5.3 GB heap resolved OOM | Host RAM/swap, heap config, OOM logs, before/after metrics | Reported; not established |
| MATLAB zero-phase filtering used | Script, dataset description, filter parameters, output | Reported; evidence missing |
| Real-time detection improvement | Baseline and post-change latency/event-loss measurements | Not established |

## Evidence capture checklist

- [ ] Tool and version recorded.
- [ ] Date/time and timezone recorded.
- [ ] Authorized target scope documented.
- [ ] Original export retained privately.
- [ ] Public copy sanitized.
- [ ] Numerator, denominator, and calculation method recorded.
- [ ] Expected result defined before the test.
- [ ] Actual result and deviations recorded.
- [ ] Failed or partial tests retained rather than omitted.
- [ ] No credentials, secrets, personal data, or sensitive target details committed.

## Publication rule

Use “implemented” only when the feature exists in the project. Use “configured” when configuration is present. Use “tested” only when a reproducible test was run. Use “validated” only when the expected behavior is supported by evidence. Use “proposed” for future work.
