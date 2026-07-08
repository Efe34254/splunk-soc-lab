# Brute-Force Investigation Workflow

## Alert

Multiple failed login attempts were detected from the same source IP address or workstation.

## Objective

Investigate repeated failed authentication attempts and determine whether the activity represents a brute-force attempt, password spraying, misconfiguration, or normal user error.

## Initial Questions

- Which user account was targeted?
- How many failed login attempts occurred?
- Did any successful login occur after the failures?
- Was the source IP internal or external?
- Is the targeted account privileged?
- Did the activity happen outside normal working hours?

## Relevant Windows Event IDs

| Event ID | Description |
|---|---|
| 4625 | Failed logon |
| 4624 | Successful logon |
| 4740 | Account lockout |
| 4672 | Special privileges assigned to new logon |

## SPL Search: Failed Login Attempts

```spl
index=* EventCode=4625
| stats count by Account_Name, Source_Network_Address, Workstation_Name
| sort - count
```

## SPL Search: Successful Login After Failures

```spl
index=* EventCode=4624
| stats count by Account_Name, Source_Network_Address, Workstation_Name
| sort - count
```

## SPL Search: Account Lockout Events

```spl
index=* EventCode=4740
| table _time Account_Name Caller_Computer_Name ComputerName
| sort - _time
```

## SPL Search: Privileged Logon Events

```spl
index=* EventCode=4672
| table _time Account_Name ComputerName Logon_ID
| sort - _time
```

## Triage Steps

1. Identify the source IP address or workstation.
2. Check the targeted account name.
3. Count the number of failed attempts.
4. Search for successful logins from the same source after the failed attempts.
5. Check whether the targeted account is privileged.
6. Review whether the activity occurred outside normal working hours.
7. Check whether the source IP or host appears in threat intelligence tools.
8. Escalate if there is evidence of successful compromise, privileged account targeting, or suspicious external access.

## Investigation Logic

A high number of failed login attempts from the same source may indicate brute-force activity.  
A high number of failed attempts across many accounts may indicate password spraying.  
Failed logins followed by a successful login should be treated as higher priority.  
Privileged account targeting should be escalated immediately.

## Possible Response Actions

- Block the source IP if it is confirmed malicious and external.
- Reset the password for the targeted account if needed.
- Disable or lock the account temporarily if compromise is suspected.
- Review successful logons after the failed attempts.
- Escalate to a senior analyst with supporting evidence.
- Document all findings in the ticketing system.

## Evidence to Collect

- Targeted account name
- Source IP address or workstation
- Number of failed login attempts
- Time range of the activity
- Any successful logins after the failed attempts
- Whether the targeted account is privileged
- Related hostnames or affected systems

## Analyst Notes

This is a lab workflow created for SOC analyst practice. It does not contain real customer data, company data, or sensitive logs.
