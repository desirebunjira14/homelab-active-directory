# 🏢 Homelab Phase 2 – Active Directory & User Management

**Role alignment:** IT Support Specialist | Junior Sysadmin | Datacenter Technician | Helpdesk

**Objective:** Build a fully functional domain from scratch and learn the daily tasks of an IT professional.

---
📦 What I Built

## 🖥️ Domain Controller (DC01)

| Property | Value |
|----------|-------|
| **Purpose** | Primary Domain Controller & Active Directory Services |
| **Operating System** | Windows Server 2022 (Desktop Experience) |
| **Hostname** | `DC01` |
| **Domain FQDN** | `mydomain.local` |
| **IP Address** | `172.16.0.1` (Static) |
| **Subnet Mask** | `255.255.255.0` |
| **Default Gateway** | (None - Internal Network) |
| **DNS Server** | `127.0.0.1` (Self) |
| **vCPU** | 2 Cores |
| **RAM** | 4 GB |
| **Hard Disk** | 60 GB (Dynamically Allocated) |
| **Network Adapter** | NAT / Internal Network |
| **Hypervisor** | VirtualBox / VMware (User's Choice) |
| **Roles Installed** | Active Directory Domain Services, DNS, DHCP (Planned) |

### 🔧 Services Hosted

- ✅ Active Directory Domain Services (AD DS)
- ✅ DNS Server
- ⬜ DHCP Server (To be installed)
- ⬜ RAS / NAT (To be installed)

### 📝 Notes

- This server acts as the primary domain controller for the `mydomain.local` forest.
- Configured with a static IP to ensure consistent network addressing.
- DNS is set to loopback (`127.0.0.1`) as the server hosts its own DNS services.
- Use the dedicated `admin.jsmith` account for administrative tasks.

- ## 🖥️ Client Machine (CLIENT1)

| Property | Value |
|----------|-------|
| **Purpose** | Windows 11 Test Client for Domain Testing |
| **Operating System** | Windows 11 |
| **Hostname** | `CLIENT1` |
| **Domain Status** | Joined to `mydomain.local` |
| **IP Address** | DHCP (Reserved: `172.16.0.100 - 172.16.0.200`) |
| **Subnet Mask** | `255.255.255.0` (Assigned by DHCP) |
| **Default Gateway** | `172.16.0.1` (DC01) |
| **DNS Server** | `172.16.0.1` (DC01) |
| **vCPU** | 2 Cores |
| **RAM** | 4 GB |
| **Hard Disk** | 128 GB (Dynamically Allocated) |
| **Network Adapter** | Internal Network |
| **Hypervisor** | VirtualBox / VMware (User's Choice) |

### 🔑 Credentials

| Account | Username | Password | Purpose |
|---------|----------|----------|---------|
| **Local Admin** | `Administrator` | `[Set During Installation]` | Initial Setup & Recovery |
| **Domain Admin** | `admin.jsmith` | `Admin123!` | Domain Administration |
| **Test User** | `mydomain\jsmith` | `Password123!` | User Testing |

### 📝 Notes

- This client is used to test domain-joined functionality.
- IP address is automatically assigned via DHCP from DC01.
- Can be used to test Group Policy application.
- Good for testing user login, folder redirection, and printer deployment.

## 🌐 Network Infrastructure

| Component | Role | IP Address | Connection |
|-----------|------|------------|------------|
| **Main Host** | VirtualBox Host | `N/A` | NAT to DC01 |
| **DC01** | Domain Controller | `172.16.0.1` (Static) | Internal Network |
| **DHCP Scope** | IP Assignment | `172.16.0.100-200` | Managed by DC01 |
| **CLIENT1** | Windows 10/11 Client | `172.16.0.x` (DHCP) | Internal Network |

### 📝 Connectivity Flow

- Main Host runs VirtualBox with NAT networking
- DC01 has a static IP (172.16.0.1) on the Internal Network
- DHCP Scope assigns IPs (172.16.0.100-200) to clients
- CLIENT1 receives an IP via DHCP and joins the domain
