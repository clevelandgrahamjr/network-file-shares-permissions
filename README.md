
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

# Network File Share & Permissions Lab

I built a small business-style file-sharing environment using **Windows Server, Windows 11, Active Directory, PowerShell, Windows Firewall, security groups, and network file sharing**. I created users, assigned access, introduced a permissions problem, diagnosed the cause, and verified the fix.

## Environments & Technologies Used

- Microsoft Azure
- Azure Virtual Machines
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- DNS
- PowerShell
- Windows Defender Firewall
- Server Message Block (SMB)
- NTFS permissions
- Active Directory security groups
- Remote Desktop Protocol (RDP)
- File Explorer

## Operating Systems Used

- **Windows Server** — domain controller and file server
- **Windows 11** — domain-connected client workstation

## High-Level Deployment & Configuration

1. **Deployed Windows Server and Windows 11 VMs** in Microsoft Azure.

2. **Installed Active Directory Domain Services (AD DS) and DNS** after temporarily disabling the server firewall for setup and testing.

3. **Created three admin accounts manually and joined the Windows 11 client to `arxcorp.com`.**

4. **Used PowerShell to create 47 employee accounts and three departmental security groups.**

5. **Re-enabled the server firewall and configured network file sharing and permissions.**

6. **Confirmed successful non-admin access, then deliberately created a permissions issue.**

7. **Tested the problem with two users and used PowerShell to narrow down the cause.**

8. **Corrected the group permissions and verified that file access was restored.**


# Deployment and Configuration Steps

## 1. Deploy Windows Server and Windows 11 VMs

**Method:** Deployed one Windows Server VM and one Windows 11 client VM in Microsoft Azure.

**Reason:** Created a simple server-and-client environment for testing Active Directory, user accounts, and file sharing.

**Navigation:**  
`Azure Portal → Virtual Machines → Create → Configure → Review + Create`

### Image 01 — Azure Server and Client VMs

<!-- Drag and drop image here -->
<!-- Source: 1-azure-client-server-vms(1).png -->

<img width="1557" height="255" alt="1-azure-client-server-vms" src="https://github.com/user-attachments/assets/2a6c5697-82c4-4708-9591-671b027abb27" />


## 2. Install and Configure Active Directory and DNS

**Method:** Temporarily disabled the Windows Server firewall, installed **Active Directory Domain Services (AD DS)** and DNS, promoted the server to a domain controller, and created the `arxcorp.com` domain.

**Reason:** Disabling the firewall during initial setup reduced possible connection issues while the domain was being configured.

**Navigation:**  
`Server Manager → Add Roles and Features → Active Directory Domain Services → Promote this server to a domain controller`

### Image 02 — Active Directory and Domain Verification

<!-- Drag and drop image here -->
<!-- Source: 2-ad-ds-dns-installed-verified-powershell(1).PNG -->

<img width="1920" height="1080" alt="2-ad-ds-dns-installed-verified-powershell" src="https://github.com/user-attachments/assets/a9f25588-1856-4c85-91ca-412d50557bb8" />


## 3. Create Administrator Accounts and Join the Client

**Method:** Manually created **Bruce Wayne, Clark Kent, and Diana Prince**, placed them in the `_ADMINS` Organizational Unit (OU), added them to **Domain Admins**, and joined the Windows 11 client to `arxcorp.com`.

**Reason:** Demonstrated manual user administration before moving to automated account creation.

**Navigation:**  
`ADUC → arxcorp.com → _ADMINS → New → User`  
`ADUC → Users → Domain Admins → Properties → Members`  
`Windows 11 → System → Domain or workgroup → Change`

### Image 03 — Administrator Accounts and Domain Admin Membership

<!-- Drag and drop image here -->
<!-- Source: 3a-ad-admin-manual-users.PNG -->

<img width="1663" height="631" alt="3a-ad-admin-manual-users" src="https://github.com/user-attachments/assets/94956f2d-2377-4a00-927b-e82ee0b78ac7" />

### Image 04 — Windows 11 Joined to `arxcorp.com`

<!-- Drag and drop image here -->
<!-- Source: 3b-arxcorp-domain-welcome.png -->

<img width="1920" height="1080" alt="3b-arxcorp-domain-welcome" src="https://github.com/user-attachments/assets/47a4d13e-f88b-4a31-b72c-922f78e9ce0d" />


## 4. Automate Employee and Security-Group Creation

**Method:** I used an **AI-assisted PowerShell script, which I personally guided and thoroughly reviewed multiple times, then adapted for this lab** to create 47 employee accounts and the `IT-Users`, `Finance-Users`, and `HR-Users` security groups.

> **PowerShell source:** [View the user-provisioning script](https://github.com/clevelandgrahamjr/clevelandgrahamjr/blob/main/scripts/create-users.ps1)

**Reason:** Automated a repetitive task while keeping account creation and group assignments consistent.

**Navigation:**  
`PowerShell ISE / PowerShell → Review script → Run as administrator → Verify results`

### Image 05 — PowerShell User Provisioning Results

<!-- Drag and drop image here -->
<!-- Source: 4-users-aduc-auto-generated-powershell.PNG -->

<img width="864" height="1072" alt="4-users-aduc-auto-generated-powershell" src="https://github.com/user-attachments/assets/b5115f27-c2ab-4d7b-bea9-607c0eab059c" />


## 5. Re-enable the Firewall and Configure File Sharing

**Method:** Re-enabled Windows Firewall, enabled the required Active Directory, file-sharing, and Remote Desktop rules, then created a Finance network share for the `Finance-Users` group.

**Reason:** Restored normal security before continuing the file-sharing portion of the lab.

**Navigation:**  
`PowerShell (Administrator) → Firewall commands`  
`Windows Server → File Explorer → Folder Properties → Sharing → Permissions`

### Image 06 — Windows Firewall Re-enabled

<!-- Drag and drop image here -->
<!-- Source: 5a-server-vm-firewall-reenabled-powershell.PNG -->

<img width="1138" height="664" alt="5a-server-vm-firewall-reenabled-powershell" src="https://github.com/user-attachments/assets/62d27ce8-6c90-4367-af9c-eda3fd704a59" />


### Image 07 — Finance Share Permissions

<!-- Drag and drop image here -->
<!-- Source: 5c-server-vm-file-sharing-permissions-configured.PNG -->

<img width="1251" height="689" alt="5c-server-vm-file-sharing-permissions-configured" src="https://github.com/user-attachments/assets/9cecd82a-b4ff-481f-b748-d0f737cf1ed8" />


## 6. Confirm Access and Create a Test Failure

**Method:** Logged into the Windows 11 client as **John Stewart (`jstewart`)**, confirmed successful access to the Finance share, then deliberately reduced the Finance group's folder permissions on the server.

**Reason:** Confirmed the setup worked before creating a controlled problem for troubleshooting.

**Navigation:**  
`Windows 11 → Sign in as domain user → File Explorer → Finance share`  
`Windows Server → Folder Properties → Security → Finance-Users`

### Image 08 — Successful Finance Share Access

<!-- Drag and drop image here -->
<!-- Source: 6a-client-vm-access-jstewart-file-shares-confirmed.png -->

<img width="1920" height="1080" alt="6a-client-vm-access-jstewart-file-shares-confirmed" src="https://github.com/user-attachments/assets/156b982f-cd41-4eb4-a7c1-5659eeaa02c7" />


### Image 09 — Deliberate Permission Error

<!-- Drag and drop image here -->
<!-- Source: 6b-server-vm-misconfiguration-introduced.png -->

<img width="510" height="623" alt="6b-server-vm-misconfiguration-introduced" src="https://github.com/user-attachments/assets/d611849f-3441-4ed8-ad8a-dea7fff74356" />


## 7. Diagnose the Access Problem

**Method:** Tested the issue as **John Stewart (`jstewart`)** and **Jennifer Brooks (`jbrooks`)**. Used PowerShell commands such as `whoami`, `hostname`, and `Test-Path`, along with File Explorer, to compare what each user could reach.

**Reason:** Confirmed that the server and share were reachable, helping narrow the problem to permissions rather than basic network connectivity.

**Navigation:**  
`Windows 11 → Sign in as test user → PowerShell → File Explorer → Network share`

### Image 10 — John Stewart Access Test

<!-- Drag and drop image here -->
<!-- Source: 7a-client-vm-nw-share-void-jstewart-verified-powershell.png -->

<img width="1920" height="1080" alt="7a-client-vm-nw-share-void-jstewart-verified-powershell" src="https://github.com/user-attachments/assets/87c78309-4b32-4d21-a8b5-d75063b3b000" />


### Image 11 — Jennifer Brooks Access Test

<!-- Drag and drop image here -->
<!-- Source: 7b-client-vm-nw-share-void-j-brooks-verified.png -->

<img width="1920" height="1080" alt="7b-client-vm-nw-share-void-j-brooks-verified" src="https://github.com/user-attachments/assets/d21b3582-fa41-4163-b33f-345d45f040bb" />


## 8. Restore Permissions and Verify the Fix

**Method:** Restored the required permissions for the `Finance-Users` group on the Windows Server, then retested access from the Windows 11 client.

**Reason:** Correcting the group permission fixed the issue for the affected users without changing permissions one user at a time.

**Navigation:**  
`Windows Server → Folder Properties → Security → Finance-Users → Edit`  
`Windows 11 → PowerShell / File Explorer → Finance share`

### Image 12 — Finance Group Permissions Restored

<!-- Drag and drop image here -->
<!-- Source: 8a-server-vm-group-permissions-restored.png -->

<img width="525" height="600" alt="8a-server-vm-group-permissions-restored" src="https://github.com/user-attachments/assets/868769b9-d5af-48f4-868a-9208796194cc" />


### Image 13 — Successful Access After the Fix

<!-- Drag and drop image here -->
<!-- Source: 8b-client-vm-nw-share-restored-jstewart-verified.png -->

<img width="1920" height="1080" alt="8b-client-vm-nw-share-restored-jstewart-verified" src="https://github.com/user-attachments/assets/7e18a976-c651-43f8-831d-331ea98ca393" />



## Result

Successfully built and tested a Windows domain and file-sharing environment, created users manually and with PowerShell, configured group-based access, introduced and diagnosed a permissions failure, and restored access through the correct security-group settings.
