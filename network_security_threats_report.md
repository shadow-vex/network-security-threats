# Research Report: Common Network Security Threats

**Author:** Sathya V
**Domain:** Network Security / Cybersecurity
**Format:** Research Report
**Repository:** `network-security-threats`
**Status:** Completed

## 1. Introduction

Network security threats are a major concern for organizations because modern businesses depend heavily on interconnected systems, cloud services, web applications, DNS infrastructure, and remote access. Attackers can exploit weaknesses in network protocols and configurations to disrupt services, intercept communications, impersonate legitimate systems, or redirect users to malicious destinations. These attacks can affect the **confidentiality, integrity, and availability (CIA)** of information systems. Understanding common network threats and applying appropriate defensive controls is therefore essential for network administrators and security teams.

# 2. DoS / DDoS Attacks

## 2.1 What is a DoS Attack?

A **Denial-of-Service (DoS)** attack attempts to make a system, application, or network service unavailable to legitimate users.

The attacker typically generates excessive traffic or requests that consume the target's available:

* Network bandwidth
* CPU resources
* Memory
* Connection tables
* Application resources

A **Distributed Denial-of-Service (DDoS)** attack uses multiple compromised systems, commonly called a **botnet**, to generate traffic from many sources simultaneously.

MITRE ATT&CK identifies Network Denial of Service as **T1498**, including direct network flooding and reflection/amplification attacks.

## 2.2 How DDoS Works

A typical DDoS attack follows this general process:

Attacker
   |
   v
Compromised Devices / Botnet
   |
   +--------+--------+--------+
   |        |        |        |
   v        v        v        v
Massive malicious traffic
   |
   v
Target Network / Server
   |
   v
Service becomes slow or unavailable


Attackers may use compromised IoT devices, servers, routers, or other systems to generate large volumes of traffic.

## 2.3 Real-World Example — Dyn DDoS Attack

In October 2016, the DNS infrastructure provider **Dyn** was targeted by a major DDoS attack. The attack involved the **Mirai botnet**, which had compromised large numbers of Internet-connected devices such as cameras, routers, and DVRs.

The attack disrupted access to several major online services, including Twitter, Spotify, Reddit, and other websites for users in parts of the United States.

The incident demonstrated how vulnerable IoT devices can be combined into a large botnet and used to attack critical Internet infrastructure.

## 2.4 Impact

DDoS attacks can result in:

* Website and application downtime
* Loss of business revenue
* Service disruption
* Customer dissatisfaction
* Increased infrastructure costs
* Operational and reputational damage

## 2.5 Mitigation Strategies

### 1. DDoS Protection Services

Organizations can use specialized DDoS protection and traffic-scrubbing services to identify and filter malicious traffic before it reaches the protected infrastructure.

### 2. Rate Limiting and Traffic Filtering

Firewalls, load balancers, and application gateways can limit excessive requests and block suspicious traffic patterns.

### 3. Redundancy and Distributed Infrastructure

Using load balancing, CDN infrastructure, multiple network paths, and geographically distributed systems can reduce the effect of an attack against a single location.

# 3. Man-in-the-Middle (MITM) Attacks

## 3.1 What is a MITM Attack?

A **Man-in-the-Middle (MITM)** attack occurs when an attacker positions themselves between two communicating parties and intercepts or potentially modifies their communication.

NIST defines a MITM attack as an attack where the attacker is positioned between communicating parties to intercept and/or alter transmitted data.

MITRE ATT&CK categorizes this activity under **Adversary-in-the-Middle (T1557)**.

## 3.2 How MITM Works

A simplified attack scenario is:

User
  |
  | Communication
  v
Attacker
  |
  | Forward / Modify
  v
Legitimate Server

The attacker may use techniques such as:

* ARP cache poisoning
* DNS manipulation
* Rogue Wi-Fi access points
* DHCP spoofing
* Malicious proxies
* Certificate-related weaknesses

If successful, the attacker may observe credentials, session information, or other sensitive data.

## 3.3 Real-World Example — Lenovo Superfish

In 2015, security researchers discovered that some Lenovo consumer laptops had **Superfish** software pre-installed.

The software installed a trusted root certificate and intercepted HTTPS connections in order to inject advertisements. Because of weaknesses in its implementation, attackers could potentially exploit the same mechanism to intercept encrypted communications.

The incident demonstrated how weakening TLS certificate validation can create a serious MITM risk.

## 3.4 Impact

MITM attacks can cause:

* Credential theft
* Session hijacking
* Sensitive data exposure
* Modification of transmitted information
* Financial fraud
* Loss of privacy

## 3.5 Mitigation Strategies

### 1. Use Strong TLS / HTTPS

Applications should use properly configured TLS and reject invalid or unexpected certificates.

### 2. Secure Wireless Networks

Organizations should use strong Wi-Fi authentication and encryption, avoid untrusted public networks for sensitive activities, and deploy wireless intrusion prevention where appropriate.

### 3. Network Segmentation and Monitoring

Network segmentation can limit an attacker's ability to move through the environment. Monitoring DNS, ARP, DHCP, and unusual network configuration changes can also help identify MITM activity.

# 4. IP Spoofing

## 4.1 What is IP Spoofing?

**IP spoofing** occurs when an attacker modifies the source IP address of network packets so that the packets appear to originate from another system.

The spoofed address may represent:

* A trusted host
* Another organization
* An internal network
* A random or nonexistent address

IP spoofing is frequently used as part of DDoS attacks because it can make identifying the true traffic source more difficult.

## 4.2 How IP Spoofing Works

Normally:

Attacker IP  --->  Target

With spoofing:

Fake Source IP  --->  Target
       ^
       |
   Attacker


The packet contains a falsified source address.

In some attack scenarios, the attacker may use spoofing together with reflection/amplification techniques to cause third-party systems to send traffic toward the victim.

## 4.3 Real-World Use — DDoS Attacks

IP spoofing has been widely observed as a component of large-scale DDoS attacks. NIST notes that spoofed source addresses can be used to make filtering malicious traffic by origin more difficult.

The technique is particularly important in reflection-based attacks, where the attacker attempts to hide the actual origin of malicious traffic.

## 4.4 Impact

IP spoofing can lead to:

* Difficulty identifying attack sources
* Bypass of weak IP-based trust controls
* Reflection-based DDoS attacks
* Network monitoring challenges
* Abuse of trusted network relationships

## 4.5 Mitigation Strategies

### 1. Ingress and Egress Filtering

Network operators should implement ingress and egress filtering to prevent packets with invalid or unauthorized source addresses from entering or leaving networks.

### 2. Avoid IP Address as the Only Authentication Factor

Systems should not treat source IP addresses as sufficient proof of identity.

Use stronger authentication mechanisms such as:

* MFA
* Cryptographic authentication
* Certificates
* Secure tokens

### 3. Network Monitoring and Anti-Spoofing Controls

Routers, firewalls, and network monitoring systems should identify suspicious traffic patterns and enforce anti-spoofing policies.


# 5. DNS Poisoning / DNS Spoofing

## 5.1 What is DNS?

The **Domain Name System (DNS)** translates human-readable domain names such as:

example.com

into IP addresses used by computers to communicate.

Because DNS is fundamental to Internet communication, manipulating DNS responses can redirect users to malicious infrastructure.

## 5.2 What is DNS Poisoning?

**DNS poisoning**, also known as DNS cache poisoning, occurs when an attacker causes a DNS resolver or client to store or accept incorrect DNS information.


The victim believes they are communicating with the legitimate destination, but the DNS resolution has been manipulated.

## 5.3 Real-World Example — Sea Turtle

The **Sea Turtle** threat actor conducted DNS-related attacks involving compromise of DNS providers and registrars.

MITRE ATT&CK reports that Sea Turtle modified DNS records at service providers to redirect legitimate resources to attacker-controlled infrastructure. The attackers could then impersonate legitimate services and capture credentials.

This demonstrates that DNS manipulation can become a stepping stone to an adversary-in-the-middle attack.

## 5.4 Impact

DNS poisoning or spoofing can result in:

* Website redirection
* Credential theft
* Phishing
* Malware delivery
* Loss of user trust
* Service disruption
* Interception of sensitive communications

## 5.5 Mitigation Strategies

### 1. Deploy DNSSEC

**DNS Security Extensions (DNSSEC)** provide mechanisms for authenticating DNS information and protecting DNS data integrity.

Organizations should implement DNSSEC where appropriate for authoritative DNS infrastructure.

### 2. Secure DNS Infrastructure

DNS servers should be patched, securely configured, access-controlled, and monitored.

Administrative access to DNS management systems should also use strong authentication such as MFA.

### 3. Monitor DNS Changes

Organizations should monitor:

* Unexpected DNS record changes
* Name server changes
* Unusual DNS responses
* Unauthorized administrative activity
* Changes to authoritative DNS infrastructure

# 6. Comparison of Network Security Threats

| Threat                   | Attack Vector                       | Who Is at Risk?                                  | Difficulty to Execute | Ease of Mitigation |
| ------------------------ | ----------------------------------- | ------------------------------------------------ | --------------------- | ------------------ |
| DoS / DDoS               | Excessive malicious traffic         | Websites, servers, cloud services, DNS providers | Medium                | Medium             |
| MITM                     | Network interception / manipulation | Users, organizations, public Wi-Fi users         | Medium–High           | Medium             |
| IP Spoofing              | Forged source IP addresses          | Networks, servers, DDoS targets                  | Medium                | Medium             |
| DNS Poisoning / Spoofing | Manipulated DNS informat            | Users, DNS providers, organizations              | Medium-High           | Medium             |

# 7. Key Takeaways for Network Administrators
1. Protect Availability

Organizations should prepare for DDoS attacks using traffic filtering, rate limiting, redundancy, monitoring, and appropriate DDoS protection services.

2. Protect Communication Integrity

Strong TLS configuration, secure authentication, network segmentation, and monitoring can significantly reduce MITM risks.

3. Protect Network Trust Infrastructure

IP filtering, anti-spoofing controls, secure DNS administration, DNSSEC, and continuous monitoring are essential for protecting the network's underlying trust mechanisms.

# 8. Conclusion

Network security threats can affect every major security objective, including confidentiality, integrity, and availability. DoS/DDoS attacks primarily threaten availability, while MITM and DNS manipulation can compromise confidentiality and integrity. IP spoofing can support several other attacks by hiding or falsifying the apparent source of network traffic.

A strong network security strategy should therefore combine secure configuration, encryption, authentication, traffic filtering, network segmentation, monitoring, and incident response. No single security control can eliminate every threat; effective defense requires multiple layers of protection and continuous security monitoring.

# 9. References
NIST — Advanced DDoS Mitigation Techniques
https://www.nist.gov/programs-projects/advanced-ddos-mitigation-techniques
NIST — Guidelines on Firewalls and Firewall Policy (SP 800-41)
https://csrc.nist.gov/publications/detail/sp/800-41/rev-1/final
NIST — Man-in-the-Middle Attack Glossary
https://csrc.nist.gov/glossary/term/man_in_the_middle_attack
NIST — Secure Domain Name System (DNS) Deployment Guide, SP 800-81r3
https://www.nist.gov/news-events/news/2026/03/secure-domain-name-system-dns-deployment-guide-final-publication
MITRE ATT&CK — Network Denial of Service (T1498)
https://attack.mitre.org/techniques/T1498/
MITRE ATT&CK — Adversary-in-the-Middle (T1557)
https://attack.mitre.org/techniques/T1557/

# Research Summary

This report examined four major network security threats:

DoS/DDoS → MITM → IP Spoofing → DNS Poisoning/Spoofing

Understanding the attack mechanism, recognizing its impact, and applying layered security controls are essential for maintaining a secure and resilient network.
