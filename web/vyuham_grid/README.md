# Vyuham Grid

- **Category:** Web 2.0
- **Points:** 350
- **Status:** Attempted / Forensic Reconnaissance
- **Artifacts:** `programs-bg.jpg`, `logo.png`, `portal_banner.png`, `enhanced.jpg`, `tron_ares.jpg`

---

## 1. Challenge Overview

A futuristic web interface inspired by the Tron / Grid aesthetic. The challenge involves examining hidden assets, client-side scripts, and image steganography embedded directly within the portal theme media.

## 2. Reconnaissance & Asset Auditing

The portal distributes several graphic elements:
- `logo.png` & `portal_banner.png`: Core portal interface branding.
- `programs-bg.jpg` & `tron_ares.jpg`: Background graphics.
- `enhanced.jpg`: Contrast-stretched image generated during steganographic inspection of portal media.

Inspecting metadata, color planes, and hidden HTML comments across the web assets revealed cryptographic hints and hidden endpoints for the challenge.
