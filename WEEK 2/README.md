<div align="center">
  
## Penetration Testing  — Week 2

 FOOTPRINTING & NETWORK SCANNING STAGES

</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.2.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Aawishko%20De-C00000?style=flat-square" />
</p>



---
**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

### 👤 Aawishko De
**Cybersecurity Professional | Networkwalks Intern | Batch B083**

</div>

---

## 🛡️ 1. Engagement Overview

| Category | Details |
|---|---|
| **Pentester** | Aawishko De |
| **Program / Batch** | B083 – Networkwalks |
| **Date** | 17 September 2026 |
| **Modules** | W2-PM1 – Multiple Kali Tools; W2-PM5 – Zenmap Scanning |
| **Targets** | `networkwalks.com` (authorized) and my own local network |
| **Authorization** | Written permission / authorized educational scope |
| **Phases Covered** | Reconnaissance & Footprinting; Scanning & Network Discovery |
| **Platform** | Kali Linux |

> All activities were performed only within the authorized scope. No exploitation or vulnerability validation was carried out as part of these modules.

---

# 🔎 2. Overview

This report summarizes the Week 2 practical work completed during my Networkwalks cybersecurity internship.

The work covered two areas:

1. **Footprinting and reconnaissance** of `networkwalks.com`
2. **Network discovery** using Zenmap on my own local network

The main purpose was to understand how publicly available information and basic network responses can be collected during the early stages of a security assessment.

---

# 🛠️ 3. Tools Used

| Tool | Purpose |
|---|---|
| **WHOIS** | Collect domain registration and name-server information |
| **WhatWeb** | Identify web technologies and CMS information |
| **Nslookup** | Resolve the domain to an IP address |
| **cURL** | Inspect HTTP response headers |
| **Wafw00f** | Check for a Web Application Firewall |
| **DNSRecon** | Enumerate publicly accessible DNS records |
| **Zenmap / Nmap** | Discover live hosts on the local subnet |
| **ifconfig** | Identify the Kali network configuration |

---

# 🔍 4. Activities Performed

## 4.1 Footprinting & Reconnaissance

I used six Kali Linux tools to collect different types of publicly observable information from the authorized `networkwalks.com` target.

### WHOIS
Used to obtain basic domain registration information and identify relevant name-server details.

### WhatWeb
Used to fingerprint technologies exposed by the website. The results identified WordPress and WP Download Manager information.

### Nslookup
Used to resolve the domain name. The observed IP address was:

```text
192.232.216.135
```

### cURL
Used with the `-I` option to inspect HTTP response headers. The response also exposed the WordPress REST API path:

```text
/wp-json/
```

### Wafw00f
Used to identify whether a Web Application Firewall was present. The scan identified:

```text
ModSecurity (SpiderLabs)
```

### DNSRecon
Used to collect accessible DNS information, including name-server, mail-server, TXT/SPF and service-related records.

These activities helped me understand how different reconnaissance tools provide different pieces of information about the same target.

---

# 🌐 4.2 Network Scanning with Zenmap

For the network-scanning activity, I first checked the Kali network configuration and identified:

```text
Local IP:   10.0.2.15
LAN Subnet: 10.0.2.0/24
```

I then used Zenmap with a **Ping Scan** against the subnet:

```text
Target: 10.0.2.0/24
Command: nmap -sn 10.0.2.0/24
```

### Live Hosts Detected

The scan reported **3 hosts up**:

| IP Address | MAC Address shown by Nmap |
|---|---|
| `10.0.2.2` | `52:54:00:12:35:00` |
| `10.0.2.3` | `52:54:00:12:35:00` |
| `10.0.2.15` | Not displayed in the captured output |

The Zenmap topology view was also used to visualize the discovered network.

> The scan results above are from the actual Zenmap output used for this report. The addresses are not being presented as three physical PCs; they are the live hosts/addresses reported by the scan on the active subnet.

---

# ⚠️ 5. Risk Observations

The activities mainly produced reconnaissance and information-disclosure observations rather than confirmed vulnerabilities.

|  # | Observation                            | Evidence                                                   | Security Relevance                                                                                     |
| -: | -------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
|  1 | **Web technology information exposed** | WhatWeb identified WordPress and WP Download Manager       | Version information may assist further security research and vulnerability assessment.                 |
|  2 | **Public IP address identified**       | Nslookup resolved the domain to `192.232.216.135`          | Identifies the network address associated with the web service and can support infrastructure mapping. |
|  3 | **HTTP information exposed**           | cURL identified HTTP response information and `/wp-json/`  | Provides additional information about the web application and may assist further enumeration.          |
|  4 | **WAF identified**                     | Wafw00f detected ModSecurity (SpiderLabs)                  | Provides information about the defensive technology protecting the web application.                    |
|  5 | **DNS information available**          | DNSRecon identified DNS, mail and service-related records  | Helps build an overview of the publicly visible domain infrastructure.                                 |
|  6 | **Live hosts identified**              | Zenmap reported three live addresses on the scanned subnet | Provides visibility into active hosts on the local network.                                            |

**These observations do not by themselves prove that a vulnerability exists.** Further authorized testing would be required to validate any suspected security issue.

---

# 🛡️ 6. Recommendations

Based on the observations from these exercises:

1. Regularly review publicly exposed technology information.
2. Keep CMS platforms, plugins and other software updated.
3. Review HTTP headers for unnecessary technical information.
4. Periodically audit publicly accessible DNS records.
5. Keep WAF protections properly configured and monitored.
6. Perform authorized internal network discovery to maintain an accurate device inventory.
7. Investigate unknown or unexpected devices found during network scans.
8. Keep network documentation and topology records updated.
9. Always perform reconnaissance and scanning within an explicitly authorized scope.

---

# 📚 7. Key Learning Outcomes

During these activities, I gained practical experience with:

- Domain reconnaissance
- Web technology fingerprinting
- DNS enumeration
- HTTP header inspection
- WAF identification
- Network discovery
- IP and MAC address identification
- Zenmap/Nmap scanning
- Network topology visualization
- Security finding documentation
- Authorized ethical hacking practices

The main takeaway was that useful security information can often be collected before any exploitation is attempted. I also learned the importance of recording the actual result of each command rather than treating reconnaissance findings as confirmed vulnerabilities.

---

# 📝 8. Conclusion

During Week 2 of my Networkwalks cybersecurity internship, I completed practical exercises covering footprinting, reconnaissance and network scanning.

The reconnaissance activities helped me understand how tools such as WHOIS, WhatWeb, Nslookup, cURL, Wafw00f and DNSRecon can be used to collect different types of information about a web target.

I also used Zenmap to identify my local network configuration and discover live hosts on the `10.0.2.0/24` subnet. The scan reported three live addresses, and the available MAC address information was recorded from the Nmap output.

Overall, the exercises gave me a better understanding of the early stages of a penetration test and the importance of working within an authorized scope. They also helped me practice documenting technical observations in a clear and structured way.

---

# 📸 9. Evidence

Add the corresponding screenshots from the practical work below.

<details>
<summary><b>WHOIS</b></summary>

![](WHOIS.PNG)

</details>

<details>
<summary><b>WhatWeb</b></summary>

![](WHATWEB.PNG)

</details>

<details>
<summary><b>Nslookup</b></summary>

![](NSLOOKUP.PNG)

</details>

<details>
<summary><b>cURL</b></summary>

![](cCURL.PNG)

</details>

<details>
<summary><b>Wafw00f</b></summary>

![](WAFW00F.PNG)

</details>

<details>
<summary><b>DNSRecon</b></summary>

![](DNSRECON.PNG)
</details>

<details>
<summary><b>Zenmap Ping Scan</b></summary>

![](ZENMAP_PING_SCAN.PNG)

</details>

<details>
<summary><b>Zenmap Network Topology</b></summary>

![](ZENMAP_TOPOLOGY.PNG)
</details>

---

# 👤 Author

**Aawishko De**

Cybersecurity Professional | Networkwalks Intern | Batch B083

**Project:** W2-PM-FINAL  
**Week:** 02  
**Program:** Cybersecurity – Networkwalks  
**Date:** September 2026

---

<div align="center">

### 🛡️ CYBERSECURITY • ETHICAL HACKING • NETWORK SECURITY

**Learn → Practice → Analyze → Secure**

</div>
