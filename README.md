# Hybrid Enterprise Windows Server & Azure AD Infrastructure Lab

## 📌 Project Overview
This advanced lab demonstrates the end-to-end deployment of a resilient, multi-server enterprise Windows Server environment virtualized within Microsoft Hyper-V. The objective was to design, implement, secure, and manage an infrastructure featuring directory replication, virtualized storage pools, automated access controls, and a hybrid identity link syncing on-premises directory objects to Microsoft Azure (Entra ID).

This lab simulates real-world enterprise network environments and validates the core engineering competencies required for Systems Administrators, Network Operations Engineers, and Hybrid Cloud Administrators.

---

## 📐 Lab Topology & Node Specifications
![Network Diagram](D5zoWY2jcjko7Xt4PBCNZqL9EQtPFbmSdd)

### 🌐 Network Isolation Strategy
- **Switch A (External Switch):** Maps interfaces directly to the host network gateway for outbound WAN access (Windows Updates, cloud software downloads, Azure AD endpoint communication).
- **Switch B (Lab-Private-Switch):** An isolated internal virtual network backbone dedicated strictly to secure Active Directory replication, local DNS queries, DHCP distribution, and internal file traffic.

### 🖥️ Virtual Machine Matrix

| Machine Name | Operating System | Primary Infrastructure Roles & Features | Network Configuration |
| :--- | :--- | :--- | :--- |
| **DC01** | Windows Server 2022 | Primary Domain Controller, AD DS, DNS, DHCP Coordinator | Dual-NIC (NAT/Private Static) |
| **DC02** | Windows Server 2022 | Secondary Replica Domain Controller, Redundant DNS | Dual-NIC (NAT/Private Static) |
| **FileServer01** | Windows Server 2022 | Central Storage Node, Storage Spaces Cluster, FSRM, SMB | Dual-NIC (NAT/Private Static) |
| **Client01** | Windows 11 Pro | Managed Domain Workstation, Enterprise User Endpoint | Dual-NIC (NAT/Private DHCP) |

---

## 🛠️ Skills Demonstrated
By successfully architecting, configuring, and executing this multi-tiered infrastructure lab environment, I have verified hands-on proficiency in the following core competencies:

*   **Hyper-V Virtualization:** Building internal and external network overlays to manage network bounds efficiently.
*   **Active Directory Administration:** Configuring organizational forest components, objects, and directory nodes.
*   **DNS Administration:** Implementing dynamic domain lookup layers and hostname mapping databases.
*   **DHCP Administration:** Building enterprise scopes and network configuration parameter distribution.
*   **Domain Replication:** Forging multi-controller directory sync fabrics for operational high availability.
*   **Group Policy Management:** Centralizing endpoint security posture controls and workstation layouts globally.
*   **Delegation of Control:** Applying granular workspace management privileges aligned to Least Privilege principles.
*   **Storage Pool Management:** Virtualizing unallocated media arrays into resilient virtual drive nodes.
*   **NTFS Security:** Constructing standard corporate resource access security frameworks (AGDLP).
*   **FSRM Quotas:** Protecting active directory server capacity with programmatic hard consumption rules.
*   **Software Deployment:** Orchestrating silent enterprise application updates to endpoints at boot.
*   **PowerShell Administration:** Executing infrastructure management and verification processes cleanly.
*   **Hybrid Identity with Microsoft Azure:** Bridging on-premises AD directory scopes up into Microsoft Entra ID cloud clouds.

---

## 🛠️ Step-by-Step Implementation & Evidence of Success

### 💻 Phase 1 – Hyper-V Infrastructure Deployment
**Objective:** Create the virtualization environment and network infrastructure.
*   **Tasks Completed:**
    *   Created External Virtual Switch
    *   Created Lab-Private Virtual Switch
    *   Created four virtual machines
    *   Connected each virtual machine to both virtual switches
*   **Evidence:**
    *   *Hyper-V Manager:* ![Hyper-V Manager](./Images/01-HyperV-Manager.png)
    *   *External Virtual Switch:* ![External Switch](./Images/02-External-vSwitch.png)
    *   *Lab-Private Virtual Switch:* ![Private Switch](./Images/03-Lab-Private-vSwitch.png)
    *   *VM Network Adapters:* ![VM Adapters](./Images/04-VM-Network-Adapters.png)

---

### ⚙️ Phase 2 – Server Installation and Initial Configuration
**Objective:** Install operating systems and prepare the servers.
*   **Tasks Completed:**
    *   Installed Windows Server 2022
    *   Installed Windows 11
    *   Renamed all virtual machines
    *   Configured static IP addresses
*   **Evidence:**
    *   *Computer Renaming:* ![Server Names](./Images/05-Server-Renames.png)
    *   *Network Configuration:* ![IP Configuration](./Images/06-IP-Configuration.png)

---

### 🔑 Phase 3 – Active Directory Domain Services (AD DS)
**Objective:** Deploy the first domain controller and create the Active Directory forest.
*   **Tasks Completed:**
    *   Installed AD DS role
    *   Created new forest
    *   Created `lab.local` domain
*   **Evidence:**
    *   *AD DS Role Installation:* ![ADDS Installation](./Images/07-ADDS-Role-Installation.png)
    *   *Domain Creation:* ![Domain Creation](./Images/08-Domain-Creation.png)
    *   *Successful Domain Controller Promotion:* ![Domain Controller Success](./Images/09-Domain-Controller-Success.png)

---

### 🌐 Phase 4 – DNS Configuration
**Objective:** Configure name resolution services.
*   **Tasks Completed:**
    *   Verified Forward Lookup Zone
    *   Created DNS records
    *   Tested DNS functionality
*   **Evidence:**
    *   *Forward Lookup Zone:* ![DNS Zone](./Images/10-DNS-Forward-Lookup-Zone.png)
    *   *DNS Host Records:* ![DNS Records](./Images/11-DNS-Host-Records.png)
    *   *NSLookup Test:* ![NSLookup](./Images/12-NSLookup-Test.png)

---

### 📡 Phase 5 – DHCP Configuration
**Objective:** Provide automatic IP addressing.
*   **Tasks Completed:**
    *   Installed DHCP role
    *   Created DHCP scope
    *   Configured DNS and gateway options
    *   Authorized DHCP server
*   **Evidence:**
    *   *DHCP Installation:* ![DHCP Installation](./Images/13-DHCP-Role-Installation.png)
    *   *DHCP Scope:* ![DHCP Scope](./Images/14-DHCP-Scope.png)
    *   *DHCP Lease:* ![DHCP Lease](./Images/15-DHCP-Lease.png)

---

### 🔄 Phase 6 – Secondary Domain Controller and Replication
**Objective:** Implement redundancy and replication.
*   **Tasks Completed:**
    *   Joined DC02 to domain
    *   Promoted DC02
    *   Verified Active Directory replication
*   **Evidence:**
    *   *DC02 Domain Join:* ![DC02 Join](./Images/16-DC02-Domain-Join.png)
    *   *DC02 Promotion:* ![DC02 Promotion](./Images/17-DC02-Promotion.png)
    *   *Replication Summary:* ![Replication](./Images/18-Replication-Summary.png)
    *   *DCDIAG Health Check:* ![DCDIAG](./Images/19-DCDIAG-Test.png)

---

### 🖥️ Phase 7 – Client Domain Join
**Objective:** Integrate a workstation into the domain.
*   **Tasks Completed:**
    *   Joined Client01 to `lab.local`
    *   Logged in using domain credentials
*   **Evidence:**
    *   *Client Domain Join:* ![Client Join](./Images/20-Client01-Domain-Join.png)
    *   *Domain User Login:* ![Domain Login](./Images/21-Client01-Domain-Login.png)

---

### 👥 Phase 8 – Active Directory Administration
**Objective:** Create the logical structure of the organization.
*   **Tasks Completed:**
    *   Created Organizational Units
    *   Created user accounts
    *   Created security groups
*   **Evidence:**
    *   *OU Structure:* ![OU Structure](./Images/22-OU-Structure.png)
    *   *User Accounts:* ![Users](./Images/23-User-Accounts.png)
    *   *Security Groups:* ![Groups](./Images/24-Security-Groups.png)

---

### 📜 Phase 9 – Group Policy Management
**Objective:** Centralize administration and security.
*   **Policies Implemented:**
    *   Password Policy
    *   Wallpaper Policy
    *   USB Restriction Policy
*   **Evidence:**
    *   *Password Policy:* ![Password Policy](./Images/25-Password-Policy.png)
    *   *Wallpaper Policy:* ![Wallpaper GPO](./Images/26-Wallpaper-GPO.png)
    *   *USB Restriction:* ![USB Restriction](./Images/27-USB-Restriction-GPO.png)
    *   *Policy Verification:* ![GPResult](./Images/28-GPResult.png)

---

### 🛡️ Phase 10 – Delegation of Control
**Objective:** Delegate administrative permissions securely to enforce a Least Privilege security framework.
*   **Evidence:**
    *   *Delegation Wizard:* ![Delegation Wizard](./Images/29-Delegation-Wizard.png)
    *   *Delegated Permissions:* ![Delegated Permissions](./Images/30-Delegated-Permissions.png)

---

### 💾 Phase 11 – File Server and Storage Management
**Objective:** Deploy centralized resilient storage.
*   **Tasks Completed:**
    *   Installed File Services
    *   Created Storage Pool (Combining 3 x 20GB raw VHDX drives)
    *   Created Virtual Disk (Mirror/Parity layout)
    *   Created formatted Production NTFS Volume
*   **Evidence:**
    *   *File Services Installation:*
    *    ![File Services](./Images/31-File-Services-Installation.png)
    *   *Storage Pool Configuration:*
    *   ![Storage Pool](./Images/32-Storage-Pool.png)
    *   *Virtual Disk Setup:*
    *    ![Virtual Disk](./Images/33-Virtual-Disk.png)
    *   *Volume Creation:*
    *   ![Volume](./Images/34-Volume-Creation.png)

---

### 📂 Phase 12 – Shared Folders and NTFS Permissions
**Objective:** Provide secure departmental file access using the AGDLP methodology.
*   **Evidence:**
    *   *Shared Folders:* ![Shares](./Images/35-Shared-Folders.png)
    *   *Share Permissions:* ![Share Permissions](./Images/36-Share-Permissions.png)
    *   *NTFS Permissions:* ![NTFS Permissions](./Images/37-NTFS-Permissions.png)

---

### 📊 Phase 13 – Storage Quotas
**Objective:** Control storage utilization via File Server Resource Manager (FSRM).
*   **Evidence:**
    *   *FSRM Installation:* ![FSRM](./Images/38-FSRM-Installation.png)
    *   *Quota Template:* ![Quota Template](./Images/39-Quota-Template.png)
