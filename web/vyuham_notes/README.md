# Vyuham Notes

- **Category:** Web 2.0
- **Points:** 500
- **Status:** Attempted / Exploitation Analysis

---

## 1. Challenge Overview

A collaborative notes web application featuring rich-text Markdown rendering, user permissions, and an automated headless admin review bot.

## 2. Attack Vectors

1. **Cross-Site Scripting (XSS):** Evaluated sanitization bypasses within the client-side Markdown rendering library (DOMPurify / marked) to inject JavaScript payloads (`<img src=x onerror=...>`, mutation XSS / mXSS).
2. **Cookie Theft / Admin Bot Triggering:** Submitting note URLs to the verification bot aimed to exfiltrate the bot's `flag` cookie or session token to an external listener.
3. **CSP Bypass:** Investigated Content Security Policy directives for script-src whitelisted CDNs or nonce leakage.
