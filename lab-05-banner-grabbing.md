# Lab 05 — Banner Grabbing & Service Fingerprinting

**Tool:** Netcat, Python  
**Date:** 2026 (Kali Linux training, Day 7–9)  
**Difficulty:** Foundational–Intermediate

---

## Situation

Banner grabbing is a technique used to extract information directly from a service
by connecting to its open port and reading the response it sends back. Unlike Nmap's
version detection, banner grabbing makes a raw connection and captures exactly what
the service announces — which often includes software name, version, and configuration
details. This lab performed banner grabbing manually using Netcat and then automated
the process with Python.

---

## Task

Connect to open services on a target host, capture their banners manually with Netcat,
then replicate and automate the process using a Python socket script.

---

## Action

**Netcat — manual banner grab:**
```bash
# Connect to a service and read its banner
nc 192.168.1.1 80

# After connecting, send an HTTP request to trigger a response
GET / HTTP/1.0

# Connect to SSH port — banner is sent immediately on connection
nc 192.168.1.1 22

# Connect to FTP port
nc 192.168.1.1 21
```

**Python — automated banner grabbing:**
```python
import socket

def grab_banner(ip, port):
    try:
        s = socket.socket()
        s.settimeout(5)
        s.connect((ip, port))
        banner = s.recv(1024).decode().strip()
        print(f"[+] {ip}:{port} — {banner}")
        s.close()
    except Exception as e:
        print(f"[-] {ip}:{port} — {e}")

# Run against common ports
ports = [21, 22, 25, 80, 443]
for port in ports:
    grab_banner("192.168.1.1", port)
```

**Process:**
1. Used Netcat to manually connect to open ports and read raw service banners
2. Sent basic protocol requests (HTTP GET) to trigger verbose responses
3. Documented the banner strings returned by each service
4. Rebuilt the process in Python using the `socket` module
5. Used `recv(1024)` to capture the response and `decode()` to convert bytes to string
6. Added error handling with try/except to manage closed ports and timeouts

---

## Result

- Successfully grabbed banners from HTTP, SSH, and FTP services manually via Netcat
- Confirmed that SSH and FTP services announce their version on connection
  without any credentials required
- Replicated the process in Python, demonstrating that banner grabbing
  can be fully automated with minimal code
- Learned the difference between `recv()` (raw bytes) and `decode()` (readable string)
- Understood that banners are voluntary — hardened servers suppress or falsify them,
  so absence of a banner is not confirmation that a service is absent

---

## Tool

**Netcat** — used for manual banner grabbing because it creates a raw TCP connection
with no protocol overhead, allowing direct interaction with any service.

**Python (socket module)** — used to automate the same process programmatically.
The `socket` module gives low-level network access and is the foundation for
building custom network tools in Python.

---

*Part of the [kali-lab-writeups](https://github.com/stephen-sec/kali-lab-writeups) series.*
