# Attack Correlation

## Overview

This project documents how related endpoint events can be combined into a single investigation narrative. The scenario links PowerShell execution, a `cmd.exe` to `powershell.exe` process chain and `certutil.exe` activity on the same Windows host within a short time window.

The purpose is to show how several low- or medium-confidence events can become more significant when they share host, user, process and timing context.

## Scenario

1. PowerShell command execution
2. Shell-to-shell process chaining
3. `certutil.exe` used with a URL
4. Correlation by host and time
5. Analyst assessment and escalation decision

## Telemetry

- Sysmon Event ID 1 process creation records
- Process image and parent image
- Command-line arguments
- Hostname, user and timestamps
- Centralised event visibility through Wazuh

## Documentation

- [`docs/01-architecture.md`](docs/01-architecture.md) — components and data flow
- [`docs/02-attack-chain.md`](docs/02-attack-chain.md) — behavioural sequence
- [`docs/03-correlation-logic.md`](docs/03-correlation-logic.md) — correlation conditions
- [`docs/04-simulation.md`](docs/04-simulation.md) — controlled test procedure
- [`docs/05-detection.md`](docs/05-detection.md) — candidate detection logic
- [`docs/06-analysis.md`](docs/06-analysis.md) — analyst interpretation and limitations

## Project Status

This repository is a correlation design and analysis exercise built from endpoint behaviours validated in the related threat-detection lab. It does not claim that a production correlation rule was deployed.

## Security Scope

All testing was performed inside a controlled, non-production lab.
