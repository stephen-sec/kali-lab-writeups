# Lab 03 — Username OSINT

**Tool:** Sherlock  
**Date:** 2026 (Kali Linux training, Day 4–5)  
**Difficulty:** Foundational

---

## Situation

In OSINT investigations, a known username is often the starting point for mapping
a target's online presence across multiple platforms. A single username reused across
sites can reveal accounts, activity patterns, and additional identifying information.
This lab simulated an OSINT reconnaissance task using only a username as the initial input.

---

## Task

Given a target username, identify all platforms where that username is registered
and document the findings in a structured format.

---

## Action

```bash
# Basic username search across 300+ platforms
sherlock targetusername

# Search with results saved to file
sherlock targetusername --output sherlock_results.txt

# Reduce timeout per site for faster results
sherlock targetusername --timeout 10

# Search multiple usernames at once
sherlock user1 user2 user3
```

**Process:**
1. Launched Sherlock with the target username
2. Monitored live output as Sherlock queried each platform
3. Noted confirmed hits — platforms where the username was found
4. Saved full output to a text file for documentation
5. Reviewed confirmed accounts for additional identifiers
   (profile photos, bio details, linked accounts)

---

## Result

- Retrieved a list of platforms where the target username exists
- Identified associated profiles that could be used for further investigation
- Learned that username reuse across platforms is extremely common and
  significantly expands the attack surface in a social engineering scenario
- Confirmed that Sherlock filters out negative results by default,
  making output clean and immediately actionable

---

## Tool

**Sherlock** — an open-source OSINT tool that queries 300+ social media and web
platforms simultaneously for a given username. Selected because it automates what
would otherwise be hundreds of manual searches, and outputs only confirmed hits,
reducing noise in the investigation.

---

*Part of the [kali-lab-writeups](https://github.com/stephen-sec/kali-lab-writeups) series.*
