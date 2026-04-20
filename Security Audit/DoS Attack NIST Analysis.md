# DoS Security Strategy Using the NIST Framework

This report applies the NIST cybersecurity framework to develop a structured incident response and security improvement plan based on a simulated DoS attack scenario.

# Incident Report

**Summary:** A multimedia company recently experienced a DoS attack, which compromised its internal network and prevented users from accessing critical services. During the attack, the organization's servers stopped responding due to an overwhelming amount of incoming ICMP packets. The security team responded by blocking the incoming traffic and restoring the network. Further investigation revealed that the flooding attack was able to occur through an unconfigured firewall. New network hardening techniques were applied to prevent future incidents from happening.

**Identify:** This incident was an ICMP DoS attack caused by an unconfigured firewall, which allowed unrestricted ICMP traffic into the internal network. The internal network, critical business systems and services, and network devices responsible for internal communication were affected for two hours. Not only were employees unable to access shared resources, disrupting normal business operations, but customers were also unable to access the company's services. There was also an increased risk of further exploitation due to the firewall misconfiguration.

**Protect:** To strengthen the organization's defenses, several systems and procedures need to be updated. All firewalls need to have properly configured rulesets, including ICMP rate limiting and source IP verification. Networks should be monitored for abnormal traffic on a regular basis. It is also best to incorporate an IDS/IPS system to filter network traffic to better detect and prevent further attacks. 

**Detect:** Several network and security tools should be used to monitor and protect the network. The security team should have a SIEM tool to aggregate and analyze network logs. An IDS to monitor incoming traffic for suspicious patterns and an IPS to automatically block malicious traffic should be added to the network. Establishing baseline network behavior and configuring alerts for deviations will help identify unusual ICMP spikes or unauthorized access attempts more quickly.

**Respond:** The incident management team was able to block incoming ICMP packets to restore critical network services while the security team continued to investigate. Future response efforts should include isolating affected segments, collecting relevant logs and packet captures for analysis, and updating firewall rules immediately when abnormal traffic is detected.

**Recover:** Critical systems were brought back online first, followed by non-essential services once the network was stable. Recovery efforts should also include verifying system integrity, reviewing backup status, documenting lessons learned, and updating response procedures to improve resilience against similar attacks.
