# Architectural Design Decisions & Technical Trade-offs

This document outlines the real-world operational reasoning behind the engineering choices made during the deployment of the Hybrid Enterprise Windows Server & Azure AD Infrastructure Lab. 

---

## 📐 Infrastructure Design Matrices

| Infrastructure Layer | Operational Implementation | Engineering Justification (Why it matters to a business) |
| :--- | :--- | :--- |
| **Dual-NIC Isolation Strategy** | Configured dual-homed networks using separate virtual switches. One handled outbound WAN traffic for Azure AD Connect; the other hosted an isolated private backend switch. | Tight environment isolation. It prevents experimental lab configurations or rogue DHCP offers from leaking into and disrupting the wider corporate production host network. |
| **Identity Redundancy & Replication** | Deployed a secondary replica domain controller (`DC02`) and verified database health parameters using native `DCDIAG` and `repadmin` diagnostic routines. | High availability configuration. Eliminates identity infrastructure single points of failure. If the primary controller drops offline, user authentication switches seamlessly to the working replica. |
| **Virtualized Storage Pools** | Aggregated three unallocated raw physical virtual hard disks (VHDX) into a singular Windows Storage Space pool with Mirror layout resiliency. | Cost-effective resource scalability. Allows a business to pool disparate, inexpensive physical drive hardware into highly flexible, fault-tolerant logical storage volumes. |
| **Access Control (AGDLP Method)** | Structural alignment where Accounts go into Global Groups, Global Groups go into Domain Local Groups, which map directly to NTFS folder system access control lists. | Standardized resource access management. Drastically simplifies user access audits. IT managers only ever add users to global roles instead of manually modifying file arrays. |
| **Storage Capacity Protections** | Installed File Server Resource Manager (FSRM) to enforce strict hard capacity boundaries over corporate file directory partitions. | Resource depletion prevention. Actively blocks end-users from monopolizing valuable storage space or filling network volumes with non-business data. |
| **Desktop Workspace Automation** | Engineered Group Policy Preferences (GPP) for scriptless mapped drive deployment alongside silent .MSI application installation at device boot. | Lower operational overhead. Eliminates manual service desk tickets by standardizing user workspaces automatically the second they log into the domain. |
| **Identity Federation Bridge** | Implemented the Azure AD Connect synchronization engine to build an express identity pipeline extending targeted local OUs to Microsoft Entra ID. | Single Sign-On (SSO) enablement. Unifies identity lifecycles so corporate users can securely use a single set of credentials for local systems and cloud SaaS tools. |

---

## 🛠️ Verification Commands Quick-Reference
To maintain this infrastructure and audit operational health during deployment, the following administrative commands were executed:

### Active Directory Health Audits
```powershell
# Evaluates domain controller status and checks for critical subsystem errors
dcdiag /v

# Displays active directory replication topologies and success status matrices
repadmin /replsummary
repadmin /showrepl
```

### Endpoint Policy Audits
```cmd
# Validates active Group Policy Object (GPO) applications on the target client node
gpresult /r
```
