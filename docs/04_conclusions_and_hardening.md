# Phase 4: Final Evaluation & Hardening Ideas

## Lab Assessment
By combining network-level detection with host-level firewall automation, the layered security system successfully defended the target environment. The final metrics are evaluated below against our core security framework:

| Simulated Attack Vector | Tooling Used | Layered Defensive System | Mitigation Outcome | CIA Triad Validation |
| :--- | :--- | :--- | :--- | :--- |
| **Network Scanning** | `nmap` | **Snort IDS Engine** | Logged the attacker's footprint and triggered real-time traffic alerts. | **Integrity Maintained:** Complete situational awareness of the setup. |
| **Brute-Force Login** | `hydra` | **Fail2Ban Daemon** | Monitored auth logs and automatically injected an IP ban after the 3rd attempt. | **Confidentiality Secured:** Unauthorized list access cut off completely. |
| **Volumetric Traffic Flood** | Layer 4 Flooder | **IPTables Firewall** | Throttled network packet rates, keeping system processing queues stable. | **Availability Secured:** The core Apache web service remained up and responsive. |

## Core Takeaways
1.  **Automation Saves Networks:** Manually reviewing logs to block an attacker takes way too long. Automated analysing tools reduce the threat mitigation window down to a few seconds.
2.  **Defenses Must Be Layered:** Firewalls alone cannot stop valid protocol traffic like SSH connection attempts. Combining log monitoring with dynamic firewall adjustments stops smart attacks.

## Production Hardening Recommendations
To upscale this virtual design to an enterprise standard, the following steps should be taken:
*   **Central Log Infrastructure:** Ship all Snort alerts and system logs securely to a centralized logging server (like Wazuh or ELK) to preserve logs even if the target host is compromised.
*   **Implement Key-Based Authentication:** Disable password authentication entirely for SSH services across all servers. Enforcing cryptographic keys stops dictionary brute-force attacks at the source.
