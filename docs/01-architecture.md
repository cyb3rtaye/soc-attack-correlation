# Architecture

## Purpose

The architecture supports collection and analysis of process creation activity from a Windows endpoint.

## Components

| Component | Role |
|---|---|
| Windows endpoint | Generates the controlled process activity |
| Sysmon | Records process creation, command lines and parent-child relationships |
| Wazuh | Provides centralised event visibility for investigation |
| Analyst workflow | Links related events and determines whether escalation is justified |

## Data Flow

```text
Controlled activity
        ↓
Sysmon Event ID 1
        ↓
Wazuh ingestion and search
        ↓
Host, user, process and time correlation
        ↓
Analyst assessment
```

## Correlation Fields

The most useful fields for this scenario are:

- hostname or agent identifier
- user account
- process image
- parent process image
- command line
- process identifier
- event timestamp

These fields allow the events to be reviewed as a sequence rather than as unrelated alerts.
