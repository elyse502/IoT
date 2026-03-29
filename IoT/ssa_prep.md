<details>
  <summary>System Administration</summary>

  # System Administration Technologies

Here are clear, structured notes in Markdown format ready for your GitHub repository.

---

## 1. Clustering Technique

### What / How

Clustering is a technique where multiple servers work together as one system.

**How it works:**
- Several servers called **nodes** are connected
- They share workload
- If one server fails, another takes over
- Managed by clustering software

**Types:**
- **Active-Active** – all servers run tasks simultaneously
- **Active-Passive** – one active, others on standby

---

### Benefits

| Benefit | Description |
|---------|-------------|
| High availability | System remains accessible even if a node fails |
| Fault tolerance | Continuous operation despite hardware failures |
| Load balancing | Workload distributed across multiple servers |
| Reduced downtime | Minimal service interruption |
| Improved performance | Multiple servers handle requests efficiently |

---

## 2. Virtualization

### What / How

Virtualization allows multiple virtual machines to run on one physical server.

**How it works:**
- A **hypervisor** is installed on hardware
- Hypervisor creates virtual machines (VMs)
- Each VM runs its own operating system
- Resources (CPU, RAM, storage) are shared between VMs

**Types:**
- **Full virtualization** – complete hardware emulation
- **Para-virtualization** – modified guest OS for better performance

**Examples:**
- VMware ESXi
- Microsoft Hyper-V
- Oracle VirtualBox
- KVM (Kernel-based Virtual Machine)

---

### Benefits

| Benefit | Description |
|---------|-------------|
| Better resource utilization | Maximize use of physical hardware |
| Cost reduction | Fewer physical servers needed |
| Easy backup and recovery | Snapshot and restore entire VMs |
| Flexible system management | Create, modify, delete VMs easily |
| Isolation between systems | Separate environments for testing and production |

---

## 3. Cloud Computing Technology

### What / How

Cloud computing provides computing services over the internet.

**How it works:**
- Data and applications stored on remote servers
- Users access services via internet
- Managed by cloud providers
- Pay-as-you-go pricing model

**Service Models:**

| Model | Full Form | Description | Example |
|-------|-----------|-------------|---------|
| **IaaS** | Infrastructure as a Service | Virtual machines, storage, networking | AWS EC2, Google Compute Engine |
| **PaaS** | Platform as a Service | Development platforms, databases | Heroku, Google App Engine |
| **SaaS** | Software as a Service | Ready-to-use applications | Gmail, Microsoft 365, Salesforce |

**Examples of Cloud Providers:**
- Amazon Web Services (AWS)
- Microsoft Azure
- Google Cloud Platform (GCP)

---

### Benefits

| Benefit | Description |
|---------|-------------|
| Scalability | Scale resources up or down on demand |
| Cost efficiency | Pay only for what you use |
| Remote access | Access systems from anywhere |
| High availability | Redundant infrastructure across regions |
| Automatic updates | Provider handles maintenance and security |

---

## Quick Comparison

| Technology | Primary Focus | Key Advantage |
|------------|---------------|---------------|
| **Clustering** | Server reliability | High availability and fault tolerance |
| **Virtualization** | Resource efficiency | Better utilization of hardware |
| **Cloud Computing** | Remote services | Scalable, pay-as-you-go access |

---

## Exam Practice Questions

1. Differentiate between Active-Active and Active-Passive clustering.
2. What is a hypervisor? Name two types.
3. Compare IaaS, PaaS, and SaaS with examples.
4. How does virtualization improve disaster recovery?
5. A company experiences frequent server downtime. Which technology would you recommend and why?

---

# System Administration Troubleshooting Tools

Here are clear, exam-ready notes in Markdown format for your GitHub repository.

---

## 1. `ipconfig /release`

### When to Use
Use when you want to **release the current IP address** from a device.

### Conditions
- IP conflict in network
- Wrong IP assigned
- DHCP issues

### Purpose
Forces the system to drop its current IP so a new one can be assigned.

### Command Example
```groovy
ipconfig /release
```

---

## 2. `ipconfig /renew`

### When to Use
Use when you want to **request a new IP address** from DHCP.

### Conditions
- After releasing IP
- No internet access
- DHCP server fixed

### Purpose
Gets a new valid IP address from the DHCP server.

### Command Example
```groovy
ipconfig /renew
```

---

## 3. `ping`

### When to Use
Use to **check connectivity between two devices**.

### Conditions
- Network not reachable
- Slow connection
- Testing if server is alive

### Purpose
Sends ICMP packets and checks for responses.

### Command Examples
```groovy
# Basic ping
ping google.com

# Ping with count limit (Linux/Mac)
ping -c 4 google.com

# Ping with count limit (Windows)
ping -n 4 google.com
```

---

## 4. `ifconfig`

### When to Use
Use to **view or configure network interfaces** in Linux.

### Conditions
- Check IP address
- Check interface status (up/down)
- Network troubleshooting

### Purpose
Displays and configures network interface parameters.

### Command Examples
```groovy
# View all interfaces
ifconfig

# View specific interface
ifconfig eth0

# Bring interface up/down
sudo ifconfig eth0 up
sudo ifconfig eth0 down
```

> **Note:** `ifconfig` is deprecated in some modern Linux distributions. Use `ip addr` as an alternative.

---

## 5. `netstat`

### When to Use
Use to **check active connections and open ports**.

### Conditions
- Suspected unauthorized connections
- Service not responding
- Port issues or conflicts

### Purpose
Shows network statistics, routing tables, and active connections.

### Command Examples
```groovy
# Show all active connections
netstat -a

# Show listening ports
netstat -l

# Show process using each port (Linux)
netstat -tulpn

# Show statistics by protocol
netstat -s
```

---

## 6. `nslookup`

### When to Use
Use to **check DNS resolution**.

### Conditions
- Website not loading
- DNS errors
- Domain not resolving to correct IP

### Purpose
Queries DNS servers to find the IP address of a domain name.

### Command Examples
```groovy
# Basic domain lookup
nslookup google.com

# Query specific DNS server
nslookup google.com 8.8.8.8

# Reverse DNS lookup (IP to domain)
nslookup 8.8.8.8
```

---

## 7. `traceroute`

### When to Use
Use to **trace the path of packets** through the network.

### Conditions
- High latency
- Network delays
- Unknown failure point in network path

### Purpose
Shows each hop (router) between source and destination with response times.

### Command Examples
```groovy
# Linux/Mac
traceroute google.com

# Windows (uses tracert)
tracert google.com

# With IPv6
traceroute -6 google.com
```

---

## 8. `telnet`

### When to Use
Use to **test connection to a specific port on a server**.

### Conditions
- Service not accessible
- Port testing or firewall verification
- Checking if remote service is listening

### Purpose
Tests if a specific port is open and reachable on a remote host.

### Command Examples
```groovy
# Test HTTP port (80)
telnet example.com 80

# Test HTTPS port (443)
telnet example.com 443

# Test SMTP port (25)
telnet mail.example.com 25
```

> **Note:** Telnet is unencrypted and not secure for production use. Use `nc` (netcat) or `nmap` for advanced port scanning.

---

## Quick Revision Table

| Command | Purpose | Platform |
|---------|---------|----------|
| `ipconfig /release` | Drop current IP address | Windows |
| `ipconfig /renew` | Request new IP from DHCP | Windows |
| `ping` | Test basic connectivity | All |
| `ifconfig` | View/configure network interfaces | Linux/Mac |
| `netstat` | Check ports and active connections | All |
| `nslookup` | Query DNS resolution | All |
| `traceroute` | Trace packet path and find delays | All |
| `telnet` | Test specific port connectivity | All |

---

## One-Liner Summary

```groovy
ipconfig /release  →  drop IP
ipconfig /renew    →  get new IP
ping               →  check connection
ifconfig           →  view network config
netstat            →  check ports and connections
nslookup           →  check DNS
traceroute         →  find path issues
telnet             →  test ports
```

---

## Exam Practice Scenario

**Scenario:** A user reports they cannot access `https://example.com`. Walk through the troubleshooting steps using the tools above.

**Solution:**
1. `ping example.com` – Check basic connectivity
2. `nslookup example.com` – Verify DNS resolution
3. `traceroute example.com` – Identify where packets are lost
4. `telnet example.com 443` – Test if HTTPS port is open
5. `ipconfig /release && ipconfig /renew` – Refresh IP if DHCP issue suspected
6. `netstat -an` – Check if local firewall is blocking outbound connections

</details>

<br /><hr /><br />

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
