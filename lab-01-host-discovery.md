# Lab 01 — Network Scanning & Host Discovery

**Tool:** Nmap  
**Date:** 2026 (Kali Linux training, Day 1–2)  
**Difficulty:** Foundational

---

## Situation

In a SOC or penetration testing engagement, the first step is always understanding what
is on the network. Before any vulnerability assessment or service enumeration can happen,
live hosts must be identified. This lab simulated that initial reconnaissance phase on
a local lab network.

---

## Task

Identify all live hosts on a local subnet using passive and active discovery techniques,
without triggering aggressive detection signatures.

---

## Action

```bash
# Ping sweep — discover live hosts without port scanning
nmap -sn 192.168.1.0/24

# Basic scan of discovered host — top 1000 ports
nmap 192.168.1.1

# Save results to file for documentation
nmap -sn 192.168.1.0/24 -oN host_discovery.txt
```

**Process:**
1. Started with a ping sweep (`-sn`) to map live hosts without scanning ports
2. Noted all responding IP addresses and their MAC addresses
3. Identified the gateway, any networked devices, and the target host
4. Saved output to a text file for reference in later enumeration stages

---

## Result

- Confirmed live hosts on the subnet
- Identified gateway IP and MAC address
- Established a target list for follow-on service enumeration
- Learned that `-sn` generates significantly less noise than a full port scan,
  making it preferable for initial discovery in sensitive environments

---

## Tool

**Nmap** (Network Mapper) — the industry-standard open-source tool for network
discovery and security auditing. Selected for this task because of its `-sn` flag,
which performs host discovery without triggering port scan alerts, and its flexible
output formats for documentation.

---

*Part of the [kali-lab-writeups](https://github.com/stephen-sec/kali-lab-writeups) series.*
