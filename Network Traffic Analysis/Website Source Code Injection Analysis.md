# Recipe Site Brute-Force Compromise Report

In this scenario, we revisit the fictional yummyrecipiesforme.com website that has been under attack once again. Several customers reported that the site unexpectedly prompted them to download a file before accessing recipes. After running the file, their browsers redirected to a different website and their computers began running slowly. These symptoms suggested that the legitimate site had been altered and was distributing malware.

A disgruntled former employee performed a brute-force attack against the website's hosting account, eventually guessing the default administrative password. With access to the admin panel, they modified the site's source code, embedded malicious JavaScript, and locked out the site owner. My role in this scenario is to investigate the suspicious behavior by analyzing tcpdump data and documenting how the attacker compromised the site.

# Incident Report

> Example tcpdump logs provided in the exercise:
>
> 14:18:36.786589 IP your.machine.36086 > yummyrecipesforme.com.http: Flags [P.], seq 1:74, ack 1, win 512, options [nop,nop,TS val 3302576859 ecr 3302576859], length 73: HTTP: GET / HTTP/1.1
>
> 14:18:36.786595 IP yummyrecipesforme.com.http > your.machine.36086: Flags [.], ack 74, win 512, options [nop,nop,TS val 3302576859 ecr 3302576859], length 0
>
> 14:20:32.192571 IP your.machine.52444 > dns.google.domain: 21899+ A? greatrecipesforme.com. (24)
>
> 14:20:32.204388 IP dns.google.domain > your.machine.52444: 21899 1/0/0 A 192.0.2.17 (40)

**Part 1: Identify the network protocol involved in the incident**

The attacker modified the website's source code, and that altered content is delivered to users through the HTTP response when the browser loads the page. Running tcpdump while accessing the site shows the browser sending an HTTP GET request to the legitimate server. That request retrieves the compromised webpage, which contains the injected JavaScript responsible for prompting the download and triggering the redirect. Because the malicious behavior is delivered through the webpage itself, HTTP is the most significant protocol in this incident.

**Part 2: Document the incident**

Multiple customers emailed the site's helpdesk and reported that they had been prompted to download and run a file to access free recipes. Their personal computers began running slowly after executing the file. In an attempt to address the situation, the website owner tried to log into the server but noticed that they were locked out of their account.

This was brought to the attention of the security team, and one of the analysts created a sandbox to observe the suspicious website behavior. By using tcpdump, the analyst was able to capture network traffic and download the malicious file without compromising the company network. Reviewing the network traffic revealed that the site redirected users to greatrecipesforme.com.

A senior cybersecurity professional confirmed that the website was compromised by analyzing the source code. The analyst discovered that JavaScript had been added to prompt visitors to download a file. The team believes the attacker performed a brute force attack to access the administrator account and then changed their password.

**Part 3: Recommend one remediation for brute force attacks**

There are several security measures that the site can implement to protect against brute force attacks. A password policy would prevent employees, and the administrator, from using generic passwords that are easy to guess. The attacker was able to gain access to the website by guessing generic passwords, which led to the incident. Setting up two-factor authentication prevents unauthorized users from accessing the system by requiring a one-time code in addition to their password. Adding these measures will improve the website's overall security posture by reducing the likelihood of unauthorized access and preventing attackers from easily guessing weak credentials.
