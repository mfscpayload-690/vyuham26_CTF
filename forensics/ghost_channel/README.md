# Ghost Channel

- **Category:** Forensics
- **Points:** 150
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 15:42:00 IST
- **Artifacts:** `ghost.wav`, `ghost_spec.png`

---

## 1. Challenge Overview

An audio transmission (`ghost.wav`) is intercepted from an adversary listening post. The transmission contains anomalous spectral emissions alongside appended binary telemetry.

## 2. Reconnaissance & Structural Analysis

Inspecting the file structure indicates a dual-layer obfuscation scheme:
1. **Appended Data Stream:** A ZIP archive header (`PK\x03\x04`) is appended directly to the end of the RIFF WAV structure at byte offset `165810`.
2. **Spectral Signaling:** Audio rendering reveals high-frequency acoustic steganography in the audio carrier.

```bash
binwalk ghost.wav
# Offset 0x287B2: Zip archive data, at least v2.0 to extract, compressed size: 48, uncompressed size: 38, name: flag.txt
```

Extracting the ZIP reveals `flag.txt`, which is encrypted using standard PKZIP password protection:
```bash
unzip -l ghost.wav
# flag.txt (Password Required)
```

## 3. Spectral Demodulation

To recover the decryption key, the audio carrier is transformed into a frequency-domain spectrogram using Fourier transformation (`scipy` / `matplotlib` / `sox`):

```bash
sox ghost.wav -n spectrogram -Y 1200 -X 2400 -o ghost_spec.png
```

Inspecting `ghost_spec.png` across the frequency bands between 600 Hz and 1100 Hz reveals clear visual acoustic steganography encoding the passphrase:

```text
SPECTRAL_WRAITH
```

## 4. Exploitation & Decryption

Supplying the recovered spectral passphrase to the encrypted archive payload:

```bash
python3 -c "
import zipfile, io
with open('ghost.wav', 'rb') as f:
    data = f.read()
idx = data.find(b'PK\x03\x04')
z = zipfile.ZipFile(io.BytesIO(data[idx:]))
print(z.read('flag.txt', pwd=b'SPECTRAL_WRAITH').decode())
"
```

The decrypted archive yields the flag.

## 5. Security Insights
- Polyglot files merging multimedia RIFF structures with trailing archive headers represent a common evasion tactic against basic mime-type validators.
- Multi-channel forensic pipelines must inspect frequency-domain acoustic signals in addition to raw byte signatures.
