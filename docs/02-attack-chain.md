# Attack Chain

## Objective

Define a controlled sequence of behaviours that can be analysed as one related event chain rather than as isolated process events.

## Sequence

### 1. PowerShell Execution

PowerShell is started with a simple command. A single PowerShell event may be legitimate, so it is treated as low-confidence activity without additional context.

### 2. Shell Process Chain

`cmd.exe` launches `powershell.exe`. The parent-child relationship provides more context than the child process alone and may indicate scripted or chained execution.

### 3. certutil Activity

`certutil.exe` is started with URL-related arguments. This is a legitimate Windows utility, but URL-based use can be associated with file retrieval and deserves review when it follows other suspicious activity.

### 4. Centralised Review

The events are reviewed together using the same endpoint, user and time window. Their combined pattern provides a stronger reason to investigate than any one event by itself.

## MITRE ATT&CK Mapping

| Behaviour | Technique |
|---|---|
| PowerShell execution | T1059.001 — Command and Scripting Interpreter: PowerShell |
| Windows command shell | T1059.003 — Command and Scripting Interpreter: Windows Command Shell |
| URL-based file retrieval | T1105 — Ingress Tool Transfer |

## Interpretation

The mapping describes the simulated behaviours. It does not by itself prove malicious intent; the analyst must still validate user, host and command context.
