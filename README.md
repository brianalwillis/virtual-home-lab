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

## 👣 Step-by-Step Guide

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







