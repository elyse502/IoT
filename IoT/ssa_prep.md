# 🛠️ System Administration Fundamentals

A quick reference guide covering core system administration concepts including access control, virtualization, networking, and system availability.

---

## 1. User Access Control & Privilege Management

### 🔐 Access Control
Ensures users can only access what they need.

**Importance**
- Protects sensitive data
- Prevents unauthorized access
- Reduces security risks
- Ensures accountability (user tracking)
- Supports compliance with policies

### 👤 Privilege Management
Ensures users are assigned appropriate permissions.

| Role        | Access Level        |
|------------|--------------------|
| Admin       | Full control       |
| Normal User | Limited access     |

---

## 2. Duties of a System Administrator

### 🧑‍💻 Core Responsibilities
- Install and configure systems/servers
- Monitor system performance
- Manage user accounts and permissions
- Perform backups and recovery
- Maintain system security and updates

### 🔧 Additional Responsibilities
- Troubleshooting issues
- Network management

---

## 3. Hyper-V & Active Directory

### 🖥️ Hyper-V
Microsoft virtualization platform.

**Key Roles**
- Run multiple virtual machines (VMs)
- Optimize hardware usage
- Support testing environments

### 📂 Active Directory (AD)

**Key Roles**
- Manage users and computers
- Provide centralized authentication
- Control access to resources

---

## 4. Proactive Measures for System Availability

- Regular system updates
- Scheduled backups
- Continuous monitoring
- Redundancy implementation
- Security hardening

---

## 5. Server Congestion

### ⚠️ Definition
Occurs when a server cannot handle incoming traffic load.

### 📉 Causes
- High user traffic
- Limited system resources
- Poor configuration

### 💥 Effects
- Slow response times
- System crashes

### 🛠️ Solutions
- Upgrade hardware
- Implement load balancing
- Optimize applications
- Monitor usage patterns

---

## 6. Clustering & Virtualization

### A. 🔗 Clustering

**Concept**  
Multiple servers operate as a single system.

**Advantages**
- High availability
- Fault tolerance

**Challenges**
- Complex setup
- Higher cost

---

### B. 🧪 Virtualization

**Concept**  
Run multiple VMs on a single physical server.

**Advantages**
- Efficient resource usage
- Cost savings

**Challenges**
- Performance overhead
- Requires management tools

---

## 7. Users in Windows & Linux

### 🪟 Windows User Types

| User Type      | Access Level      |
|---------------|------------------|
| Administrator | Full control     |
| Standard User | Limited access   |
| Guest         | Very limited     |

### 🐧 Linux User Types

| User Type     | Role                     |
|--------------|--------------------------|
| Root         | Full control             |
| Normal User  | Limited access           |
| Service User | Runs background services |

---

## 8. DHCP Process (DORA)

Dynamic Host Configuration Protocol assigns IP addresses automatically.

| Step       | Description                          |
|------------|--------------------------------------|
| Discover   | Client broadcasts request            |
| Offer      | Server offers IP address             |
| Request    | Client requests offered IP           |
| Acknowledge| Server confirms assignment           |

---

## 9. RAID (Redundant Array of Independent Disks)

### 📊 RAID Levels

| Level  | Description                | Benefit            |
|--------|----------------------------|--------------------|
| RAID 0 | No redundancy              | High performance   |
| RAID 1 | Mirroring                  | High reliability   |
| RAID 5 | Parity-based distribution  | Balanced approach  |

### ✅ Benefits
- Data protection
- Improved performance

### ⚠️ Challenges
- Cost
- Complex setup

---

## 10. System Availability & Business Continuity

- Backup and recovery strategies
- Disaster recovery sites
- Load balancing
- Redundant infrastructure
- Monitoring and alerting tools

---

## ⚡ Quick Revision

- Access control → Protects systems  
- Admin → Manages infrastructure  
- Hyper-V → Enables virtualization  
- Active Directory → Manages identities  
- DHCP → Assigns IP addresses  
- RAID → Protects data  
- Clustering → Improves availability  
- Virtualization → Optimizes resources  

---

## 📌 Contributing

Feel free to improve this document by:
- Adding real-world examples
- Including diagrams
- Expanding sections with commands or tools

---

## 📄 License

This documentation is open-source and free to use.
