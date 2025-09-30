# Windows Server Project 

This project demonstrates a complete **Windows Server 2019 setup** for an enterprise environment, including domain services, user management, security policies, and automated deployments.  

---

## 📌 Summary
This Windows Server project implements key services such as:
- **Active Directory Domain Services (AD DS)** for centralized domain management.
- **Network Sharing with Roaming Profiles** for user mobility.
- **File Server Resource Manager (FSRM)** for quotas and file restrictions.
- **Infrastructure Services**: DHCP, DNS, and WDS.
- **Remote Desktop (RDP)** for remote access.
- **Group Policies (GPOs)** for system-wide restrictions and configurations.
- **Drive Mapping & Logon Restrictions** for controlled access.

Author: **Mahmoud Ahmed Elsawah**  

---

## 🧑‍💻 Domain Users and Organizational Units
- Each domain user has a **dedicated home directory** with mapped drives.
- Example: `Alice` has a personal shared folder with controlled NTFS permissions.
- Users access their home directories through assigned mapped drives.

---

## 📂 Storage Quotas and File Restrictions (FSRM)
| Organizational Unit | Quota Limit | File Restrictions |
|---------------------|-------------|-------------------|
| HR                  | 2 GB        | MP4 files not allowed |
| Graphics            | 10 GB       | No restrictions |
| IT                  | 5 GB        | MP4 files not allowed |
| Sales               | 4 GB        | No restrictions |

- HR and IT OUs cannot upload video files.  
- Quotas applied via **custom FSRM templates**.

---

## ⏰ Logon Restrictions
- **Non-IT users**:
  - Can log on only from one assigned PC.
  - Logon hours: **8:00 AM – 4:00 PM (Sunday–Thursday)**.
- **IT users**:
  - Can log on from any PC.
  - No time restrictions.

---

## 🖥️ Group Policies (GPO)
- Standard desktop background for all domain PCs.
- **USB & Phone Access**:
  - Only IT users can use USB drives and transfer files.
  - All other users blocked from removable storage.
- **Phone Restrictions**:
  - Deny read/write access to WPD devices.
- **System Restrictions**:
  - Non-IT users cannot access Task Manager, Control Panel, or change passwords.

---

## 📦 Software Deployment
- Google Chrome is automatically installed on all domain PCs via **GPO software deployment**.

---

## 🌐 DHCP & DNS
- Configured **DHCP scope** for client IP assignment.
- DNS configured for name resolution within the domain.

---

## 🔑 Password Policy
- Passwords must:
  - Change every **60 days**.
  - Be at least **6 characters** long.
  - Contain complexity (uppercase, lowercase, number, symbol).
  - Remember the **last 3 passwords**.

---

## 🔒 Remote Desktop Configuration
- Enabled on server and client PCs.
- Configured via GPO:
  - Allow remote connections.
  - Disable user authentication requirement.
- **Firewall rules** added for RDP.
- Tested remote connection to `192.168.200.6 (PC-01)`.

---

## 👤 Roaming Profiles
- Created a **hidden shared folder (`$`)**.
- Profile path set in user properties.
- Users (e.g., Alice) can log in from any PC and keep the same environment.

---

## 💿 Windows Deployment Services (WDS)
- Installed and configured **AD DS, DHCP, DNS, and WDS**.
- WDS Image Store hosted on **NTFS** volume.
- Added:
  - `install.wim` under **Install Images**.
  - `boot.wim` under **Boot Images**.
- Clients boot via **PXE** for automated OS installation.

---
