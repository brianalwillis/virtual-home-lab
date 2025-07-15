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

### Step 1: `Server 19` Virtual Machine Creation and Provisioning

The virtual machine, named `Domain-Controller`, was configured as a domain controller using the `Windows Server 2019 ISO`. It was provisioned with 2048 MB of RAM and 4 virtual CPUs to support `Active Directory` and core infrastructure services.

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

Before running the script to create all 1,000 users, I tested its functionality by manually inserting my name, `Briana Willis`, as the first entry in the `names.txt` file. After executing the PowerShell script, a total of 1,001 users were created in Active Directory, confirming that the script worked as intended. The test user account `bwillis` was successfully generated using the naming convention implemented in the script, verifying that both the account creation logic and OU assignment were functioning properly.

<img width="747" height="523" alt="Lab 94" src="https://github.com/user-attachments/assets/dc9c0eef-808a-4fa2-8463-572d78254a4c" /></br>

---
## 👣 STEP-BY-STEP: SETTING UP THE CLIENT

### Step 1: `Windows 10` Virtual Machine Creation and Provisioning

The virtual machine, named `Client1`, was created using the Windows 10 ISO and provisioned with 4096 MB of RAM and 4 virtual CPUs. Network Adapter 1 was enabled on the same internal network as our domain controller, `test 3`.

<img width="1131" height="471" alt="Lab 99" src="https://github.com/user-attachments/assets/8b8772d9-4a50-4efe-8d1a-dab122dda7c7" /></br>

---

### Step 2: `Windows Setup`

Powered on the virtual machine and proceeded through the Windows 10 installation process using the ISO image.

<img width="635" height="475" alt="Lab 20" src="https://github.com/user-attachments/assets/3ed47f26-c3dd-4559-8da0-4576b3284a63" /></br>

*Windows Server 10 Pro → Accept the license terms → Username: bwillis → Password: Password18*

---

### Step 3: Confirming `DHCP` Functionality

After setting up `Client1`, I logged in using the `bwillis` account with the default credentials for the first time. I then opened a command prompt and ran `ipconfig` to verify network settings. The Ethernet adapter showed the following configuration:

<img width="538" height="280" alt="Lab 100" src="https://github.com/user-attachments/assets/d3cf4e9c-3cd4-4d3e-8dc2-33f0abed07a9" /></br>

These values confirm that the `DHCP` server is functioning correctly and issuing addresses within the defined scope, along with proper DNS domain suffix assignment. To validate `DNS` resolution, I successfully pinged `www.google.com` to confirm external connectivity and pinged `mydomain.com` to verify internal name resolution to the domain controller.

<img width="512" height="279" alt="Lab 101" src="https://github.com/user-attachments/assets/3ac7403f-e9ba-423a-980c-084accce8573" /></br>

<img width="464" height="205" alt="Lab 102" src="https://github.com/user-attachments/assets/ddec1a42-9364-4307-bb56-cecdc9de6196" /></br>

---

### Step 4: Join `Client1` to the Domain

In `System Properties`, I changed the computer name to `Client1` and selected `Domain` under the `Member of` section. I entered `mydomain.com` as the domain name and was prompted to provide credentials. After authentication, the system was successfully added to the domain and prompted for a restart to apply the changes.

<img width="297" height="147" alt="Lab 106" src="https://github.com/user-attachments/assets/236cb17a-d5ba-48a0-bf7c-ba0c01c23d7b" /></br>

<img width="745" height="521" alt="Lab 108" src="https://github.com/user-attachments/assets/d500ba67-c71a-42ab-819c-9d9118eb63d2" /></br>

<img width="382" height="118" alt="Lab 109" src="https://github.com/user-attachments/assets/be222b97-9232-41c4-b88b-ef68f02f7142" /></br>

---

## HOW TO MANUALLY RESET A PASSWORD

To reset a user's password in `Active Directory`, press `Win + R`, type `dsa.msc`, and press Enter to open `Active Directory Users and Computers`. Locate the user account—in this case, `bwillis`—by browsing to the appropriate Organizational Unit. Right-click the user and select `Reset Password`.

<img width="512" height="509" alt="Lab 116" src="https://github.com/user-attachments/assets/6c6f078a-b4d0-4283-a918-3bc202cd1397" /></br>

Assign an easy-to-remember password `Password1`, check `User must change password at next logon`, and also check `Unlock the user’s account` if it was previously locked. This process restores access while enforcing a secure password update upon next login.

<img width="376" height="254" alt="Lab 117" src="https://github.com/user-attachments/assets/6c9c166a-fe9a-4a72-a582-b96636af8192" /></br>

<img width="315" height="148" alt="Lab 118" src="https://github.com/user-attachments/assets/1ac6a648-e034-4c68-b266-c009acd33517" /></br>

---

## HOW TO AUTOMATE PASSWORD RESETS

Password resets can also be automated using `PowerShell`, which is especially useful for bulk or remote management tasks. The following script resets the password for the user `bwillis`, enforces a password change at next logon, unlocks the account if it was locked, and ensures the account is enabled:

```powershell

# Reset password
Set-ADAccountPassword -Identity bwillis -Reset -NewPassword (ConvertTo-SecureString "Password1234567890!@" -AsPlainText -Force)

# Require password change at next logon
Set-ADUser -Identity bwillis -ChangePasswordAtLogon $true

# Unlock and enable the account
Unlock-ADAccount -Identity bwillis
Enable-ADAccount -Identity bwillis
```

---

## GROUP POLICY MANAGEMENT EDITOR

For the final test, I launched the `Group Policy Management` Console by pressing `Win + R`, typing `gpmc.msc`, and pressing Enter. This opened the `Group Policy Management Editor`, allowing me to explore how `Group Policy Objects` (GPOs) are created, linked to `Organizational Units` (OUs), and used to manage user and computer configurations across the domain.

<img width="804" height="319" alt="Lab 122" src="https://github.com/user-attachments/assets/f171a8c0-67c2-4cdc-9792-102cbd65831b" /></br>

Within the `Group Policy Management Editor`, I navigated to `Computer Configuration` > `Policies` > `Windows Settings` > `Security Settings` > `Account Policies` > `Password Policy` to enforce stricter password requirements across the domain.

<img width="804" height="319" alt="Lab 122" src="https://github.com/user-attachments/assets/68ff421b-cdaf-461d-9426-92568e8ef5eb" /></br>

<img width="802" height="318" alt="Lab 123" src="https://github.com/user-attachments/assets/0a040ab2-f4cc-40ff-9981-a5c5d72e53ef" /></br>

To enable auditing for user activity, I configured `audit policies` to track logon events, logoffs, and account lockouts. These settings allow security teams to monitor authentication activity and detect potential unauthorized access attempts, account misuse, or lockout patterns across the domain.

<img width="803" height="592" alt="Lab 127" src="https://github.com/user-attachments/assets/8ca1e105-1c55-451e-b869-a5d740ab74a8" /></br>

These audits can be analyzed in `Event Viewer` (`Win + R` > `eventvwr.msc`) under `Windows Logs` > `Security`.

<img width="1156" height="595" alt="Lab 132" src="https://github.com/user-attachments/assets/0e675f68-a347-40b9-a058-6251d1ee5677" /></br>

| Task Category   | Event ID | Description                                                |
|:----------------|:---------|:-----------------------------------------------------------|
| Logon           | 4624     | Successful user logon                                      |
| Logoff          | 4634     | User logoff                                                |
| Logon Failure   | 4625     | Failed user logon attempt                                  |
| Account Lockout | 4740     | A user account was locked out due to failed login attempts |
| Special Logon   | 4672     | Logon with special privileges (e.g., admin rights)         |

---

*This project simulates a realistic enterprise network environment to practice and demonstrate core cybersecurity and IT infrastructure skills. It involves setting up a virtualized lab with a Windows Server 2019 domain controller, Active Directory, DHCP, and client machines, allowing hands-on experience with domain management, user provisioning, network configuration, and security policy enforcement..*

**Created By:** `Briana Willis`  
**Date:** `2025-07-15`  
**Time:** `15:42 UTC`
