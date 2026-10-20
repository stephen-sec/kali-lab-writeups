# Lab 04 — Email OSINT

**Tool:** Holehe  
**Date:** 2026 (Kali Linux training, Day 5–6)  
**Difficulty:** Foundational

---

## Situation

When a target's email address is known, it can be used to map which online services
they are registered with — without sending any emails or alerting the target.
This is a common technique in threat intelligence and social engineering pre-text
research. This lab used Holehe to perform passive email-based account enumeration.

---

## Task

Given a target email address, identify all online platforms where that email
is registered using password reset flow analysis.

---

## Action

```bash
# Basic email check across 120+ platforms
holehe target@email.com

# Export only confirmed registrations
holehe target@email.com --only-used > holehe_results.txt
```

**Process:**
1. Ran Holehe against a test email address
2. Observed real-time output as each platform was queried
3. Noted confirmed registrations (✅), non-registrations (❌),
   and platforms that couldn't be checked (⚠️)
4. Exported confirmed results to file for documentation
5. Analyzed confirmed platforms for investigative follow-on steps

---

## Result

- Identified platforms where the target email is registered
- Confirmed that Holehe operates passively — no emails are sent to the target,
  making it undetectable during the enumeration phase
- Learned that the password reset flow is a reliable signal:
  sites return different responses for known vs. unknown emails
- Noted that rate limiting on some platforms causes ⚠️ results —
  these require manual verification or a delayed retry
- Understood the investigative value: a confirmed account list narrows
  the scope of further OSINT and social engineering research significantly

---

## Tool

**Holehe** — an open-source OSINT tool that checks whether an email address is
registered on 120+ websites by abusing password reset flows. Selected because it
is entirely passive (no contact with the target), fast, and outputs clean,
actionable results. Pairs well with Sherlock when both a username and email are known.

---

*Part of the [kali-lab-writeups](https://github.com/stephen-sec/kali-lab-writeups) series.*
