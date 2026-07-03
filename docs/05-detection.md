# Detection Design

## Purpose

Translate the documented behaviours into candidate detection and correlation conditions.

## Event-Level Conditions

### PowerShell Execution

```text
Event ID = 1
AND Image ends with \\powershell.exe
```

### Shell-to-Shell Execution

```text
Event ID = 1
AND Image ends with \\powershell.exe
AND ParentImage ends with \\cmd.exe
```

### URL-Based certutil Use

```text
Event ID = 1
AND Image ends with \\certutil.exe
AND CommandLine contains -urlcache
AND CommandLine contains http
```

## Correlation Condition

Create an investigation lead when all three conditions occur on the same endpoint within five minutes.

## Analyst Context to Include

- endpoint and agent name
- account name
- complete command lines
- parent and child process paths
- first and last event timestamps
- related alerts from the same endpoint

## Implementation Note

These are analytical conditions rather than a claim of a deployed production rule. Any implementation in Wazuh or another SIEM should be tested against the platform's available fields and normal activity before use.
