<h1 = align=center>HOME LAB - ACTIVE DIRECTORY</h1>
<h2 = align=center>Bulk User Creation with PowerShell </h2>

<p align="center">
<img width="1342" height="883" alt="Untitled Diagram drawio (3)" src="https://github.com/user-attachments/assets/978f6667-84a3-403e-b02b-9328f6341827" />
</p>

---

## 🛠️ TECHNOLOGY & TOOLS UTILIZED

- **`VirtualBox:`**  
  Used as the primary virtualization platform to host multiple virtual machines in an isolated local environment for cybersecurity testing and infrastructure simulation.

- **`Windows Server 2019:`**  
  Deployed as the domain controller within the lab. Configured to run Active Directory Domain Services (AD DS), DNS, and Group Policy to emulate enterprise-level identity and access management scenarios.

- **`Windows 10:`**  
  Installed as a domain-joined workstation to simulate a typical enterprise endpoint. Used for user behavior simulation, GPO testing, and endpoint visibility through logging tools.

- **`Active Directory:`**  
  Implemented to manage user accounts, groups, and organizational units (OUs). Used for hands-on experience with authentication flows, access control, privilege escalation testing, and administrative scripting.

- **`PowerShell:`**  
  Used for automating administrative tasks such as creating users, managing AD objects, and configuring system settings within both the server and client machines.
  
- **`Group Policy Management:`**  
  Applied GPOs to enforce password policies, audit policies, restrict user privileges, and configure security baselines across the domain environment.

---

## OBJECTIVE

Designed and deployed a virtualized Windows domain lab using `VirtualBox`, `Windows Server 2019`, and `Windows 10` to gain hands-on experience with enterprise network infrastructure and identity management. The project focused on configuring `Active Directory`, `Group Policy`, and domain-joined `endpoints` to simulate real-world authentication, access control, and administrative workflows. This lab environment served as a foundation for practicing common security tasks, including privilege escalation prevention, user access auditing, and scripting automation with `PowerShell`.

## 👣 STEP-BY-STEP: SETTING UP THE DOMAIN CONTROLLER

### Step 1: `Virtual Machine` Creation and Provisioning

The virtual machine, named `Domain-Controller`, was configured as a domain controller using the `Windows Server 2019 ISO`. It was provisioned with 2 GB of RAM and 4 virtual CPUs to support `Active Directory` and core infrastructure services.

<img width="755" height="580" alt="Lab 1" src="https://github.com/user-attachments/assets/e081d054-9449-483e-a0cf-f4a4de7ce8d5" /></br>

---

### Step 2: Configure `Network Adapters`

For networking, `Network Adapter 1` was enabled and attached to `NAT` to allow internet access. `Network Adapter 2` was connected to an `internal network` named `Test 3` to facilitate isolated communication between lab machines without external exposure.

<img width="1131" height="471" alt="Lab 4" src="https://github.com/user-attachments/assets/c379a872-b1dc-4bb6-880b-a0917fe99f13" /></br>

<img width="1134" height="472" alt="Lab 5" src="https://github.com/user-attachments/assets/06246298-cf3c-4f36-b51d-e89544dc861c" /></br>

---

### Step 3: `Windows Setup`

Powered on the virtual machine and proceeded through the Windows Server 2019 installation process using the ISO image.

<img width="636" height="476" alt="Lab 6" src="https://github.com/user-attachments/assets/31f0efb0-f514-40d9-8987-d7ba2b00bff5" /></br>

*Windows Server 2019 Standard Evaluation (Desktop Experience) → Accept the license terms → Username: Administrator → Password: Password18*

---

### Step 4: Check `Network Configuration`

Checked the `network connection details` of the virtual machine and observed it was automatically assigned an IPv4 address of `169.254.120.207`, indicating an `APIPA` (Automatic Private IP Addressing) address.

<img width="357" height="434" alt="Lab 9" src="https://github.com/user-attachments/assets/45c3d59a-f363-406e-b31b-a33ed6a64961" /></br>

Under `Network Connections`, we renamed the NAT adapter to `Internet` and the internal network adapter to `Internal_Network` for better clarity. The `Internet_Network` adapter was then manually configured with the following static IP settings:  
- **IP address:** `172.16.0.1`  
- **Subnet mask:** `255.255.255.0`  
- **Preferred DNS server:** `127.0.0.1`

<img width="782" height="159" alt="Lab 10" src="https://github.com/user-attachments/assets/2804da41-c4c7-45be-9c22-80c003b31bb3" /></br>

<img width="755" height="455" alt="Lab 11" src="https://github.com/user-attachments/assets/b898dda0-d4af-41cb-9547-9c77c69ce378" /></br>

---

### Step 5: Set Up `Active Directory`

In `Server Manager`, we began by launching the `Add Roles and Features` Wizard to install `Active Directory Domain Services` (AD DS). During the setup, we also included `Group Policy Management` and `Remote Server Administration Tools` (RSAT) to enable centralized domain control and administrative functionality.

<img width="1001" height="741" alt="Lab 12" src="https://github.com/user-attachments/assets/c5771a04-7c98-4775-b2da-d8c923f4b627" /></br>

<img width="783" height="556" alt="Lab 22" src="https://github.com/user-attachments/assets/009e3290-608c-4122-8e58-9fac3755b499" /></br>

After completing the role installation, we proceeded with the `post-deployment configuration` by promoting the server to a domain controller. During the configuration, we created a new forest with the root domain name `mydomain.com`, and enabled both the `Domain Name System` (DNS) server and `Global Catalog` (GC) options. We also set the NetBIOS domain name to `MYDOMAIN`.

<img width="1227" height="764" alt="Lab 31" src="https://github.com/user-attachments/assets/ba1b4759-d514-4bc1-9d9b-f6541081624d" /></br>

---

### Step 6: Set up `Domain Admins` and `Domain Users`

After logging back into the server, we navigated to `Active Directory Users and Computers` to begin configuring domain objects. We created a new `Organizational Unit` (OU) named `_ADMINS`, and within that OU, added a new user account with the full name `Briana Willis` and the user logon name `a-bwillis`.

<img width="433" height="374" alt="Lab 40" src="https://github.com/user-attachments/assets/051ed52a-ed78-447a-93a8-6a89ad11aa60" /></br>

Within `Briana Willis’` account properties in `Active Directory Users and Computers`, we navigated to the `Member Of` tab and added the user to the `Domain Admins` group. This granted her administrative privileges across the domain. 

<img width="1225" height="763" alt="Lab 45" src="https://github.com/user-attachments/assets/b9c074da-91da-4683-9aa3-637794e44dcc" /></br>

---

### Step 7: Set up `Remote Access` Services

In `Server Manager`, we returned to `Add Roles and Features` to install the `Remote Access role`. During the setup, we selected the role services `DirectAccess and VPN` (RAS) as well as `Routing` to enable secure remote connectivity and traffic management for the network.

<img width="781" height="555" alt="Lab 49" src="https://github.com/user-attachments/assets/9f3e9a0b-ac0a-4e73-baa5-1f18c2166a33" /></br>

Next, we navigated to `Tools` > `Routing and Remote Access` and launched the Routing and Remote Access Server Setup Wizard. We proceeded to configure `NAT` by selecting our internet-facing network interface, named `Internet`, to provide network address translation for internal clients. Upon successful configuration, the domain controller (local server) displayed a green status arrow, indicating the service was running properly.

<img width="616" height="437" alt="Lab 58" src="https://github.com/user-attachments/assets/2743e64b-b68c-41e4-b333-be1a7b70fd47" /></br>

---

### Step 8: Set up `DHCP Server`

Back in `Server Manager`, we launched the `Add Roles and Features` Wizard again to install the `DHCP Server` role, enabling the server to assign IP addresses dynamically within the network.

<img width="779" height="554" alt="Lab 61" src="https://github.com/user-attachments/assets/2ba6c860-10d4-4a5e-b1cf-945f01291840" /></br>

We navigated to `Tools` > `DHCP` and launched the `New Scope Wizard` to configure a DHCP scope. We named the scope `172.16.0.100-200` and set the IP address range from `172.16.0.100` to `172.16.0.200` with a subnet mask of `255.255.255.0` (prefix length 24). The router (default gateway) was set to `172.16.0.1`, and the parent domain was specified as `mydomain.com`. After activating, authorizing, and refreshing the DHCP server, its status displayed a green icon indicating it was functioning properly.

<img width="167" height="172" alt="Lab 77" src="https://github.com/user-attachments/assets/cbfe1307-c73c-4d5b-9284-b3705fd0899e" /></br>

<img width="271" height="378" alt="Lab 78" src="https://github.com/user-attachments/assets/f484b260-c072-473e-9c35-a2888a5f4902" /></br>

---

### Step 9: Bulk User Creation with `PowerShell` in `Active Directory`

To efficiently add 1,000+ user accounts to `Active Directory`, we used a `PowerShell` script in combination with a text file containing first and last names. The script created a new organizational unit called `_USERS` and then processed each name to generate a standardized username consisting of the user’s first initial and last name in lowercase. Each user was created with a default password `Password18` and placed within the _USERS OU. This automated method significantly streamlined bulk user provisioning, reducing manual effort and ensuring consistent account configuration across the domain.

**Script:**
```powershell
$PASSWORD_FOR_USERS   = "Password18" 
$USER_FIRST_LAST_LIST = Get-Content .\names.txt
# ------------------------------------------------------ #

$password = ConvertTo-SecureString $PASSWORD_FOR_USERS -AsPlainText -Force
New-ADOrganizationalUnit -Name _USERS -ProtectedFromAccidentalDeletion $false

foreach ($n in $USER_FIRST_LAST_LIST) {
    $first = $n.Split(" ")[0].ToLower()
    $last = $n.Split(" ")[1].ToLower()
    $username = "$($first.Substring(0,1))$($last)".ToLower()
    Write-Host "Creating user: $($username)" -BackgroundColor Black -ForegroundColor Cyan
    
    New-AdUser -AccountPassword $password `
               -GivenName $first `
               -Surname $last `
               -DisplayName $username `
               -Name $username `
               -EmployeeID $username `
               -PasswordNeverExpires $true `
               -Path "ou=_USERS,$(([ADSI]`"").distinguishedName)" `
               -Enabled $true
}
```
**Results:**

<img width="748" height="525" alt="Lab 89" src="https://github.com/user-attachments/assets/72a92db7-4552-406a-b0ef-cbb1315af366" /></br>

Before running the script to create all 1,000 users, I tested its functionality by manually inserting my name `Briana Willis` as the first entry in the `names.txt` file. After executing the PowerShell script, a total of 1,001 users were created in Active Directory, confirming that the script worked as intended. The test user account `bwillis` was successfully generated using the naming convention implemented in the script, verifying that both the account creation logic and OU assignment were functioning properly.

<img width="747" height="523" alt="Lab 94" src="https://github.com/user-attachments/assets/dc9c0eef-808a-4fa2-8463-572d78254a4c" />

---

### Windows Defender and Updates

Turning on `Windows Security` features—such as real-time antivirus protection, ransomware protection, and exploit mitigation—adds additional layers of defense. Ensuring that `Windows Updates` are enabled and set to install automatically helps keep the system protected against newly discovered threats and vulnerabilities. Additionally, keeping all operating system components and third-party applications updated with the latest security patches is essential.

<img width="792" height="581" alt="security" src="https://github.com/user-attachments/assets/3f71b339-ec5a-42c9-a779-15fa9e92a3fc" /></br>

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/ead80d00-87fc-47e1-bafe-40d60fee587e" /></br>

---

### `139/tcp` NetBIOS Session Service

<img width="1160" height="630" alt="Lab 237" src="https://github.com/user-attachments/assets/d7913fb4-5876-4c57-ab32-3d4ad3acc839" /></br>

Control Panel → Network and Internet → Network Connections → Properties → Internet Protocol Version 4 → Properties → Advanced → WINS → Disable NetBIOS over TCP/IP

<img width="861" height="587" alt="Lab 238" src="https://github.com/user-attachments/assets/13ffafba-9a1a-485c-8c9d-8f1d4a2b3440" /></br>

Services → TCP/IP NetBIOS Helper → Properties → Startup Type: Disabled → Service Status: Stop

---

### `445/tcp` Microsoft-DS (SMB over TCP)

<img width="740" height="632" alt="Lab 236" src="https://github.com/user-attachments/assets/0f8305c6-4150-4743-9051-d58352786298" /></br>

Control Panel → Programs → Programs and Features → Disable SMB 1.0/CIFS File Sharing Support

---

### `3389/tcp` Remote Desktop Protocol (RDP)

<img width="795" height="630" alt="Lab 231" src="https://github.com/user-attachments/assets/e719e705-143b-45a5-a0d9-8dcd8b408a57" /></br>

Settings → System → Remote Desktop → Off

<img width="407" height="463" alt="Lab 235" src="https://github.com/user-attachments/assets/1efcf22c-aab2-4888-a27c-9577ce1aefaa" /></br>

Win + R → sysdm.cpl → Remote → Remote Desktop → Don't Allow Remote Connections

---

### All Unnecessary and Vulnerable Ports are Closed

<img width="605" height="229" alt="Lab 239" src="https://github.com/user-attachments/assets/b2a472bc-f93d-4f7e-8fa5-a919daef666d" />

---

*This project simulates a real-world attack scenario in a controlled virtual lab environment to demonstrate how a malicious payload can be delivered, executed, and monitored using offensive security tools. Its purpose is to analyze attacker behavior, assess system vulnerabilities, and explore defensive measures using tools like Splunk and Sysmon.*

**Created By:** `Briana Willis`  
**Date:** `2025-07-13`  
**Time:** `17:50 UTC`
