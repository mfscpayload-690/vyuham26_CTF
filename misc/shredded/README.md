# Shredded

- **Category:** Misc
- **Points:** 100 / 130
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 15:54:00 IST
- **Artifacts:** `shredded.png`

---

## 1. Challenge Overview

An image of a mechanically shredded document (`shredded.png`, 482x682 pixels). The original document containing the flag has been processed through a vertical cross-cut or strip-cut shredder, with vertical strips randomly permuted across the horizontal canvas.

## 2. Structural Analysis

Inspecting the pixel dimensions:
- **Height:** 682 px
- **Width:** 482 px

The document strips share a fixed width $W_s$ across the vertical axis. To reconstruct the original sheet:
1. Identify shred boundaries by locating vertical seam discontinuities where pixel intensity variance between adjacent columns jumps sharply.
2. Measure edge-affinity scores (e.g., Euclidean distance or mean squared error between the right edge of strip $A$ and left edge of strip $B$).
3. Permute strips to minimize edge discontinuity across text strokes and lines.

## 3. Strip Reassembly Algorithm

```python
import numpy as np
from PIL import Image

im = Image.open('shredded.png')
arr = np.array(im)

# Detect strip boundaries based on periodic width or gradient peaks
# Match left edge of strip i with right edge of strip j using difference minimization
# Reconstruct ordered strip indices
```

Reassembling the strips restores the unbroken horizontal lines of text across the document, revealing the flag.

## 4. Key Takeaways
- Strip-cut paper shredding maintains spatial correlation along the vertical axis, rendering purely 1D physical destruction susceptible to automated graph-matching reassembly.
