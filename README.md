<img src="assets/ActiveDirectoryProject.webp">

# Active-Directory-Server-Project

Welcome to the Active Directory Server Project! This project demonstrates the setup and management of a Windows Server environment, featuring **Active Directory**, **IIS**, **DNS**, **DHCP**, and **Sysmon Monitoring**. The goal is to build a secure and functional domain environment with granular user management and robust monitoring capabilities.

---

## Project Overview

This project involves configuring a Windows-based server to provide essential domain and network services, including:

- **Active Directory (AD)** for centralized user and resource management.
- **IIS (Internet Information Services)** for web application hosting.
- **DNS** for domain name resolution.
- **DHCP** for dynamic IP allocation.
- **Sysmon Monitoring** to capture and analyze security-related events.

The configuration highlights best practices in security, role-based access, and user activity monitoring, with an emphasis on understanding Windows Server administration.

---

## Network Design Summary

### Overview

The project creates a simulated network environment with the following elements:
- **Active Directory**: Centralized domain management.
- **IIS**: Hosting a web application for administrative purposes.
- **DNS and DHCP**: Managing network communication and IP allocation.
- **Sysmon**: Monitoring system activities for enhanced security.

---

**IP Table**

| Device              | Role                  | IP Address      |
|---------------------|-----------------------|-----------------|
| **Domain Controller** | AD, DNS, DHCP         | `192.168.1.1`   |
| **Server**          | IIS, Monitoring       | `192.168.1.2`   |
| **Client VMs**      | Domain-Joined Devices | `DHCP Assigned` |

---

### Network Devices

- **Windows Server 2022**: Configured for Active Directory, DNS, DHCP, and IIS roles.
- **Client VMs**: Configured to join the domain and interact with server services.

---

### Key Services Configured
**[1. Active Directory](#1-active-directory)**
- **Service**: Configured AD for user and group management in a domain.

**[2. IIS (Internet Information Services)](#2-iis)**
- **Service**: Configured IIS to host a secure web application.

**[3. DNS** and **DHCP](#3-dns-and-dhcp)**
- **Service**: Configured DNS for domain resolution and DHCP for dynamic IP allocation.

**[4. Sysmon Monitoring](#4-sysmon-monitoring)**
- **Service**: Implemented Sysmon to capture user activities and detect security events.

---

## How Everything Works

1. **Active Directory**: Provides centralized control over users, groups, and resources within the domain.
2. **IIS**: Hosts a web application for administrative or informational purposes, secured with best practices.
3. **DNS and DHCP**: Work together to enable smooth communication between devices in the domain.
4. **Sysmon**: Monitors critical events like logins, process executions, and unauthorized access attempts.

---

## Configuration Details

### **1. Active Directory**
1. Installed the **AD DS** role and promoted the Domain Controller to a domain.
2. Created a new forest and domain (`example.local`).
3. Configured Organizational Units (OUs) for user management:
   - **AdminUsers OU**: For administrators like Alice.
   - **StandardUsers OU**: For regular users like Bob.
4. Joined other servers and clients to the domain.

---

### **2. IIS (Internet Information Services)**
1. Installed IIS on the server and deployed a sample web application.
2. Assigned Alice permissions to manage IIS and its resources.
3. Secured IIS with HTTPS and NTFS permissions to prevent unauthorized access.

---

### **3. DNS and DHCP**
1. Configured DNS:
   - Verified name resolution for domain resources.
   - Added conditional forwarders for external DNS resolution.
2. Configured DHCP:
   - Set up a scope to allocate IP addresses dynamically.
   - Enabled dynamic DNS updates for seamless IP-to-hostname mapping.

---

### **4. Sysmon Monitoring**
1. Installed Sysmon from [Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon).
2. Applied a configuration file ([SwiftOnSecurity Sysmon Config](https://github.com/SwiftOnSecurity/sysmon-config)) to capture relevant events.
3. Monitored and analyzed user activities:
   - Alice's administrative actions.
   - Bob's file access attempts.

---

## Challenges Faced

1. **Domain Controller Promotion Issues**:
   - DNS was not properly configured during AD promotion, causing domain joins to fail. Fixed by manually correcting DNS settings in `Server Manager`.

2. **IIS Configuration**:
   - Permissions on the `wwwroot` folder caused access issues. Resolved by adjusting NTFS permissions and testing with Alice's credentials.

3. **DHCP Failures**:
   - Clients were not receiving IP addresses due to a misconfigured DHCP scope. Adjusted the range and restarted the DHCP service.

4. **Sysmon Noise**:
   - Sysmon logs contained excessive noise. Applied filters in the configuration file to focus on critical events.

---

## How to Use This Project

1. **Set Up the Environment**:
   - Configure a private network in your virtualization tool.
   - Install Windows Server 2022 on all VMs.

2. **Deploy Active Directory**:
   - Promote the Domain Controller VM to a domain.
   - Join the Server and Client VMs to the domain.

3. **Configure Services**:
   - Install and configure IIS, DNS, DHCP, and Sysmon as outlined above.

4. **Verify Functionality**:
   - Test:
     - User logins and domain permissions.
     - IIS access for Alice.
     - DHCP and DNS resolution on clients.
     - Sysmon logs for monitored activities.

---

## Contributors

- **Rayane Oulad** - Configuration & Documentation

---

## Future Improvements

1. **Scalability**: Extend the domain to include additional sites or forests.
2. **Security**: Implement advanced security measures like Group Policy hardening and multi-factor authentication.
3. **Monitoring Enhancements**: Integrate tools like Splunk or ELK for more detailed log analysis.
4. **Backup and Disaster Recovery**: Automate backups for Active Directory and server configurations.

---
