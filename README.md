# Active Directory Home Lab

This project presents a simple Active Directory lab environment built using virtual machines.  
The lab simulates a small company infrastructure with centralized user management, file sharing and Group Policy configuration.

---

## Environment

Virtualization platform: VirtualBox

### Server

- DC1 - Windows Server 2022  
  Roles:
  - Active Directory Domain Services
  - DNS Server
  - File Server

### Client

- DESKTOP01 - Windows 11  
  Domain-joined workstation

### Domain

- company.com

---

## Final Configuration

### Active Directory

Organizational Units:

- HR
- IT
- Sales
- Groups

Users:

- anna.nowak (HR)
- michal.kowalczyk (IT)
- jan.kowalski (Sales)

Security Groups:

- HR_Users
- IT_Users
- Sales_Users

Users are assigned to groups based on department.

---

### File Shares

Shared path:
\\DC1\Shares

Folders:

- HR
- IT
- Sales
- Public

---

### Permissions

Access is controlled using security groups:

- HR -> HR_Users
- IT -> IT_Users
- Sales -> Sales_Users
- Public -> Domain Users

Each department has access only to its own folder.

---

### Group Policy

Configured GPOs:

1. Drive mapping  
   H: -> \\DC1\Shares\HR

2. Control Panel restriction  
   Prevents users from accessing system settings

---

### Verification

- users can access only their department folder
- all users can access Public folder
- access to other folders is denied
- network drive is mapped automatically
- Control Panel is blocked

---

## Implementation Steps

<details>
<summary>Click to expand full configuration process</summary>

### 1. Active Directory setup

![AD structure](screenshots/aduc.png)

_Active Directory Users and Computers console with domain structure._

---

### 2. Organizational Units

![OU structure](screenshots/ou-structure.png)

_Creation of Organizational Units for HR, IT and Sales._

---

### 3. Users

![Users](screenshots/users-created.png)

_Creation of domain users in respective departments. In this example Michal Kowalczyk is user of IT department._

---

### 4. Security Groups

![Groups](screenshots/creating-groups.png)

_Creation of security groups for each department._

![All groups created](screenshots/security-groups-created.png)

_All security groups._

![Add user to group](screenshots/adding-user-to-a-group.png)

_Assigning users to appropriate security groups. In this example, Anna Nowak is being assigned to HR Users group._

---

### 5. DNS Configuration

![DNS](screenshots/dns-zone.png)

_DNS zone configured for domain name resolution._

---

### 6. Client joined to domain

![Client domain](screenshots/client-domain.png)

_Client machine successfully joined to the domain._

---

### 7. File Shares

![Folders](screenshots/share-folders.png)

_Creation of shared folders for departments._

![Share config](screenshots/share-config.png)

_Shares folder published in the network._

---

### 8. NTFS Permissions

![Inheritance disabled](screenshots/disabling-inheritance-for-a-folder.png)

_Disabling inheritance to configure custom permissions._

![HR permissions](screenshots/ntfs-permissions-for-hr.png)

_Permissions assigned to HR group._

![Public permissions](screenshots/ntfs-permissions-for-a-public-folder.png)

_Public folder accessible to all domain users._

---

### 9. Group Policy ? Drive Mapping

![Drive mapping](screenshots/gpo-drive-map.png)

_GPO mapping network drive H: to department share._

![Drive mapped](screenshots/gpo-drive-mapped.png)

_Drive mapping GPO configured._

---

### 10. Group Policy ? Control Panel restriction

![Control panel blocked](screenshots/control-panel-blocked.png)

_GPO restricting access to Control Panel._

![Control panel blocked](screenshots/control-panel-gpo-settings.png)

_Control Panel GPO configured._

---

### 11. Verification

![Log in](screenshots/login-as-hr-user.png)

_Logging in as an HR user._

![Mapped drive](screenshots/mapped-drive-seen-by-hr-user.png)

_Network drive automatically mapped after login._

![Shares folder](screenshots/shared-folders-seen-by-an-hr-user.png)

_Shared folders seen by an HR user._

![Shared folders](screenshots/subfolders-of-shares-folder.png)

_Subfolders of "Shares" folder seen by an HR user._

![HR folder](screenshots/succesfully-opened-hr-folder.png)

_Succesfully opened folder for the HR department._

![Access denied](screenshots/access-denied-for-an-it-folder.png)

_User denied access to unauthorized folder._

![Client test](screenshots/control-panel-access-denied.png)

_User denied access to control panel._

</details>

## Summary

This lab demonstrates:

- Active Directory configuration
- user and group management
- NTFS permissions
- SMB file sharing
- Group Policy management
