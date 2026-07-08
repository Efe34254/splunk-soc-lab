# Splunk SOC Lab

Home SOC lab project built to demonstrate basic SOC analyst skills using Splunk, Windows Event Logs, and Sysmon.

## Objective

The goal of this lab is to collect Windows security and Sysmon logs, search them with SPL, and document simple investigation workflows for common SOC alerts.

## Skills Demonstrated

- SIEM monitoring
- Alert triage
- Windows Event Log analysis
- Sysmon event analysis
- Basic threat detection
- Incident investigation documentation

## Lab Environment

| Component | Purpose |
|---|---|
| Windows 10 VM | Endpoint generating logs |
| Sysmon | Enhanced endpoint telemetry |
| Splunk Enterprise / Free | SIEM for log ingestion and searching |
| Splunk Universal Forwarder | Forward Windows/Sysmon logs to Splunk |

## Detection Use Cases

1. Failed login attempts
2. Suspicious PowerShell execution
3. Sysmon process creation monitoring
4. Sysmon network connection monitoring
5. Brute-force investigation workflow

## Repository Structure

```text
splunk-soc-lab/
├── README.md
├── spl-queries/
│   ├── failed_logins_4625.spl
│   ├── suspicious_powershell.spl
│   ├── sysmon_process_creation.spl
│   └── sysmon_network_connections.spl
├── investigation-notes/
│   └── brute-force-investigation.md
├── configs/
│   └── inputs.conf
├── dashboards/
│   └── dashboard-notes.md
└── screenshots/
```

## Example SPL Queries


## Lab Evidence

This lab was built on a Windows 10 virtual machine using Splunk Enterprise and Sysmon.

Evidence collected:
- Splunk successfully indexed Windows Sysmon Operational logs.
- `index=*` returned over 7,000 events from the lab environment.
- Sysmon-related searches returned over 6,000 events.
- Process Create activity was identified using Sysmon Event ID 1.

Screenshots:
- `screenshots/splunk-all-events.png`
- `screenshots/splunk-sysmon-events.png`
- `screenshots/splunk-process-create-events.png`

See the `spl-queries/` folder.

## Notes

This project uses a home lab environment. No real company data, customer data, or sensitive logs are included.
