# Server and System Administration - CAT Preparation Guide

As your lecturer for Server and System Administration, I've compiled comprehensive answers to all the questions in your past paper. Let's go through them systematically.

---

# SECTION A

## QUESTION 1 (COMPULSORY)

### A. Steps to Assess Impact of Increased Network Traffic (5 Marks)

**Step 1: Establish Baseline Metrics**
- Measure normal server performance during typical operations
- Document CPU, memory, disk I/O, and network utilization during off-peak hours

**Step 2: Monitor Server Resource Utilization**

| Resource | Metrics to Monitor | Tools |
|----------|-------------------|-------|
| CPU | Usage %, Load Average, Context Switches | top, htop, Windows Performance Monitor |
| Memory | RAM usage, Swap usage, Page faults | free -m, vmstat |
| Disk I/O | Read/write speed, Queue length, IOPS | iostat, iotop |
| Network | Bandwidth usage, Packet loss, Latency | iftop, nload, Wireshark |

**Step 3: Analyze Application Performance**
- Response time measurements
- Throughput (requests per second)
- Error rates (HTTP 5xx errors)
- Transaction completion rates

**Step 4: Identify Peak Usage Patterns**
- Time-based analysis (daily, weekly patterns)
- User concurrency levels
- Geographic distribution of traffic

**Step 5: Document Findings**
- Create performance reports
- Identify thresholds being exceeded
- Prioritize areas requiring immediate attention

**Recommended Monitoring Tools:**
- **Nagios/Zabbix** - Comprehensive server monitoring
- **Prometheus + Grafana** - Metrics collection and visualization
- **NetFlow/sFlow** - Network traffic analysis
- **ELK Stack** - Log analysis

---

### B. Identify Bottlenecks and Troubleshooting Strategies (5 Marks)

**Common Bottlenecks:**

| Bottleneck Type | Symptoms | Diagnostic Commands |
|-----------------|----------|---------------------|
| **CPU Bottleneck** | High load average, slow response | `top`, `mpstat -P ALL` |
| **Memory Bottleneck** | High swap usage, OOM errors | `free -h`, `vmstat 1` |
| **Disk I/O Bottleneck** | High wait time (iowait), slow reads | `iostat -x 1`, `iotop` |
| **Network Bottleneck** | Packet loss, high latency, retransmissions | `netstat -i`, `ping`, `traceroute` |

**Troubleshooting Strategies:**

**1. Hardware-Level Diagnosis:**
```bash
# Check CPU load and processes
top -c

# Check memory usage
free -m

# Check disk I/O
iostat -x 1 5

# Check network connections
netstat -tunap | wc -l
```

**2. Software-Level Diagnosis:**
- Review application logs (`/var/log/`)
- Check web server logs (Apache/Nginx access and error logs)
- Analyze database slow query logs
- Examine system logs for errors (`journalctl -xe`)

**3. Network-Level Diagnosis:**
```bash
# Test network connectivity
ping -c 10 target_server

# Trace network path
traceroute target_server

# Monitor real-time bandwidth
iftop -i eth0

# Capture packets for analysis
tcpdump -i eth0 -w capture.pcap
```

**4. Remediation Strategies:**
- **Scale up**: Upgrade hardware (more RAM, faster CPU)
- **Scale out**: Add more servers behind load balancer
- **Optimize**: Tune application configuration
- **Cache**: Implement caching layers (Redis, Memcached)
- **Queue**: Use message queues for async processing

---

# SECTION B

## QUESTION 2: Availability Mechanisms (10 Marks)

Five solutions to ensure system availability:

### 1. **Redundant Hardware Configuration**
- **RAID (Redundant Array of Independent Disks)** - Protect against disk failure
  - RAID 1 (mirroring), RAID 5/6 (parity), RAID 10 (striping + mirroring)
- **Redundant Power Supplies (RPS)** - Prevent power failure outages
- **Redundant Network Interface Cards (NIC Teaming)** - Failover if one NIC fails

### 2. **High Availability (HA) Clustering**
- Multiple servers work together as a cluster
- If one server fails, another automatically takes over
- Examples: **Pacemaker + Corosync**, **Windows Failover Cluster**

### 3. **Load Balancing**
- Distribute traffic across multiple servers
- Prevent any single server from being overwhelmed
- Tools: **HAProxy**, **Nginx**, **F5 Big-IP**, **AWS Elastic Load Balancer**

### 4. **Comprehensive Backup and Disaster Recovery**
- **Regular backups** (daily, weekly, offsite)
- **3-2-1 Backup Rule**: 3 copies, 2 different media, 1 offsite
- **RTO (Recovery Time Objective)** and **RPO (Recovery Point Objective)** defined
- **Disaster Recovery Plan (DRP)** documented and tested

### 5. **Monitoring and Alerting System**
- Proactive monitoring to detect issues before they cause outages
- Real-time alerts for threshold breaches
- Tools: **Nagios**, **Zabbix**, **Prometheus**, **Datadog**

---

## QUESTION 3: Clustering and Virtualization

### A. Clustering Technique (5 Marks)

**Concept:**
Clustering is the practice of grouping multiple servers to work together as a single system, providing high availability, load balancing, and scalability.

**Types of Clusters:**

| Cluster Type | Purpose | Example |
|--------------|---------|---------|
| **High Availability (HA)** | Automatic failover | Web server cluster |
| **Load Balancing** | Distribute workload | Application servers |
| **High Performance Computing (HPC)** | Parallel processing | Scientific computing |

**Challenges:**
- **Complexity** in configuration and management
- **Split-brain** scenarios (multiple nodes thinking they're primary)
- **Cost** of additional hardware and software licenses
- **Network latency** between cluster nodes

**Advantages:**
- **Fault tolerance** - No single point of failure
- **Scalability** - Add nodes as demand grows
- **Improved performance** - Workload distribution
- **Maintenance without downtime** - Rolling updates

---

### B. Virtualization Technology (5 Marks)

**Concept:**
Virtualization creates virtual versions of physical resources (servers, storage, networks) allowing multiple operating systems to run on a single physical machine.

**Types of Virtualization:**
- **Server Virtualization** - VMware ESXi, Microsoft Hyper-V, KVM
- **Desktop Virtualization** - VDI (Virtual Desktop Infrastructure)
- **Network Virtualization** - SDN (Software-Defined Networking)
- **Storage Virtualization** - SAN, NAS

**Challenges:**
- **Performance overhead** - Hypervisor consumes resources
- **Licensing complexity** - OS licensing across VMs
- **Security concerns** - VM escape vulnerabilities
- **Management complexity** - Multiple VMs to monitor

**Advantages:**
- **Resource utilization** - Consolidate underutilized servers
- **Cost savings** - Reduce hardware, power, cooling costs
- **Isolation** - Applications run independently
- **Disaster recovery** - Quick VM backup and restoration
- **Flexibility** - Rapid provisioning of new servers

---

## QUESTION 4: User Access Controls & Server Congestion

### A. Importance of User Access Controls (5 Marks)

**1. Prevent Unauthorized Access**
- Ensure only authenticated users access systems
- Protect sensitive data from breaches

**2. Least Privilege Principle**
- Users get only necessary permissions
- Minimize damage from compromised accounts

**3. Audit and Accountability**
- Track who did what and when
- Meet compliance requirements (GDPR, HIPAA, etc.)

**4. Segregation of Duties**
- Prevent single user from having excessive control
- Reduce fraud and error risks

**5. Operational Stability**
- Prevent accidental system changes by unauthorized users
- Maintain system integrity

**Common Access Control Mechanisms:**
- **RBAC** (Role-Based Access Control)
- **MFA** (Multi-Factor Authentication)
- **SSH key authentication**
- **sudo** for privilege escalation

---

### B. Server Congestion (5 Marks)

**Sources of Server Congestion:**

| Source | Cause |
|--------|-------|
| **CPU Congestion** | Too many processes, inefficient code, CPU-intensive tasks |
| **Memory Congestion** | Memory leaks, insufficient RAM, excessive swap usage |
| **Disk I/O Congestion** | Slow disks, high read/write operations, insufficient IOPS |
| **Network Congestion** | Bandwidth saturation, high latency, packet loss |

**How to Handle Server Congestion:**

**1. Proactive Monitoring:**
```bash
# Monitor system resources in real-time
top
htop
nload -u M
```

**2. Immediate Mitigation:**
- Identify and kill resource-hungry processes
- Restart problematic services
- Throttle non-critical services

**3. Short-term Solutions:**
- Increase resources (scale up)
- Add caching layers
- Implement rate limiting

**4. Long-term Solutions:**
- Load balancing across multiple servers
- Database query optimization
- Application code optimization
- Move to distributed architecture

**5. Capacity Planning:**
- Trend analysis of resource usage
- Predictive scaling based on growth patterns

---

## QUESTION 5: Configuration Management & Server Security

### A. Configuration Management Tools (5 Marks)

**Role of Configuration Management Tools:**
- Automate server provisioning and configuration
- Ensure consistent configurations across environments
- Track and manage configuration changes
- Enable Infrastructure as Code (IaC)

**Popular Tools and Their Features:**

| Tool | Features | Use Case |
|------|----------|----------|
| **Ansible** | Agentless, YAML-based playbooks, simple syntax | Configuration management, application deployment |
| **Puppet** | Declarative language, master-agent architecture | Enterprise configuration management |
| **Chef** | Ruby-based, recipe and cookbook model | Infrastructure automation |
| **Terraform** | Infrastructure as Code, multi-cloud | Provisioning cloud resources |
| **SaltStack** | High-speed, remote execution | Large-scale infrastructure management |

---

### B. Steps to Secure a Server (5 Marks)

**1. Physical Security**
- Secure server rooms with access control
- Surveillance cameras
- Environmental controls (temperature, fire suppression)

**2. Operating System Hardening**
- Remove unnecessary services and packages
- Apply security patches regularly
- Configure firewall (iptables, firewalld)
- Enable SELinux or AppArmor

**3. Access Control**
- Use SSH key authentication (disable password auth)
- Implement MFA for administrative access
- Configure sudo with least privilege
- Regular password policy enforcement

**4. Malware Protection**
- Install and update antivirus/anti-malware
- Regular security scanning
- Monitor for suspicious processes
- Use intrusion detection systems (IDS) like OSSEC, Snort

**5. Denial-of-Service Protection**
- Implement rate limiting at application level
- Use DDoS protection services (Cloudflare, AWS Shield)
- Configure connection limits in web servers
- Deploy load balancers to distribute traffic

**Security Hardening Checklist:**
```bash
# Disable root SSH login
PermitRootLogin no

# Change default SSH port
Port 2222

# Configure firewall
ufw allow 2222/tcp
ufw enable

# Check listening ports
netstat -tulpn

# Monitor logs
tail -f /var/log/auth.log
```

---

## QUESTION 6: Network Operating System & System Assessment

### A. Network Operating System Components (5 Marks)

**Typical NOS Architecture Components:**

```
┌─────────────────────────────────────────┐
│           Applications Layer            │
├─────────────────────────────────────────┤
│         Network Services Layer          │
│   (DNS, DHCP, Web, File, Print)         │
├─────────────────────────────────────────┤
│           Protocol Stack                │
│      (TCP/IP, UDP, ICMP, etc.)          │
├─────────────────────────────────────────┤
│           Network Drivers               │
├─────────────────────────────────────────┤
│           Hardware Layer                │
│      (NICs, Switches, Routers)          │
└─────────────────────────────────────────┘
```

**Component Roles:**

| Component | Role |
|-----------|------|
| **Kernel** | Manages hardware resources, process scheduling, memory management |
| **Network Stack** | Handles TCP/IP protocol implementation |
| **Network Services** | DNS resolution, DHCP addressing, file sharing, web serving |
| **Security Layer** | Firewall, authentication, access control |
| **Management Interface** | CLI, GUI, API for administration |

---

### B. Importance of Comprehensive System Assessment (5 Marks)

**Why Conduct System Assessment Before Changes:**

1. **Risk Identification**
   - Identify potential negative impacts before implementation
   - Prevent unexpected outages

2. **Baseline Establishment**
   - Know current performance metrics
   - Measure improvements after changes

3. **Dependency Mapping**
   - Understand system interdependencies
   - Avoid breaking dependent services

4. **Resource Planning**
   - Ensure adequate resources for proposed changes
   - Prevent capacity issues

5. **Rollback Planning**
   - Define steps to revert if changes fail
   - Minimize downtime during issues

**Assessment Checklist:**
- Current system configuration documentation
- Performance baseline (CPU, memory, disk, network)
- Dependency mapping
- Backup verification
- Change impact analysis
- Rollback procedure

---

# Linux System Administration Section

## QUESTION 2: Linux Architecture Components (10 Marks)

### A. The Kernel (4 Marks)

**Main Responsibilities:**
- **Process Management**: Schedules and manages processes, handles context switching
- **Memory Management**: Manages virtual memory, paging, swapping
- **Device Management**: Controls hardware devices through drivers
- **File System Management**: Manages file operations, permissions
- **System Calls**: Provides interface between user applications and hardware

**Location:** `/boot/vmlinuz`

---

### B. Tools and Applications (2 Marks)

User-level programs and utilities that interact with the kernel through system calls. Includes:
- **System Utilities**: `ls`, `cp`, `mv`, `grep`, `find`
- **Network Tools**: `ping`, `ssh`, `curl`
- **Package Managers**: `apt`, `yum`, `dnf`
- **Office Tools**: LibreOffice
- **Web Browsers**: Firefox, Chrome

---

### C. Hardware Layer (H/W) (2 Marks)

Physical components of the computer system:
- **CPU** (Central Processing Unit)
- **RAM** (Random Access Memory)
- **Storage** (HDD, SSD, NVMe)
- **Network Interface Cards** (NIC)
- **Peripherals** (keyboard, mouse, display)

The kernel communicates directly with hardware through device drivers.

---

### D. Shell (2 Marks)

**Definition:** Command-line interface that interprets user commands and communicates with the kernel.

**Types of Shells:**
| Shell | Description |
|-------|-------------|
| **Bash** | Bourne Again Shell (most common) |
| **Zsh** | Z Shell (enhanced features) |
| **Fish** | Friendly Interactive Shell |
| **Sh** | Original Bourne Shell |

**Shell Functions:**
- Command interpretation
- Scripting and automation
- Environment management
- Job control

---

## QUESTION 3: Linux Installation Methods (10 Marks)

### A. Virtual Machine (4 Marks)

**Description:** Installing Linux within a virtualized environment using hypervisor software.

**Process:**
1. Install virtualization software (VirtualBox, VMware, KVM)
2. Create new virtual machine
3. Allocate resources (CPU, RAM, disk space)
4. Mount ISO file and install
5. Install guest additions for better integration

**Advantages:**
- No dual-boot required
- Run multiple OS simultaneously
- Snapshot and rollback capabilities
- Safe for testing

**Disadvantages:**
- Performance overhead
- Requires sufficient host resources

---

### B. Dual Boot (2 Marks)

**Description:** Installing Linux alongside an existing operating system, choosing which to boot at startup.

**Process:**
1. Partition disk for Linux
2. Install Linux on new partition
3. Configure GRUB bootloader
4. Select OS at boot time

**Advantages:**
- Full hardware access (no virtualization overhead)
- Better performance

**Disadvantages:**
- Requires partitioning
- Only one OS can run at a time
- Bootloader configuration complexity

---

### C. Live CD/DVD/USB (2 Marks)

**Description:** Running Linux directly from removable media without installing to hard disk.

**Process:**
1. Download ISO file
2. Create bootable USB using tools like Rufus or `dd`
3. Boot from USB
4. Run in "Try" mode or install

**Advantages:**
- Test before installing
- Recovery and troubleshooting tool
- No permanent changes

**Disadvantages:**
- Slower performance
- Changes lost after reboot

---

### D. Wubi (Windows-based Ubuntu Installer) (2 Marks)

**Description:** Installer that allows Ubuntu to be installed within Windows without partitioning.

**Process:**
1. Download Wubi installer
2. Run installer on Windows
3. Select installation size and username
4. Reboot and choose Ubuntu from boot menu

**Advantages:**
- No partitioning required
- Easy uninstallation via Windows Add/Remove Programs

**Disadvantages:**
- Deprecated (no longer supported for newer Ubuntu versions)
- File system stored as file within Windows
- Performance limitations

---

## QUESTION 4: Linux File Filtering Commands (10 Marks)

### A. List Files Created in Specific Period (2.5 Marks)

```bash
# Files modified in the last 7 days
find /path/to/directory -type f -mtime -7

# Files created today
find /path/to/directory -type f -newermt "2024-03-15"

# Files created between two dates
find /path/to/directory -type f -newermt "2024-03-01" ! -newermt "2024-03-15"
```

---

### B. Display Files with Parameter and Line Numbers (2.5 Marks)

```bash
# Search for pattern with line numbers
grep -n "parameter" filename.txt

# Search in multiple files
grep -n "error" /var/log/*.log

# Recursive search with line numbers
grep -rn "pattern" /path/to/directory/
```

---

### C. Display Lines NOT Matching a Pattern (2.5 Marks)

```bash
# Exclude lines containing pattern
grep -v "pattern" filename.txt

# Exclude multiple patterns
grep -v -e "pattern1" -e "pattern2" filename.txt
```

---

### D. Count of Matching Lines (2.5 Marks)

```bash
# Count occurrences of pattern
grep -c "pattern" filename.txt

# Count lines containing pattern
grep "pattern" filename.txt | wc -l

# Count across multiple files
grep -c "pattern" *.log
```

---

## QUESTION 5: Directory Structure & Permissions (10 Marks)

### A. Create Directory Structure (4 Marks)

```bash
# Create nested directory structure
mkdir -p project/docs
mkdir -p project/src
mkdir -p project/tests
mkdir -p project/users

# Create files
touch project/docs/readme.txt
touch project/src/main.py
touch project/src/utils.py
touch project/tests/test_main.py
```

### B. Delete "users" Directory (3 Marks)

```bash
# Delete empty directory
rmdir project/users

# OR delete directory with contents
rm -rf project/users
```

---

### C. Assign Permissions (3 Marks)

```bash
# On management directory
# User: read, write, execute (7)
# Group: read only (4)
# Others: write and execute (3)

chmod 743 management_directory

# Explanation:
# 7 = 4+2+1 (rwx) for user
# 4 = 4 (r--) for group
# 3 = 2+1 (-wx) for others

# Alternative symbolic method:
chmod u=rwx,g=r,o=wx management_directory
```

**Permission Values:**

| Value | Permission | Binary |
|-------|------------|--------|
| 7 | rwx | 111 |
| 6 | rw- | 110 |
| 5 | r-x | 101 |
| 4 | r-- | 100 |
| 3 | -wx | 011 |
| 2 | -w- | 010 |
| 1 | --x | 001 |
| 0 | --- | 000 |

---

## QUESTION 6: Linux File Types (10 Marks)

### A. General/Ordinary Files (2.5 Marks)

**Description:** Regular files containing text, data, programs, or binary information.

**Examples:**
- Text files: `.txt`, `.conf`, `.log`
- Executable files: `.bin`, `.sh`
- Data files: `.csv`, `.json`, `.xml`

**Identification:**
```bash
# Show file type
file filename.txt
ls -l filename.txt  # Shows - as first character
```

---

### B. Directory Files (2.5 Marks)

**Description:** Files that contain lists of other files and directories; act as containers.

**Examples:**
- `/home/`
- `/etc/`
- `/var/log/`

**Identification:**
```bash
ls -ld /home  # Shows d as first character
```

---

### C. Device/Special Files (2.5 Marks)

**Description:** Files representing hardware devices; used for I/O operations.

**Types:**
| Type | Character | Example | Description |
|------|-----------|---------|-------------|
| Character Device | `c` | `/dev/tty` | Serial devices (keyboard, terminal) |
| Block Device | `b` | `/dev/sda` | Storage devices (hard drives, USB) |

**Identification:**
```bash
ls -l /dev/sda   # Shows b (block device)
ls -l /dev/tty   # Shows c (character device)
```

---

### D. Hidden Files (2.5 Marks)

**Description:** Files starting with a dot (`.`) that are not displayed in normal directory listings.

**Examples:**
- `.bashrc` - Bash configuration
- `.gitconfig` - Git configuration
- `.ssh/` - SSH keys and config

**Commands:**
```bash
# Show hidden files
ls -a
ls -la

# Create hidden file
touch .hiddenfile

# View hidden files
ls -la | grep "^\."
```

