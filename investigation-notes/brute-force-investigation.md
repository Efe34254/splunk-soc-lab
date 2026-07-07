# Brute-Force Investigation Workflow

## Alert

Multiple failed login attempts detected from the same source IP address.

## Initial Questions

- Which user account was targeted?
- How many failed attempts occurred?
- Did any successful login happen after the failures?
- Was the source IP internal or external?
- Is the targeted account privileged?

## SPL Search

```spl
index=wineventlog EventCode=4625
| stats count by Account_Name, Source_Network_Address, Workstation_Name
| sort - count
```

## Triage Steps

1. Identify the source IP address.
2. Check the targeted account name.
3. Search for successful logins from the same source.
4. Check whether the source IP appears in threat intelligence tools.
5. Escalate if there is evidence of successful compromise or privileged account targeting.

## Possible Response Actions

- Block source IP if malicious and external.
- Reset password for targeted account if needed.
- Escalate to senior analyst with evidence.
- Document all findings in the ticketing system.

## Analyst Notes

This is a lab workflow and does not contain real customer or company data.
