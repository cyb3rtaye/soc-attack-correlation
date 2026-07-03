# Correlation Analysis

## Analyst Narrative

A PowerShell process was observed on a Windows endpoint. Shortly afterwards, `cmd.exe` launched another PowerShell process, followed by `certutil.exe` with URL-related arguments. All events occurred under the same host and user context within a short time window.

The sequence is more significant than a single PowerShell event because it combines shell execution, process chaining and native-tool activity associated with file retrieval. The pattern warrants validation of the user, command purpose and destination before escalation.

## Investigation Questions

- Was the user authorised to run the commands?
- Was the endpoint undergoing approved administration or software deployment?
- Did the URL belong to an approved service?
- Did the retrieved file exist, execute or create further network activity?
- Were similar events observed on other hosts?
- Did Microsoft Defender or Wazuh generate related alerts?

## Suggested Disposition

- **Benign:** confirmed administrative or testing activity with an approved destination
- **Suspicious:** no clear business justification or unusual user/host context
- **Escalate:** additional execution, persistence, credential access or outbound communication is identified

## Limitations

This repository documents correlation logic and analyst reasoning. It does not contain an evidence pack or claim that an automated production correlation rule was deployed.
