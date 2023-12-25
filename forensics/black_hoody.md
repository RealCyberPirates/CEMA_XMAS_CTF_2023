# Black Hoody

## Introduction

In the "Black Hoody" challenge, we embarked on a journey to uncover the actions of a suspicious individual who used a USB stick on Santa's computer. The challenge involved analyzing Windows event logs to trace the attacker's steps and discover the nature of the attack.

## Methodology

### Step 1: Event Log Analysis

- Initial Clue: Santa's encounter with a suspicious person holding a USB stick suggested unauthorized activity on his computer.
- Event Log Conversion: We used evtxexport to convert Windows event logs into a readable text format for analysis.
- Investigation Goal: The first task was to identify the executable run from the USB stick.

### Step 2: Identifying Malicious Activity

- Executable Discovery: Analysis of the event logs led to the discovery of `G:\svchost.exe` being executed from the USB stick, mimicking a legitimate Windows process.
- Privilege Escalation: Further investigation revealed a command used for privilege escalation: `cmd.exe /c echo pbaycc > \\.\pipe\pbaycc`.

### Step 3: Determining the Payload

- Challenging Aspect: The most challenging part was identifying the payload used to control Santa's computer.
- Educated Guess: Without direct evidence from the logs, an educated guess led to the conclusion that the payload was `Meterpreter`, a common and versatile payload used in penetration testing and malicious attacks.

This led to the flag: `CEMA{N1ce_J0b_Incident_R3sponder!}`

## Conclusion

The "Black Hoody" challenge emphasized the importance of meticulous log analysis in cybersecurity. By combing through the event logs, we successfully uncovered the executable used in the initial breach and the command for privilege escalation. Although the final payload was not explicitly found in the logs, our understanding of typical attack patterns and payloads guided us to a reasonable conclusion.
