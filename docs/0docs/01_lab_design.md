# Phase 1: Lab Design & Specifications

## Design Objectives
Relying on a single firewall or security tool leaves a network highly vulnerable. This project focuses on building a "defense-in-depth" architecture inside a virtual lab. By running specific attack scenarios, we can see exactly how vulnerabilities are exploited, how security logs are generated, and how defense tools can use those logs to take action.

### The CIA Triad and Defense Mapping
To keep the project focused on clear engineering goals, every attack and defensive control is mapped directly to the CIA Security Triad:

| Triad Component | Monitored Risk | Defensive Security Tool | Expected Engineering Outcome |
| :--- | :--- | :--- | :--- |
| **Confidentiality** | SSH Brute-Force Password Cracking | Fail2Ban Engine + Log Parsing | Malicious IPs are jailed via the firewall after 3 failed login attempts. |
| **Integrity** | Network Scanning & Service Discovery | Snort IDS Real-Time Signature Alerts | Unauthorized network scans trigger immediate alert flags for analysis. |
| **Availability** | Denial-of-Service (DoS) Flooding | IPTables Firewall Throttling Rules | Traffic spikes are controlled so the core web server stays online. |

## Lab Setup and Host Configurations
The entire lab is completely isolated inside VMware Workstation using a custom host-only network (`192.168.160.0/24`). This guarantees that no traffic can bleed out into a live, production network.

### Hardware and Operating System 

| Machine Role | Operating System | Base Memory | Configured Services / Tools Used | IP Address |
| :--- | :--- | :--- | :--- | :--- |
| **Attacker** | Parrot OS | 2048 MB | `nmap`, `hydra`, Network Flooding Tools | `192.168.160.134` |
| **Target** | Ubuntu Server | 2048 MB | `sshd`, Apache `httpd`, Snort (v2.9), Fail2Ban | `192.168.160.135` |

![VMware Configuration](../images/vmware_config.png)
*Figure 1.1: Verification of the isolated virtual machine setup inside VMware Workstation.*
