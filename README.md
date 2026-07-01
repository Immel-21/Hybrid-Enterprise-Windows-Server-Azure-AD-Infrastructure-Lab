# Hybrid Enterprise Windows Server & Azure AD Infrastructure Lab

## 📌 Project Overview
This advanced lab demonstrates the end-to-end deployment of a resilient, multi-server enterprise Windows Server environment virtualized within Microsoft Hyper-V. The objective was to design, implement, secure, and manage an infrastructure featuring directory replication, virtualized storage pools, automated access controls, and a hybrid identity link syncing on-premises directory objects to Microsoft Azure (Entra ID).

This lab simulates real-world enterprise network environments and validates the core engineering competencies required for Systems Administrators, Network Operations Engineers, and Hybrid Cloud Administrators.

---

## 📐 Lab Topology & Node Specifications
![Network Diagram](Documentation/NetworkDiagram.png)

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
    *   *Hyper-V Manager:*
    *   ![Hyper-V Manager](images/HyperV/01-4vms-HyperV-Manager.PNG)
    *   *Hyper-V Virtual Switch:*
    *    ![Virtual Switch](images/HyperV/02-default-and-private-Switch.PNG)
    *   *VM Network Adapters:*
    *    ![VM Adapters](images/HyperV/03-VM-Network-Adapters.PNG)

---

### ⚙️ Phase 2 – Server Installation and Initial Configuration
**Objective:** Install operating systems and prepare the servers.
*   **Tasks Completed:**
    *   Installed Windows Server 2022
    *   Installed Windows 11
    *   Renamed all virtual machines
    *   Configured static IP addresses
*   **Evidence:**
    *   *Computer Renaming:*
    *   ![Server Names](images/ServerSetup/04-Server-Renames.PNG)
    *   *Network Configuration:*
    *    ![IP Configuration](images/ServerSetup/05-IP-Configuration.PNG)

---

### 🔑 Phase 3 – Active Directory Domain Services (AD DS)
**Objective:** Deploy the first domain controller and create the Active Directory forest.
*   **Tasks Completed:**
    *   Installed AD DS role
    *   Created new forest
    *   Created `lab.local` domain
*   **Evidence:**
    *   *AD DS Role Installation:*
    *   ![ADDS Installation](images/ADDS/06-ADDS-Role-Installation.PNG)
    *   *Domain Creation:*
    *    ![Domain Creation](images/ADDS/07-Domain-creation.PNG)
    *   *Successful Domain Controller Promotion:*
    *   ![Domain Controller Success](images/ADDS/08-Domain-Controller-Success.PNG)

---

### 🌐 Phase 4 – DNS Configuration
**Objective:** Configure name resolution services.
*   **Tasks Completed:**
    *   Verified Forward Lookup Zone
    *   Created DNS records
    *   Tested DNS functionality
*   **Evidence:**
    *   *Forward Lookup Zone:*
       ![DNS Zone](images/DNS/09-DNS-Forward-Lookup-Zone.PNG)
    *   *DNS Host Records:*
       ![DNS Records](images/DNS/10-DNS-Forward-Lookup-Zone.PNG)
    *   *NSLookup Test:*
        ![NSLookup](images/DNS/10-DNS-Forward-Lookup-Zone.PNG)

---

### 📡 Phase 5 – DHCP Configuration
**Objective:** Provide automatic IP addressing.
*   **Tasks Completed:**
    *   Installed DHCP role
    *   Created DHCP scope
    *   Configured DNS and gateway options
    *   Authorized DHCP server
*   **Evidence:**
    *   *DHCP Installation:*
       ![DHCP Installation](images/DHCP/12-DHCP-Role-Installation.PNG)
    *   *DHCP Scope:*
       ![DHCP Scope](images/DHCP/13-DHCP-Scope.PNG)
    *   *DHCP Lease:*
       ![DHCP Lease](images/DHCP/14-DHCP-Lease.PNG)

---

### 🔄 Phase 6 – Secondary Domain Controller and Replication
**Objective:** Implement redundancy and replication.
*   **Tasks Completed:**
    *   Joined DC02 to domain
    *   Promoted DC02
    *   Verified Active Directory replication
*   **Evidence:**
    *   *DC02 Domain Join:*
    *    ![DC02 Join](images/Replication/15-DC02-Domain-Join.PNG)
    *   *DC02 Promotion:*
    *   ![DC02 Promotion](images/Replication/16-DC02-Promotion.PNG)
    *   *Replication Summary:*
    *   ![Replication](images/Replication/17-Replication-Summary.PNG)
    *   *DCDIAG Health Check:*
    *   ![DCDIAG](images/Replication/18-DCDIAG-Test.PNG)

---

### 🖥️ Phase 7 – Client Domain Join
**Objective:** Integrate a workstation into the domain.
*   **Tasks Completed:**
    *   Joined Client01 to `lab.local`
    *   Logged in using domain credentials
*   **Evidence:**
    *   *Client Domain Join:*
    *   ![Client Join](images/ClientJoin/19-Client01-Domain-Join.PNG)
    *   *Domain User Login:*
    *    ![Domain Login](images/ClientJoin/20-Client01-Domain-Login.PNG)

---

### 👥 Phase 8 – Active Directory Administration
**Objective:** Create the logical structure of the organization.
*   **Tasks Completed:**
    *   Created Organizational Units
    *   Created user accounts
    *   Created security groups
*   **Evidence:**
    *   *OU Structure:*
    *   ![OU Structure](images/AD-Administration/21-OU-Structure.PNG)
    *   *User Accounts:*
    *   ![Users](images/AD-Administration/22-User-Accounts..PNG)
    *   *Security Groups:*
    *    ![Groups](images/AD-Administration/23-Security-Groups.PNG)

---

### 📜 Phase 9 – Group Policy Management
**Objective:** Centralize administration and security.
*   **Policies Implemented:**
    *   Password Policy
    *   Wallpaper Policy
    *   USB Restriction Policy
*   **Evidence:**
    *   *Password Policy:*
    *    ![Password Policy](images/GPO/24-Password-Policy.PNG)
    *   *Wallpaper Policy:*
    *    ![Wallpaper GPO](images/GPO/25-Wallpaper-GPO..PNG)
    *   *USB Restriction:*
    *    ![USB Restriction](images/GPO/26-USB-Restriction-GPO.PNG)
    *   *Policy Verification:*
    *    ![GPResult](images/GPO/27-GPResult.PNG)

---

### 🛡️ Phase 10 – Delegation of Control
**Objective:** Delegate administrative permissions securely to enforce a Least Privilege security framework.
*   **Evidence:**
    *   *Delegation Wizard:*
    *    ![Delegation Wizard](images/Delegation/28-Delegation-Wizard.png)
    *   *Delegated Permissions:*
    *    ![Delegated Permissions](images/Delegation/29-Delegated-Permissions.PNG)

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
    *    ![File Services](images/FileServer/30-File-Services-Installation.PNG)
    *   *Storage Pool Configuration:*
    *   ![Storage Pool](images/FileServer/31-Storage-Pool.PNG)
    *   *Virtual Disk Setup:*
    *    ![Virtual Disk](images/FileServer/32-Virtual-Disk.PNG)
    *   *Volume Creation:*
    *   ![Volume](images/FileServer/33-Volume-Creation.PNG)

---

### 📂 Phase 12 – Shared Folders and NTFS Permissions
**Objective:** Provide secure departmental file access using the AGDLP methodology.
*   **Evidence:**
    *   *Shared Folders:*
    *   ![Shares](images/NTFS/34-Shared-Folders.PNG)
    *   *Share Permissions:*
    *    ![Share Permissions](images/NTFS/35-Share-Permissions.PNG)
    *   *NTFS Permissions:*
    *    ![NTFS Permissions](images/NTFS/36-NTFS-Permissions.PNG)

---

### 📊 Phase 13 – Storage Quotas
**Objective:** Control storage utilization via File Server Resource Manager (FSRM).
*   **Evidence:**
    *    *  **Hard Storage Consumption Allocation Control Limit Boundary Layouts:**
    *    ![FSRM](images/Quota/37-Quota-Template.PNG)
    *    **Active Enforced Storage Volumes Quota Enforcement Scopes Dashboard:**
    *    ![Quota Template](images/Quota/38-Quota-Applied.PNG)
 
---

### 🗺️ Phase 14 – Drive Mapping
Automated data storage discovery settings to map department network spaces cleanly on login.
*   **Group Policy Preferences (GPP) Logical Drive-Map Policy Properties:**
    ![Drive Mapping GPO](images/DriverMapping/39-Drive-Mapping-GPO.PNG)
*   **Endpoint File Explorer Mapped Storage Target Drive Profiles:**
    ![Mapped Drives](images/DriverMapping/40-Mapped-Drives.PNG)

---

### 📦 Phase 15 – Software Deployment
Automated common software setups to keep remote network systems uniform.
*   **Centralized Deployment Package (.MSI) Shared Distribution Repository:**
    ![Software Share](images/SoftwareDeployment/41-Software-Share.png)
*   **Active Directory Group Policy Software Distribution Scope Paths:**
    ![Software Deployment](images/SoftwareDeployment/42-Software-Deployment-GPO.png)
*   **Target Client Device Applications Installation Verification History:**
    ![Installed Software](images/SoftwareDeployment/43-Installed-Software.png)

---

### ☁️ Phase 16 – Azure AD Connect Synchronization
Objective: Implement hybrid identity by linking on-premises directory structures to Microsoft Azure (Entra ID).
* **Tasks Completed:**
* Installed Azure AD Connect Engine
* Connected Cloud Azure Identity Tenant
* Configured OU Filtering and Delta Synchronization
* Verified Successful Sync Operations
* **Evidence:**
* **Azure AD Connect Installation:**
   ![Azure AD Connect](images/AzureADConnect/44-AzureADConnect-Installation.PNG)
* **Azure Tenant Connection Handshake:**
   ![Azure AD Connect](images/AzureADConnect/45-Azure-Tenant-Connection.PNG)
* **Synchronization Profile Configuration:**
   ![Azure AD Connect](images/AzureADConnect/46-Synchronization-Configuration.PNG)
* **Successful Sync Lifecycle Dashboard:**
   ![Azure AD Connect](images/AzureADConnect/47-Synchronization-Success.PNG) 
