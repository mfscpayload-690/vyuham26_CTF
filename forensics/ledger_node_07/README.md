# Ledger Node 07

- **Category:** Forensics
- **Points:** 200
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 15:46:00 IST
- **Flag:** `CTF{b1t_pl4n3_4n4lys1s_p41d_0ff}`
- **Artifacts:** `ledger07.img.gz`, `fid122.png`, `lsb_R.png`, `lsb_G.png`, `lsb_B.png`

---

## 1. Challenge Overview

An extracted ext4 filesystem image (`ledger07.img.gz`) recovered from a compromised distributed ledger validator node. The node operated automated transaction verification routines before sudden anomalous termination.

## 2. Filesystem Carving & Analysis

Uncompressing and mounting the disk image:

```bash
gzip -dc ledger07.img.gz > ledger07.img
fls -r ledger07.img
```

A search for unlinked/deleted inodes and anomalous media assets highlights an extracted asset at File ID `122` (`fid122.png`, 320x64 pixels). 

Standard visual inspection shows a pseudo-random RGB noise pattern resembling encrypted telemetry or corrupted image data.

## 3. Bitplane Decomposition & LSB Extraction

To analyze hidden modulation within the sub-perceptual color space, each 8-bit color channel (Red, Green, Blue) is dissected down to its least significant bitplane ($b_0$):

```python
import numpy as np
from PIL import Image

im = Image.open('fid122.png')
arr = np.array(im)

# Extract bitplane 0 for each channel
for idx, ch in enumerate(['R', 'G', 'B']):
    bitplane = (arr[:, :, idx] & 1) * 255
    Image.fromarray(bitplane.astype(np.uint8)).save(f'lsb_{ch}.png')
```

### Channel Dissection Results:
- **`lsb_G.png` / `lsb_B.png`:** Exhibits pseudo-random entropy distribution across all 320x64 blocks.
- **`lsb_R.png`:** Completely clean background with sharp typographic glyphs rendered directly into the red channel's least significant bit.

The rendered message in `lsb_R.png` displays:
```text
CTF{b1t_pl4n3_4n4lys1s_p41d_0ff}
```

## 4. Key Takeaways
- Steganographic encoding targeting single-channel least-significant bits evades naive perceptual hashing and bulk file integrity checks.
- Comprehensive digital forensics on carved media files necessitates layer-by-layer bitplane slicing across all color components.
