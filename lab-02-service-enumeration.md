# Lab 02 — Service & Version Enumeration

**Tool:** Nmap  
**Date:** 2026 (Kali Linux training, Day 2–3)  
**Difficulty:** Foundational

---

## Situation

After identifying live hosts on a network, the next step in any reconnaissance phase
is determining what services are running and which versions are installed. Outdated or
misconfigured services are a primary attack surface in real-world engagements.
This lab focused on extracting detailed service information from a target host.

---

## Task

Perform service and version enumeration on a known live host to identify open ports,
running services, software versions, and operating system details.

---

## Action

```bash
# Service and version detection
nmap -sV 192.168.1.1

# OS fingerprinting
nmap -O 192.168.1.1

# Aggressive scan — OS, version, scripts, traceroute combined
nmap -A 192.168.1.1

# Scan all 65535 ports (not just top 1000)
nmap -p- 192.168.1.1

# Targeted port scan with version detection
nmap -sV -p 22,80,443 192.168.1.1
```

**Process:**
1. Ran `-sV` to probe open ports and identify service/version information
2. Ran `-O` separately to attempt OS fingerprinting
3. Used `-A` for a combined aggressive scan to see full host profile
4. Documented all open ports, associated services, and version strings
5. Noted any services running on non-standard ports as higher-priority findings

---

## Result

- Identified all open ports and their associated services
- Retrieved version strings for running services (e.g. OpenSSH 8.x, Apache 2.4.x)
- Confirmed OS family via TTL values and TCP stack fingerprinting
- Learned that version strings alone can reveal whether a service is unpatched
  and potentially vulnerable — a critical step before any exploitation phase
- Noted that `-A` is loud and would trigger IDS alerts in a real environment;
  `-sV` alone is preferable when stealth matters

---

## Tool

**Nmap** — used for service enumeration because of its NSE (Nmap Scripting Engine)
integration with `-sV`, which actively probes services to extract banner and version
information. The `-O` flag uses TCP/IP stack fingerprinting to infer the operating
system without requiring root on the target.

---

*Part of the [kali-lab-writeups](https://github.com/stephen-sec/kali-lab-writeups) series.*
