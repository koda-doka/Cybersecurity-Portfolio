# Travel Agency Server Flood Analysis

This project is based on a fictional travel agency whose employees rely on the company website to look up promotional vacation packages for customers. One afternoon, the organization's monitoring system reported abnormal behavior on the web server. When attempting to load the site, users received connection timeout errors instead of the expected webpage. A Wireshark packet capture revealed a surge of TCP SYN packets coming from an unfamiliar sourse, overwhelming the server's ability to comple TCP handshakes.

My role is to examine the symptoms, interpret the network traffic, and identify the type of attack affecting the server. Using the packet capture and sceanrio details, I will determine how the attack disrupted normal operations. 

# Incident Report

> Example logs provided in the exercise:
>
> 110	17.590783	203.0.113.0	192.0.2.1	TCP	54770->443 [SYN] Seq=0 Win=5792 Len=0...
>
> 111	18.413795	203.0.113.0	192.0.2.1	TCP	54770->443 [SYN] Seq=0 Win=5792 Len=0...
>
> 112	18.436807	203.0.113.0	192.0.2.1	TCP	54770->443 [SYN] Seq=0 Win=5792 Len=0...
>
> 113	18.459819	203.0.113.0	192.0.2.1	TCP	54770->443 [SYN] Seq=0 Win=5792 Len=0...

**Part 1: Identify the type of attack that may have caused this network inerruption**

The reason why the website is displaying a conneciton timeout error message is that the server is being overloaded from an unknown source. The Wireshark logs show that an attacker has targeted the server by continuously sending SYN packets to prevent the server from completing the TCP handshake. This is a classic example of a DosS attack known as SYN flooding.

**Part 2: Explain how the attack is causing the webstie to malfunction**

When users visit the webstie, a three-way handshake occurs using the TCP protocol to establish a connection. That handshake looks like this:

1. SYN - A client sends a SYN packet to the server, requesting a connection.

2. SYN, ACK - The server receives the request and replies with a SYN-ACK packet to accept the request. The server will reserve resources for the client to connect.

3. ACK - The client sends a final ACK packet to the server, establishing a connection.

SYN flooding is when a malicious actor sends a large numer of SYN packets all at once, overwhelming a server's available resources. This results in clients being unable to establish a new session because there are no resources left for TCP connections. From the logs, it is clear that the web server has reached capacity and is no longer able to process legitimate SYN requests. When a client tries access the website, the server responds with a timeout error because it is unable to open a new connection.
