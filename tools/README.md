# CTF Tooling & Utilities

This directory contains standalone tools and utilities utilized during the competition.

## Included Utilities

### Steghide (Portable Suite)
- **Path:** `tools/steghide/usr/bin/steghide`
- **Purpose:** Steganography analysis and extraction for concealed payloads in JPEG and WAV media.
- **Dependencies:** Embedded libraries in `tools/steghide/usr/lib/`.
- **Usage Example:**
  ```bash
  LD_LIBRARY_PATH=tools/steghide/usr/lib:$LD_LIBRARY_PATH tools/steghide/usr/bin/steghide extract -sf target.jpg
  ```
