 Common Network Security Threats

 1. Introduction

Network security threats are a major concern for organizations because modern businesses, educational institutions, governments, and individuals depend heavily on interconnected systems and Internet-based services. An attack against a network can interrupt services, expose sensitive information, redirect users to malicious infrastructure, or allow attackers to manipulate communications. Threats such as Distributed Denial-of-Service (DDoS), Man-in-the-Middle (MITM), IP spoofing, and DNS poisoning exploit different weaknesses in network communication and infrastructure. Effective network security therefore requires multiple layers of protection, including secure network architecture, traffic filtering, encryption, authentication, monitoring, and appropriate incident-response procedures.

---

 2. DoS/DDoS Attacks

 2.1 What is a DoS/DDoS Attack?

A Denial-of-Service (DoS) attack attempts to make a system, application, or network service unavailable to legitimate users by exhausting its resources or overwhelming it with malicious requests.

A Distributed Denial-of-Service (DDoS) attack performs the same basic objective using multiple systems or devices, often a compromised botnet. Because traffic originates from many sources, DDoS attacks can be much more difficult to filter than attacks from a single source.

 2.2 How the Attack Works

A typical DDoS attack follows this general process:

1. The attacker compromises or gains control of multiple Internet-connected devices.
2. These devices become part of a botnet.
3. The attacker instructs the botnet to send large amounts of traffic or requests toward a target.
4. The target's bandwidth, network devices, server resources, or application capacity become exhausted.
5. Legitimate users experience slow responses, errors, or complete service unavailability.

DDoS attacks can use several techniques, including volumetric traffic floods, protocol attacks, and application-layer requests. Reflection and amplification attacks can also abuse legitimate third-party services to generate a larger volume of traffic toward the victim.

 2.3 Real-World Example: Dyn/Mirai DDoS Attack

On October 21, 2016, DNS infrastructure provider Dyn was targeted by a large-scale DDoS attack. The attack generated malicious traffic from a very large number of IP addresses and disrupted Dyn's DNS services.

Because Dyn provided DNS services for many major websites, the consequences extended beyond Dyn itself. Users experienced difficulty accessing services including Twitter, Reddit, Spotify, the New York Times, and other websites.

Security researchers linked a significant portion of the attack traffic to the Mirai IoT botnet, which consisted of compromised Internet-connected devices such as cameras and routers. The incident demonstrated how poorly secured IoT devices could be combined into a large botnet and used against critical Internet infrastructure.

Source: WIRED, "What We Know About Friday's Massive East Coast Internet Outage" (2016).

 2.4 Impact

The potential effects of DoS/DDoS attacks include:

* Website and application downtime
* Loss of availability of critical services
* Business and financial losses
* Increased infrastructure and mitigation costs
* Reduced customer confidence
* Disruption of dependent services
* Diversion of security teams while other attacks may be attempted

The Dyn incident demonstrated that attacking an important infrastructure provider can create collateral effects for many unrelated organizations that depend on that provider.

 2.5 Mitigation Strategies

 1. Use DDoS protection and traffic filtering

Organizations can use dedicated DDoS protection services, filtering infrastructure, firewalls, and other traffic-management mechanisms to identify and discard malicious traffic before it consumes critical resources.

 2. Coordinate with upstream network providers

Large attacks can exceed the capacity of an organization's own Internet connection. Organizations should maintain an established incident-response relationship with their ISP or upstream provider so malicious traffic can be filtered, rate-limited, or redirected upstream.

 3. Apply rate limiting and monitor network traffic

Rate limiting can restrict excessive requests to network services and applications. Continuous monitoring of traffic volume, source addresses, protocol behavior, CPU usage, and service availability can help identify attacks and support rapid response.

CISA recommends understanding the nature of the attack, analyzing traffic, working with service providers, applying filtering measures, and continuing to monitor other network assets during an attack.

 2.6 Key Security Lesson

DDoS protection should not focus only on individual servers. Organizations should also protect the network infrastructure and external services on which their applications depend.

---

 3. Man-in-the-Middle (MITM) Attacks

 3.1 What is a MITM Attack?

A Man-in-the-Middle (MITM) attack occurs when an attacker positions themselves between two parties that believe they are communicating directly. The attacker may observe, capture, relay, or modify traffic between the parties.

MITRE ATT&CK refers to this broader technique as Adversary-in-the-Middle (T1557). Techniques that can help an attacker establish this position include ARP cache poisoning, DHCP spoofing, name-resolution poisoning, and rogue wireless access points.

 3.2 How the Attack Works

A simplified MITM attack can occur as follows:

1. The attacker gains a position on or near the victim's network communication path.
2. The attacker manipulates network protocols or configuration so traffic is routed through the attacker's system.
3. The victim sends traffic believing it is communicating with the legitimate destination.
4. The attacker intercepts the communication.
5. Depending on the protections in place, the attacker may read, modify, replay, or forward the traffic to the legitimate destination.

For example, ARP cache poisoning can cause a victim device to associate the attacker's MAC address with the IP address of another system. This can redirect local network traffic through the attacker.

 3.3 Real-World Example: DigiNotar Certificate Compromise

In 2011, Dutch certificate authority DigiNotar was compromised. Attackers obtained hundreds of fraudulent digital certificates, including a certificate for Google.

A fraudulent Google certificate was subsequently observed in use and could enable an attacker to impersonate a legitimate Google service and conduct a man-in-the-middle attack against Gmail traffic.

The incident had serious consequences for DigiNotar's trustworthiness. Major browser vendors, including Google, Mozilla, and Microsoft, moved to block DigiNotar's certificates.

Source: WIRED, "DigiNotar Files for Bankruptcy in Wake of Devastating Hack" and related reporting (2011).

 3.4 Impact

MITM attacks can result in:

* Theft of usernames and passwords
* Theft of session cookies or access tokens
* Exposure of confidential information
* Manipulation of transmitted information
* Redirection to malicious websites
* Unauthorized access to systems
* Loss of trust in network infrastructure

The exact impact depends heavily on whether communications are properly encrypted and authenticated.

 3.5 Mitigation Strategies

 1. Use properly configured TLS/HTTPS

Encryption and certificate validation make it significantly harder for an attacker to successfully impersonate a legitimate service or read protected application traffic.

Organizations should ensure that certificates are valid, trusted, correctly configured, and not accepted when certificate validation fails.

 2. Reduce local-network attack opportunities

Organizations can use network segmentation, secure switch configurations, port security, and protected wireless networks to reduce opportunities for attackers to position themselves inside trusted network segments.

 3. Disable insecure name-resolution protocols where possible

Protocols such as LLMNR can be abused for name-resolution poisoning and credential theft. CISA recommends disabling LLMNR where it is not required and using network segmentation when it cannot be disabled.

Network monitoring should also be used to identify unusual ARP, DNS, DHCP, or authentication behavior.

 3.6 Key Security Lesson

Encryption alone is not sufficient if users and systems do not properly authenticate the endpoints they are communicating with. Network segmentation, secure protocols, certificate validation, and monitoring should work together.

---

 4. IP Spoofing

 4.1 What is IP Spoofing?

IP spoofing is the practice of modifying a network packet so that its source IP address appears to belong to another system.

The important distinction is that spoofing an IP address does not automatically give the attacker control over the legitimate system associated with that address. Instead, the attacker is falsifying the source identity contained in network packets.

IP spoofing is commonly used as part of other attacks, particularly reflection/amplification attacks and some forms of network reconnaissance or traffic manipulation.

 4.2 How the Attack Works

A simplified example is:

1. The attacker creates a network packet.
2. Instead of using the attacker's actual source IP address, the attacker places another address in the source field.
3. Network devices forward the packet based primarily on its destination.
4. The receiving system sees the forged source address.
5. Depending on the protocol and network configuration, the response may be sent toward the spoofed address.

Spoofing can be particularly useful in reflection attacks. In such attacks, the attacker sends requests to third-party servers while forging the victim's IP address as the source. The third-party servers then send their responses toward the victim.

 4.3 Real-World Example: Mirai-Related DDoS and Reflection Attacks

IP address spoofing has been used extensively in large-scale DDoS and reflection/amplification attacks. CISA's guidance on UDP-based amplification attacks specifically recommends ingress filtering to block spoofed packets and discusses the use of spoofed source addresses in reflected traffic.

The 2016 Dyn attack also illustrates the broader relationship between botnets, distributed traffic, and attacks against Internet infrastructure, although the Dyn incident should not be described as simply an "IP spoofing attack." IP spoofing is a technique that can be used within particular DDoS/reflection attack scenarios.

 4.4 Impact

IP spoofing can:

* Hide the true source of network traffic
* Make incident investigation more difficult
* Enable reflection/amplification attacks
* Circumvent poorly designed source-address trust mechanisms
* Facilitate certain denial-of-service attacks
* Make malicious traffic appear to originate from another network

It is important to note that modern security systems should not treat a packet's source IP address as sufficient proof of identity.

 4.5 Mitigation Strategies

 1. Implement Source Address Validation

Network operators can validate whether packets entering or leaving a network use source addresses that are legitimate for that interface or network.

NIST recommends Source Address Validation (SAV) as an important mechanism for preventing IP address spoofing.

 2. Use ingress and egress filtering

Routers and firewalls can use access control rules to block packets containing source addresses that should not legitimately appear on a particular network interface.

Ingress filtering can prevent spoofed packets from entering a network, while egress filtering can reduce the ability of internal compromised systems to send traffic using forged source addresses.

 3. Use uRPF and appropriate routing controls

Unicast Reverse Path Forwarding (uRPF) can help verify whether a packet's source address is reachable through an expected interface. NIST identifies uRPF alongside source-address validation and filtering as useful mechanisms for reducing IP spoofing.

 4.6 Key Security Lesson

IP addresses should be treated as routing information rather than complete proof of identity. Network security controls should validate traffic at network boundaries instead of blindly trusting source addresses.

---

 5. DNS Poisoning/Spoofing

 5.1 What is DNS?

The Domain Name System (DNS) translates human-readable domain names such as `example.com` into IP addresses that computers use to communicate with servers.

Because DNS is involved in locating Internet services, manipulation of DNS information can redirect users and applications toward incorrect or malicious destinations.

NIST's current SP 800-81r3 explains that attacks against DNS infrastructure can threaten network operations and recommends protecting the integrity, availability, and authenticity of DNS services.

 5.2 How DNS Poisoning/Spoofing Works

DNS poisoning or spoofing occurs when an attacker causes a DNS resolver or DNS infrastructure to provide an incorrect DNS response.

A simplified attack can look like:

```text
User
  |
  | "bank.example"
  v
DNS Resolver
  |
  | Malicious / manipulated DNS response
  v
Incorrect IP address
  |
  v
Attacker-controlled server
```

If successful, the victim may connect to an attacker-controlled system while believing they are communicating with the legitimate service.

Attackers may attempt to manipulate DNS through compromised DNS servers, malicious DNS responses, compromised infrastructure, or other techniques that influence name resolution.

MITRE ATT&CK documents how compromised DNS infrastructure can allow adversaries to alter DNS records and redirect organizational traffic to attacker-controlled infrastructure.

 5.3 Real-World Example: DNS Infrastructure Compromise

A practical real-world category of DNS attacks involves attackers compromising DNS infrastructure and changing records so that legitimate domains resolve to attacker-controlled systems.

MITRE ATT&CK specifically documents the compromise of third-party DNS servers as a technique. Once an attacker gains control of such infrastructure, they may alter DNS records to redirect traffic and support credential theft or other malicious activity.

This illustrates why protecting DNS infrastructure is not simply a matter of protecting individual user computers. A compromised DNS server can affect many users and systems simultaneously.

 5.4 Impact

DNS poisoning or spoofing can lead to:

* Redirection to fake websites
* Credential theft
* Malware delivery
* Phishing
* Interception of communications
* Loss of access to legitimate services
* Manipulation of application traffic
* Large-scale organizational disruption

Because DNS is used by many applications, an attack on DNS infrastructure can have consequences across an entire organization.

 5.5 Mitigation Strategies

 1. Deploy DNSSEC

DNS Security Extensions (DNSSEC) provide cryptographic mechanisms that allow DNS data to be authenticated. DNSSEC helps users and resolvers determine whether DNS information has been digitally signed by the legitimate source.

NIST's current SP 800-81r3 specifically recommends protecting the integrity and authenticity of authoritative DNS information using DNSSEC.

 2. Secure authoritative and recursive DNS infrastructure

Organizations should keep DNS software updated, restrict administrative access, separate DNS roles where appropriate, use strong authentication, and minimize unnecessary exposure of DNS infrastructure.

Administrative changes to DNS records should also be logged and monitored.

 3. Monitor DNS activity and unexpected record changes

Organizations should monitor DNS queries, responses, configuration changes, and unusual domain-resolution patterns. Unexpected changes to important DNS records should trigger investigation.

Protective DNS services can also help identify and block known malicious domains and suspicious DNS activity.

 5.6 Key Security Lesson

DNS should be treated as a critical security component rather than merely an Internet "address book." Protecting DNS integrity and authenticity is essential because manipulation can redirect legitimate users toward attacker-controlled infrastructure.

---

 6. Comparison of Network Security Threats


| Threat | Attack Vector | Who Is at Risk? | Difficulty to Execute | Ease of Mitigation |
|---|---|---|---|---|
| DoS/DDoS | Flooding network, protocol, or application resources with malicious traffic or requests | Public-facing websites, APIs, DNS providers, servers, and network infrastructure | Medium to High | Medium |
| MITM | Intercepting or manipulating communication between two parties using techniques such as ARP poisoning, DHCP spoofing, DNS manipulation, or rogue access points | Users, organizations, wireless networks, internal networks, and applications | Medium to High | Medium |
| IP Spoofing | Forging the source IP address in network packets | Networks and services that trust source addresses; DDoS targets | Medium | Medium |
| DNS Poisoning/Spoofing | Manipulating DNS responses, records, or DNS infrastructure to redirect users to incorrect or malicious destinations | Users, organizations, applications, websites, and DNS-dependent services | Medium to High | Medium |
             

### Comparison Note

The difficulty and mitigation ratings are qualitative rather than universal measurements. Actual difficulty depends on the attacker's resources, the target's architecture, network exposure, existing security controls, and whether the attacker already has access to the target environment.



 Important comparison note

The difficulty and mitigation ratings above are qualitative rather than universal measurements. Actual difficulty depends on the attacker's resources, the target's architecture, network exposure, security controls, and whether the attacker has already obtained privileged access.

---

 7. Conclusion

Network administrators should remember three key lessons:

 1. Protect availability as well as confidentiality

DDoS attacks demonstrate that a system can be secure from unauthorized access and still fail because its availability is attacked. Network administrators should prepare DDoS response procedures, traffic controls, monitoring, and upstream-provider coordination before an incident occurs.

 2. Never rely on a single trust mechanism

IP addresses, DNS responses, network locations, and local network protocols should not automatically be treated as proof of identity. Strong encryption, authentication, segmentation, source-address validation, and secure protocol configurations provide multiple layers of defense.

 3. Monitor critical network infrastructure continuously

DNS servers, routers, firewalls, wireless infrastructure, and other network components are security-critical assets. Unexpected DNS changes, abnormal traffic, suspicious network routing, and unusual authentication or ARP/DHCP activity can provide early indicators of compromise.

A layered defense strategy combining secure configuration, preventive controls, continuous monitoring, and a tested incident-response process provides stronger protection than relying on any single security technology.

---

 8. References

1. National Institute of Standards and Technology (NIST). SP 800-81 Rev. 3: Secure Domain Name System (DNS) Deployment Guide. March 19, 2026.
   https://csrc.nist.gov/pubs/sp/800/81/r3/final

2. National Institute of Standards and Technology (NIST). SP 800-189: Resilient Interdomain Traffic Exchange: BGP Security and DDoS Mitigation.
   https://csrc.nist.gov/pubs/sp/800/189/final

3. Cybersecurity and Infrastructure Security Agency (CISA), FBI, and MS-ISAC. Understanding and Responding to Distributed Denial-of-Service Attacks.
   https://www.cisa.gov/sites/default/files/publications/understanding-and-responding-to-ddos-attacks_508c.pdf

4. Cybersecurity and Infrastructure Security Agency (CISA). UDP-Based Amplification Attacks.
   https://www.cisa.gov/ncas/alerts/ta14-017a

5. MITRE ATT&CK. Adversary-in-the-Middle — Technique T1557.
   https://attack.mitre.org/techniques/T1557/

6. MITRE ATT&CK. Compromise Infrastructure: DNS Server — T1584.002.
   https://attack.mitre.org/techniques/T1584/002/

7. SANS Institute. Introduction to IP Spoofing.
   https://www.sans.org/white-papers/959/

8. Newman, L. H. What We Know About Friday's Massive East Coast Internet Outage. WIRED, October 21, 2016.
   https://www.wired.com/2016/10/internet-outage-ddos-dns-dyn/

9. Zetter, K. DigiNotar Files for Bankruptcy in Wake of Devastating Hack. WIRED, September 20, 2011.
   https://www.wired.com/2011/09/diginotar-bankruptcy/

10. Zetter, K. Google Certificate Hackers May Have Stolen 200 Others. WIRED, August 31, 2011.
    https://www.wired.com/2011/08/diginotar-breach/
