# Dashboard Notes

This file documents planned dashboard panels for the Splunk SOC Lab.

## Objective

The goal of the dashboard is to provide a quick overview of Windows and Sysmon activity collected from the lab endpoint.

## Planned Dashboard Panels

### 1. Sysmon Event Overview

Purpose:

Show the total number of Sysmon events collected from the Windows 10 VM.

Example SPL:

```spl
index=* "Sysmon"
| timechart count
```

### 2. Process Creation Activity

Purpose:

Monitor Sysmon Event ID 1 process creation events.

Example SPL:

```spl
index=* EventCode=1
| stats count by Image
| sort - count
```

### 3. Suspicious PowerShell Execution

Purpose:

Identify PowerShell executions that may indicate suspicious command usage.

Example SPL:

```spl
index=* EventCode=1 Image="*powershell.exe*"
(CommandLine="*-enc*" OR CommandLine="*-EncodedCommand*" OR CommandLine="*IEX*" OR CommandLine="*DownloadString*" OR CommandLine="*FromBase64String*" OR CommandLine="*bypass*")
| table _time ComputerName User CommandLine ParentImage
| sort - _time
```

### 4. Network Connections

Purpose:

Monitor Sysmon Event ID 3 network connection activity.

Example SPL:

```spl
index=* EventCode=3
| stats count by DestinationIp, DestinationPort, Image
| sort - count
```

### 5. Failed Login Attempts

Purpose:

Identify repeated failed authentication attempts.

Example SPL:

```spl
index=* EventCode=4625
| stats count by Account_Name, Source_Network_Address, Workstation_Name
| sort - count
```

## Notes

This dashboard is designed for a home SOC lab environment.  
No real company data, customer data, or sensitive logs are included.
