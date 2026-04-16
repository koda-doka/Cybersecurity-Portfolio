# Recipe Site Outage Analysis

This project is a mock analysis based on a fictional client whose customers reported that their website, yummyrecipiesforme.com, was suddenly unreachable. Visitors attempting to load the page received a "destination port unreachable" error instead of the expected content. The issue appeared to affect multiple users, suggesting a broader network or service disruption rather than an isolated problem.

As the cybersecurity analyst assigned to investigate, my role was to determine which network protocol was impacted and why the website could not be reached. The scenario describes how a browser first performs a DNS lookup using UDP before attempting an HTTPS connection, and how the system responded with ICMP messages indicating that UDP traffic to port 53 was unreachable. Based on this information, my task was to analyze the symptoms, interpret the network behavior, and identify the protocol responsible for the outage.

# Incident Report

> Example logs provided in the exercise:
>
> 13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipiesforme.com. (24)
>
> 13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

**Part 1: Provide a summary of the problem found in the DNS and ICMP traffic log**

The UDP protocol reveals that the packet was undeliverable to port 53 of the DNS server. Based on the results of the network analysis, the ICMP error message indicated that UDP port 53 is unreachable. The port noted in the error message is used for DNS, which translates internet domain names into IP addresses. The most likely issue is that the DNS server is unavailable. The service is either not running, the port is closed, or a firewall is blocking UDP traffic to port 53.

**Part 2: Explain your analysis of the data and provide at least one cause of the incident**

This incident occurred around 1:24 PM. Several clients reported that they could not reach the webpage, which was brought to the attention of the IT team immediately. The IT department first recreated the issue by trying to load the webpage, which confirmed that the site was not responding on the server side. To troubleshoot the issue, the IT team used tcpdump to determine the underlying cause as to why the site is not responding. When trying to connect to the website, the DNS server rejected the request which resulted in an ICMP error. This led to the website not loading for any user. The most likely cause of the incident is a misconfiguration or failure on the DNS server that prevented it from accepting queries on port 53, resulting in an ICMP error response, making the website inaccessible.
