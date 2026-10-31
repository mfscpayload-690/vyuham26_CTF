# CTF Operations Repository &mdash; BinaryBandits

An archive of challenge artifacts, forensic investigations, custom exploit tooling, and writeups produced by team **BinaryBandits** during the CTF competition.

```
       _____ _                            ____                  _ _ _       
      | __  |_|___ ___ ___ _ _    ___    | __  |___ ___ ___ _ _|_| | |_ ___ 
      | __ -| |   | .'|  _| | |  |___|   | __ -| .'|   | . | | | |  _| |_ -|
      |_____|_|_|_|__,|_| |_  |          |_____|__,|_|_|___|___|_|_| |_|___|
                          |___|                                             
```

---

## Performance Summary

| Metric | Standing |
| :--- | :--- |
| **Team Name** | `BinaryBandits` |
| **Final Rank** | **7th Place** (Top 30% of 23 competing teams) |
| **Score Accumulated** | **3,461 Points** |
| **Solve Ratio** | 13.19% Solves / 86.81% Global Field Submissions |
| **Primary Vectors** | OSINT (33.3%), Forensics (25.0%), Stego (25.0%), Misc (16.7%), Rev |

---

## Team Members

<table>
  <tr>
    <td align="center" width="150px">
      <a href="https://github.com/mfscpayload-690">
        <img src="https://github.com/mfscpayload-690.png?size=100" width="100" height="100" style="border-radius: 50%;" alt="Aravind Lal"/><br />
        <sub><b>Aravind Lal</b></sub>
      </a><br />
      <a href="https://github.com/mfscpayload-690"><sub><code>@mfscpayload-690</code></sub></a>
    </td>
    <td align="center" width="150px">
      <a href="https://github.com/Benoommenmathew">
        <img src="https://github.com/Benoommenmathew.png?size=100" width="100" height="100" style="border-radius: 50%;" alt="Ben Oommen Matthew"/><br />
        <sub><b>Ben Oommen Matthew</b></sub>
      </a><br />
      <a href="https://github.com/Benoommenmathew"><sub><code>@Benoommenmathew</code></sub></a>
    </td>
    <td align="center" width="150px">
      <a href="https://github.com/Bhavith-fs">
        <img src="https://github.com/Bhavith-fs.png?size=100" width="100" height="100" style="border-radius: 50%;" alt="Bhavith Madhav"/><br />
        <sub><b>Bhavith Madhav</b></sub>
      </a><br />
      <a href="https://github.com/Bhavith-fs"><sub><code>@Bhavith-fs</code></sub></a>
    </td>
  </tr>
</table>

---

## Solves & Score Distribution

```
Category Breakdown
========================================================================
[====================] OSINT     (33.33%) &bull; 1,541 pts
[===============     ] Forensics (25.00%) &bull;   400 pts
[===============     ] Stego     (25.00%) &bull;   400 pts
[==========          ] Misc      (16.67%) &bull; 1,000 pts
[=======             ] Rev                &bull;   120 pts
========================================================================
Total Verified CTFd Points: 3,461
```

### Solve Ledger (Chronological)

| Time (IST) | Category | Challenge Name | Points | Flag / Primary Finding |
| :--- | :--- | :--- | :---: | :--- |
| **12:18 PM** | Stego | [Snow](stego/snow/README.md) | 50 | Temporal variance & median stacking across noise frames |
| **12:25 PM** | Stego | [Depth](stego/depth/README.md) | 150 | Single-Image Autostereogram autocorrelation solver |
| **12:42 PM** | Stego | [Lullaby](stego/lullaby/README.md) | 200 | Stereo phase difference ($L - R$) spectral demodulation |
| **01:12 PM** | OSINT | [Borrowed Light](osint/borrowed_light/README.md) | 500 | Historical Ancient Lights architectural easement tracing |
| **02:03 PM** | OSINT | [Paper Neighbourhood](osint/paper_neighbourhood/README.md) | 121 | Key West Sanborn Fire Insurance map indexing (Block 104/89) |
| **03:37 PM** | Forensics | [Breadcrumbs](forensics/breadcrumbs/README.md) | 50 | `CTF{cl34rt3xt_cr3ds_0n_th3_w1r3}` |
| **03:42 PM** | Forensics | [Ghost Channel](forensics/ghost_channel/README.md) | 150 | Polyglot ZIP carver + spectral audio password recovery |
| **03:46 PM** | Forensics | [Ledger Node 07](forensics/ledger_node_07/README.md) | 200 | `CTF{b1t_pl4n3_4n4lys1s_p41d_0ff}` |
| **03:50 PM** | Misc | [Side Channel](misc/side_channel/README.md) | 130 | Acoustic signal spectrum analysis & modulation decoding |
| **03:54 PM** | Misc | [Shredded](misc/shredded/README.md) | 100 | Mechanically shredded document seam-affinity reassembly |
| **05:09 PM** | OSINT | [Mud to Identity](osint/mud_to_identity/README.md) | 450 | Soil composition and vehicular tread intelligence mapping |
| **05:10 PM** | OSINT | [The Rescue Ledger](osint/the_rescue_ledger/README.md) | 370 | Maritime AIS transponder and SAR radio ledger correlation |
| *Session* | OSINT | [The Patent's Birthday](osint/patents_birthday/README.md) | 100 | USPTO patent gazette historical grant verification |
| *Session* | Misc | [Time's Arrow](misc/times_arrow/README.md) | 300 | Non-destructive cellular automaton state time inversion |
| *Session* | Misc | [Endless Shuffle](misc/endless_shuffle/README.md) | 470 | PRNG state reconstruction & disjoint cycle decomposition |
| *Session* | Rev | [Lookup Table](rev/lookup_table/README.md) | 20 | Stripped ELF64 anti-ptrace bypass & S-box inversion |
| *Session* | Rev | [Tiny VM](rev/tiny_vm/README.md) | 100 | Custom virtual architecture disassembler & bytecode reversal |

---

## Repository Structure

The workspace follows a category-isolated, per-challenge hierarchy:

```
├── forensics/
│   ├── breadcrumbs/          # Network PCAP stream & plaintext credential leakage
│   ├── ghost_channel/        # Audio steganography & polyglot archive extraction
│   └── ledger_node_07/       # Carved ext4 image, inode PNG & bitplane LSB unmasking
├── misc/
│   ├── endless_shuffle/      # Permutation cycle recovery & PRNG cracking
│   ├── shredded/             # 1D strip reassembly & edge continuity correlation
│   ├── side_channel/         # Audio cassette acoustic side-channel demodulation
│   └── times_arrow/          # Discrete state inversion & entropy decay reversal
├── osint/
│   ├── borrowed_light/       # Legal survey records & Ancient Lights easement dockets
│   ├── mud_to_identity/      # Forensic geology, vehicular spatter & registry lookups
│   ├── over_the_line/        # Borderline marker & aerial infrastructure geolocation
│   ├── paper_neighbourhood/  # Sanborn Fire Insurance maps (Key West, FL 1889-1899)
│   ├── patents_birthday/     # USPTO intellectual property gazette intelligence
│   └── the_rescue_ledger/    # Maritime distress ledger & AIS transponder correlation
├── rev/
│   ├── lookup_table/         # Stripped x86-64 binary, ptrace checks & lookup table
│   ├── tiny_vm/              # Virtual machine opcode dispatch loop & bytecode reverser
│   └── x_floor/              # Floating-point step constraints & Z3 SMT solver
├── stego/
│   ├── depth/                # Autostereogram solver, autocorrelation & depth map
│   ├── lullaby/              # Stereo phase difference cancellation & spectrogram
│   └── snow/                 # Animated static noise GIF & temporal median filter
├── tools/
│   ├── steghide/             # Portable steghide utilities suite
│   └── README.md             # Operational tooling and environment manual
├── web/
│   ├── staff_directory/      # E-Corp Intranet, IDOR & employee directory audit
│   ├── vyuham_grid/          # Tron Grid client-side theme analysis & asset stego
│   └── vyuham_notes/         # Markdown sanitizer audits & admin bot interaction
└── web3/
    ├── ember_jar/            # DeFi smart contract reentrancy drain attack
    └── whisper_vault/        # EVM smart contract decompilation (Solidity v0.8.28)
```

---

## Operational Tooling Highlights

- **Steganography & Signal Processing:** `scipy`, `numpy`, `skimage`, `Pillow`, `sox`, `FFmpeg`
- **Reverse Engineering & Disassembly:** `objdump`, `readelf`, `GDB`, `strace`, `ltrace`
- **Network & System Forensics:** `tcpdump`, `Wireshark`, `tshark`, `fls`, `sleuthkit`, `mitmproxy`
- **Automation Solvers:** Custom Python disparity calculators, frame-stack statistical reducers, and SMT constraint solvers.

---

## Privacy & Operational Security (OPSEC)

All artifacts in this repository have been sanitized to protect private operational data:
- Stripped absolute host paths (`/home/...`) and system identifiers.
- Scrubbed local network addresses, private keys, authentication cookies, and transient virtual environment caches (`.venv`).
- Retained competition-grade technical documentation and reproducibility for research purposes.
