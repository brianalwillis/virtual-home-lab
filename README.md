<h1 = align=center>Creating a Virtual Home Lab</h1>

<img width="1162" height="902" alt="Untitled Diagram drawio (7)" src="https://github.com/user-attachments/assets/d91ce5c4-678e-4d14-8f5d-c7ecc6e1bca9" />

## 🏡 What is a Home Lab?
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

## 🛠️ TECHNOLOGY & TOOLS UTILIZED

- **`VirtualBox:`**  
  Served as the primary hypervisor for hosting virtual machines locally in a controlled lab environment.

- **`Windows Server:`**  
  Deployed as the core infrastructure server for testing services such as Active Directory, DNS, or file sharing.

- **`Kali Linux:`**  
  Used as the attacker machine for penetration testing, vulnerability scanning, and offensive security simulations.

- **`Local Storage (50 GB):`**  
  Allocated for virtual machine disk images and snapshots, supporting test scenarios and system state preservation.

  ---
