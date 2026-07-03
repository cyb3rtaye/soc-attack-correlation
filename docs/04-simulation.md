# Controlled Simulation

## Objective

Generate the documented process sequence on one Windows endpoint so the resulting Sysmon events can be reviewed together.

## Commands

Run the commands within one or two minutes from the same user session.

### PowerShell Execution

```powershell
powershell.exe -Command "Get-Process"
```

### Shell Process Chain

```powershell
cmd.exe /c powershell.exe -Command "Get-Date"
```

### certutil Process Activity

```powershell
certutil.exe -urlcache -split -f https://example.com/ sample.txt
```

The correlation exercise only requires the process and command-line telemetry; a successful file download is not required.

## Observation Points

### Sysmon

```text
Event Viewer
Applications and Services Logs
Microsoft
Windows
Sysmon
Operational
```

Review Event ID 1 records for process image, parent image, command line, user and timestamp.

### Wazuh

Search the Windows agent events for the same execution period and confirm that the related fields are available for analysis.

## Expected Evidence

- PowerShell process creation
- `cmd.exe` to `powershell.exe` parent-child relationship
- `certutil.exe` process creation with URL arguments
- timestamps close enough to support correlation
