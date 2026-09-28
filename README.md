
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Network File Share & Permissions Lab</h1>

In this tutorial, I built a simulated file-sharing environment using <b>Windows Server</b>, <b>Active Directory</b>, <b>PowerShell</b>, <b>SMB</b>, <b>NTFS permissions</b>, <b>OUs</b>, and <b>security groups</b>. I also manually created 3 users, automated 47 extra users with <b>PowerShell</b>, configured departmental access, investigated an access failure, and verified the resolution.

#### <h2>Environments & Technologies Used:</h2>
- <b>Microsoft Azure</b>
- <b>Windows Server</b>
- <b>Active Directory Domain Services (AD DS)</b>
- <b>Active Directory Users and Computers (ADUC)</b>
- <b>PowerShell</b>
- <b>Organizational Units (OUs)</b>
- <b>Active Directory Security Groups</b>
- <b>Server Message Block (SMB)</b>
- <b>NTFS Permissions</b>
- <b>Windows Network Shares</b>
- <b>UNC Paths</b>

#### <h2>Operating Systems Used:</h2>
- <b>Windows Server</b> — domain controller and file server
- <b>Windows 11</b> — domain-joined client workstation

#### <h2>High-Level Deployment & Configuration:</h2>
1. Deploy and configure <b>Windows Server</b> and <b>Windows 11</b> virtual machines.
2. Install and configure <b>Active Directory Domain Services (AD DS)</b> and <b>DNS</b> on <b>Windows Server</b>.
3. Join the <b>Windows 11</b> client to the <b>Active Directory</b> domain.
4. Create departmental <b>OUs</b> and <b>security groups</b> for IT, Finance, and HR.
5. Create three users manually and use <b>PowerShell</b> to provision the remaining 47 users.
6. Create departmental network shares and configure <b>SMB</b> and <b>NTFS permissions</b>.
7. Test user access from the <b>Windows 11</b> client, including a deliberately misconfigured account.
8. Troubleshoot, correct, verify, and document the access-control issue and final configuration.

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="[write-image-description-here]"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="[write-image-description-here]"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="[write-image-description-here]"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
