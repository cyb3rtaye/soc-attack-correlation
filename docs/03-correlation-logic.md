# Correlation Logic

## Objective

To define how individual events are linked together to form a meaningful detection narrative.

Rather than analysing alerts in isolation, this phase focuses on identifying relationships between events based on context, timing, and behaviour.

---

## What is Correlation

Correlation is the process of connecting multiple events to determine whether they represent a sequence of related activity.

In a SOC environment, correlation allows analysts to move from:

Single alerts → Behavioural patterns → Attack understanding

---

## Correlation Strategy

The correlation approach in this project is based on four key factors:

- Host correlation (same system)
- Time correlation (events occurring close together)
- Process relationship (parent-child links)
- Behavioural progression (logical attack sequence)

---

## Correlation Conditions

### 1. Same Host

All events originate from the same endpoint.

---

### 2. Time Proximity

Events occur within a short timeframe (for example, within a few minutes).

---

### 3. Process Context

Events show a relationship between processes:

- cmd.exe launching powershell.exe
- powershell execution preceding certutil usage

---

### 4. Behavioural Sequence

The order of activity follows a logical progression:

1. Execution (PowerShell)
2. Process chaining (cmd → PowerShell)
3. Tool usage (certutil)

---

## Example Correlation Flow

PowerShell execution  
→ Process chain detected  
→ certutil usage observed  

Individually:
- Low or medium value events

Combined:
- Strong behavioural indicator

---

## Detection Logic Concept

Instead of triggering alerts on single events, the goal is to identify:

Multiple related events on the same host within a short time window

---

## Analyst Interpretation

Correlation enables analysts to:

- understand attacker intent
- identify escalation of behaviour
- prioritise investigations
- reduce noise from isolated alerts

---

## Detection Confidence Levels

### Low Confidence
Single event (e.g. PowerShell execution)

### Medium Confidence
Process chain behaviour

### High Confidence
Multiple correlated behaviours within a short timeframe

---

## Outcome

This phase establishes the logic required to link events together into a meaningful detection narrative.
