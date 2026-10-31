# The Rescue Ledger

- **Category:** OSINT
- **Points:** 370
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 17:10:00 IST

---

## 1. Challenge Overview

A maritime search-and-rescue (SAR) open-source intelligence investigation. The challenge required cross-referencing naval dispatch logs, Coast Guard rescue ledgers, Automated Identification System (AIS) vessel transponder pings, and Morse/VHF distress transmissions.

## 2. Methodology & Resolution

1. **Vessel Transponder Tracking:** Reconstructed vessel trajectories using archival MarineTraffic / VesselFinder AIS coordinates.
2. **Maritime Incident Logs:** Audited maritime rescue ledger incident dockets, corroborating distress call times against vessel MMSI records.
3. **Target Identification:** Pinpointed the exact distress coordinates and vessel name, submitting the recovered coordinate sequence to claim the solve.

```text
CTF{m4r1t1m3_r3scu3_l3dg3r_c00rd1n4t3s_r3c0v3r3d}
```
