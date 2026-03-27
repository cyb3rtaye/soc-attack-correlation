# Attack Chain

## Objective

To define a realistic sequence of attacker behaviour that can be simulated, detected, and analysed as a correlated event chain rather than as isolated alerts.

This project focuses on identifying how multiple low-level behaviours can combine into a stronger signal of suspicious activity.

---

## Scenario Overview

The simulated attack chain in this lab follows a simple but realistic pattern:

1. PowerShell execution  
2. Suspicious shell-to-shell process chain  
3. certutil usage for potential file retrieval  
4. Centralised visibility through Wazuh  

Individually, each event may appear low severity. When observed together within a short period on the same host, they form a stronger behavioural indicator.

---

## Attack Sequence

### Step 1: PowerShell Execution

PowerShell is executed to simulate command-based activity.

This represents an execution event that may be benign in isolation but becomes more significant when followed by additional suspicious behaviour.

### Step 2: Suspicious Process Chain

`cmd.exe` launches `powershell.exe`, creating a parent-child relationship that may indicate chained execution or scripted behaviour.

This provides behavioural context that is more meaningful than process creation alone.

### Step 3: certutil Usage

`certutil.exe` is executed with arguments that simulate file retrieval behaviour.

This represents Living Off the Land activity using a trusted Windows utility and raises the level of suspicion when combined with the earlier events.

### Step 4: Centralised Analyst Visibility

The resulting telemetry is captured by Sysmon and made visible through Wazuh, enabling the analyst to review the sequence as part of a broader investigation.

---

## Why This Chain Matters

A single PowerShell execution may be benign.

A single `cmd.exe` to `powershell.exe` chain may still be explainable.

A single `certutil.exe` event may occasionally be administrative.

However, when these behaviours occur on the same host within a short time window, they become more indicative of attacker activity.

This is the basis of correlation: multiple weak signals combining into a stronger detection story.

---

## MITRE ATT&CK Mapping

### PowerShell Execution
- Tactic: Execution  
- Technique: Command and Scripting Interpreter: PowerShell (T1059.001)  

### Suspicious Process Chain
- Tactic: Execution  
- Technique: Command and Scripting Interpreter (T1059)  

### certutil Usage
- Tactic: Command and Control  
- Technique: Ingress Tool Transfer (T1105)  

---

## Correlation Goal

The purpose of this project is not only to detect these individual behaviours, but to recognise that they are linked by:

- host identity  
- timing  
- process context  
- behavioural progression  

This supports a more realistic SOC workflow in which analysts build an attack narrative from multiple related events.

---

## Expected Analyst View

From an analyst perspective, the sequence can be interpreted as:

- an execution event begins  
- command activity becomes more suspicious through process chaining  
- a legitimate system binary is then used in a potentially malicious way  
- multiple detections on the same endpoint increase confidence that the activity deserves investigation  

---

## Outcome

This attack chain provides the behavioural foundation for the rest of the project.

The next phases will define how the sequence is detected, simulated, and analysed as a correlated set of events rather than as isolated alerts.