# Correlation Logic

## Objective

Define the conditions that would link the three process events into a higher-confidence investigation lead.

## Required Conditions

### Same Endpoint

All events must originate from the same Windows host or Wazuh agent.

### Time Proximity

The events should occur within a short window, such as five minutes. The final value would require tuning against normal administrative activity.

### Process and Command Context

The sequence should contain:

- `powershell.exe` execution
- `cmd.exe` as the parent of `powershell.exe`
- `certutil.exe` with URL-related command-line arguments

### Logical Order

The events should follow a plausible progression from command execution to native-tool use.

## Candidate Correlation

```text
WHEN PowerShell execution occurs
AND cmd.exe launches powershell.exe
AND certutil.exe contains a URL argument
ON the same endpoint
WITHIN five minutes
THEN create a correlation lead for analyst review
```

## Confidence Model

| Observation | Indicative confidence |
|---|---|
| PowerShell alone | Low |
| Shell-to-shell process chain | Medium |
| URL-based certutil use | Medium to high, depending on context |
| All three on one host in a short window | Higher-priority investigation lead |

## Tuning Considerations

- approved administration scripts
- software deployment activity
- known service accounts
- expected download domains
- repeated events from the same user or host

The correlation should support investigation, not automatically declare an incident.
