# Framework Architecture

## Logical data flow

```text
PEOPLE
Awareness survey ────────┐
Gophish simulation ──────┤
                         v
PROCESS              Test scenario and evidence
Acunetix DAST ───────────┤
OWASP Juice Shop target ┘
                         |
                         v
TECHNOLOGY
Wazuh Agent -> Wazuh Manager -> Decoder / Rules -> Indexer -> Dashboard
                         |
                         v
PURPLE TEAM FEEDBACK
Expected event vs observed event -> Gap analysis -> Detection tuning -> Retest
```

## Core components

| Component | Input | Output | Validation evidence |
|---|---|---|---|
| Awareness survey | Participant responses | Anonymized aggregate results | Original export, question wording, denominator |
| Gophish | Approved campaign configuration | Delivery and interaction events | Campaign export and event definitions |
| Acunetix | In-scope lab URL | DAST findings | Scan export and safe validation |
| OWASP Juice Shop | Controlled test requests | Application behavior and logs | Version, scope, sanitized logs |
| Wazuh Agent | Host/application logs | Forwarded events | Agent status and collection evidence |
| Wazuh Manager | Forwarded events | Decoder and rule results | wazuh-logtest and rule IDs |
| Wazuh Indexer/Dashboard | Alerts and events | Searchable SOC view | Alert document and timestamps |

## Detection validation stages

A test is end-to-end validated only when evidence exists for each applicable stage:

1. Test action executed in authorized scope.
2. Expected source event generated.
3. Agent collected and forwarded the event.
4. Manager decoded the event.
5. Intended rule matched.
6. Alert was indexed and visible.
7. Analyst interpretation and follow-up were recorded.

If a stage is not proven, report the result as partial or unverified rather than successful.
