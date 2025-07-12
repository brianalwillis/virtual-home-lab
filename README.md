<h1 = align=center>Creating a Virtual Home Lab</h1>

<img width="1162" height="902" alt="Untitled Diagram drawio" src="https://github.com/user-attachments/assets/7387547d-fbac-4c45-b6a7-ea13775466c6" />

## 🏡 What is a Virtual Home Lab?
A **virtual home lab** is a software-based environment you set up at home to test, learn, or experiment with IT infrastructure, networking, cybersecurity, development, or system administration — without needing a full rack of physical servers.

**A virtual lab usually includes:**
|Component        |Purpose 
|-----------------|------------------------------------------------------------------------------|
|Hypervisor       | Allows you to run multiple virtual machines on your PC                       |
|Virtual Machines | Each VM can simulate a server, router, or client                             |
|Virtual Network  | Simulates switches, routers, and firewalls to test real networking scenarios |
|Storage          | Shared virtual drives for things like file servers or backup testing         |
|Services         | DNS, DHCP, Active Directory, Web Servers, Pen-testing tools, etc.            |

**What can you do with a virtual home lab?**
|Component        |Purpose 
|-----------------|---------------------------------------------------------------------------|
|Learn IT Skills       | Practice Windows Server, Linux, networking, Docker, Kubernetes, etc. |
|Cybersecurity Testing | Set up attack & defense labs                                         |
|Certifications        | Prepare for exams like CompTIA, Cisco, AWS, Microsoft, etc.          |
|Software Development  | Isolate dev/test environments                                        |
|Home Automation       | Run Home Assistant, Pi-hole, Plex, or media servers                  |

---

## 🛠️ Technology & Tools Utilized

- **`VirtualBox:`**  
  Served as the primary hypervisor for hosting virtual machines locally in a controlled lab environment.

- **`Windows Server:`**  
  Deployed as the core infrastructure server for testing services such as Active Directory, DNS, or file sharing.

- **`Kali Linux:`**  
  Used as the attacker machine for penetration testing, vulnerability scanning, and offensive security simulations.

- **`Local Storage (50 GB):`**  
  Allocated for virtual machine disk images and snapshots, supporting test scenarios and system state preservation.

  ---

## 👣 Installing `VirtualBox`

### Step 1: Visit the Official VirtualBox Website: `https://www.virtualbox.org`

<img width="2543" height="583" alt="Lab 1" src="https://github.com/user-attachments/assets/c5b23e6d-2ed4-40e4-85d5-56c2233219da" />

---

### Step 2: Download the Windows Hosts Installer

<img width="1089" height="502" alt="Lab 2" src="https://github.com/user-attachments/assets/8a60e312-f2f4-4aea-a46e-947bb7e4f6a9" />

---

### Step 3: Run the Installer and Follow the Installation Wizard
1. **Custom Setup:** Next
2. **Warning: Network Interfaces:** Next
3. **Missing Dependencies:** Yes
4. **Ready to Install:** Install

*Note: The installation process takes a while, and you will lose internet connection during the process. Once complete, click **Finish** and VirtualBox will automatically open.*

<img width="802" height="472" alt="image" src="https://github.com/user-attachments/assets/9b35136c-d897-4a15-aac6-bd8c6609ccbc" />

---

## 👣 Installing `Windows 10` in VirtualBox

### Step 1: Download a Windows 10 ISO: `https://www.microsoft.com/en-us/software-download/windows10`

<img width="992" height="263" alt="Lab 6" src="https://github.com/user-attachments/assets/a45d311f-e6a3-4c92-b63a-5fa1918179a5" />

---

### Step 2: Run the Installer and Follow the Installation Wizard
1. **Applicable Notices and License Terms:** Accept
2. **Create Installation Media:** Next
3. **Select Language, Architecture, and Edition:** Use the recommended options → Next
4. **ISO File:** Next

*Note: Save the ISO file on your desktop or wherever you'd like.*

---

### Step 3: Open VirtualBox and Create a New VM

<img width="1277" height="727" alt="Lab 11" src="https://github.com/user-attachments/assets/eff2147d-5286-41c9-a6bf-4a25f0179c81" /></br>

- **Name:** Windows 10 (or whatever you'd like)
- **ISO Image:** C:\Users\User\Desktop\Windows.iso
- **Next**

<img width="794" height="457" alt="Lab 12" src="https://github.com/user-attachments/assets/97fc9e44-0f08-4e70-a75c-328d8d7ce946" /></br>

- **Base Memory:** 4096 MB
- **Processors:** 1 CPU  
- **Next**

<img width="794" height="454" alt="Lab 13" src="https://github.com/user-attachments/assets/e1f1804d-6ccc-46c9-90f1-9a0d0873e224" /></br>

- **Create a Virtual Hard Disk:** 50 GB
- **Next**

<img width="794" height="454" alt="Lab 14" src="https://github.com/user-attachments/assets/851bb072-5154-43b7-b9e4-db347e8c51e6" /></br>

- **Summary:** Finish

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

1. In the Downloads folder, right-click `kali-linux...`
2. Hover over 7-Zip
3. Extract to `kali-linux...`
4. Double-click the extracted folder
5. Double-click the `kali-linux...vbox` to import into VirtualBox

 <img width="641" height="230" alt="Lab 30" src="https://github.com/user-attachments/assets/8fb3ec55-15fd-4ce3-8ce9-f3512747504e" /></br>

*Note: If you can't see file extensions `.vbox`, click on view and check file name extensions.*

---

### Step 4: Start the Kali Linux VM

<img width="722" height="245" alt="Lab 31" src="https://github.com/user-attachments/assets/33d83883-343f-4f93-940a-d60d7be700ef" /></br>

*Note: The default credentials for Kali Linux are `Kali` for both username and password.*

*Optional: Change the default password in the terminal with the command `passwd`:*

<img width="348" height="212" alt="Lab 42" src="https://github.com/user-attachments/assets/98bcbd8a-19da-4bc7-a85e-35f1fbd37c01" />

---

<h1 = align=center>Congratulations on Creating a Virtual Home Lab</h1>

<img width="2127" height="857" alt="Lab 48" src="https://github.com/user-attachments/assets/c9f75fc8-5d13-461b-88f9-f216f4493077" />

## Key Takeaways

### Properly Configure Your Virtual Machines!

1. Ensure they have enough **resources**
2. Set up **networking** appropriately
3. Install **Guest Additions**
4. Take a clean **snapshot** for a baseline and before testing
5. Harden or weaken **security** based on test goals

---

*This project was designed to simulate a controlled virtual environment for cybersecurity testing and network analysis using Windows Server and Kali Linux virtual machines. The goal was to assess system vulnerabilities, practice ethical hacking techniques, and observe system behavior under various security conditions.*

**Created By:** `Briana Willis`  
**Date:** `2025-07-11`  
**Time:** `20:15 UTC`












