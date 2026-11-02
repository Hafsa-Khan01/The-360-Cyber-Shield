# Wazuh SIEM Validation Notes

## Objective

Validate the path from a known lab event to a searchable Wazuh alert. A screenshot of the dashboard alone does not prove collection, parsing, rule matching, and indexing.

## Validation sequence

1. Generate a benign, known test event on an authorized lab endpoint.
2. Confirm the relevant log source is configured for collection.
3. Confirm the Wazuh agent is connected and forwarding events.
4. Test decoder and rule behavior with wazuh-logtest.
5. Record the matching rule ID and severity.
6. Confirm the alert is indexed and searchable.
7. Correlate timestamps and retain sanitized evidence.

## XML configuration troubleshooting

The supplied project notes mention XML parsing errors in local_rules.xml. Validate XML syntax and test custom rules before restarting or relying on the manager. Preserve the exact error output and the corrected test result. Do not describe a rule as operational until it matches a representative event.

## Indexer resource troubleshooting

The notes report OOM termination and a 5.3 GB JVM heap adjustment. Heap values must be selected in relation to total host memory and other services. Record total RAM, swap, heap minimum/maximum, indexer logs, kernel OOM messages, and before/after resource measurements. Do not treat 5.3 GB as a general recommendation.

## Safe publication

Remove passwords, tokens, IP addresses where sensitive, hostnames, usernames, email addresses, and proprietary event data from public logs and screenshots.
