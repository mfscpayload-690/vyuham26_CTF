# Snow

- **Category:** Steganography
- **Points:** 50
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 12:18:00 IST
- **Artifacts:** `snow.gif`, `frames/`

---

## 1. Challenge Overview

An animated GIF (`snow.gif`) displaying dynamic white-noise television snow. The challenge tasks operators with identifying information concealed within transient static noise.

## 2. Frame Extraction & Statistical Analysis

The animated GIF consists of multiple sequential frames exhibiting high spatial noise variance. Each frame appears completely obscured when viewed individually.

Using PIL / ImageMagick to unpack the frame sequence:

```bash
convert snow.gif -coalesce frames/frame_%02d.png
```

Across the 16 extracted frames (`frame_00.png` through `frame_15.png`), each pixel fluctuates between randomized luminosity values generated to simulate analog static.

## 3. Temporal Noise Filtering & Median Stacking

While pseudo-random noise fluctuates rapidly across time steps, concealed message pixels retain static or deterministic invariant values across the temporal axis ($t$):

```python
import numpy as np
from PIL import Image

# Load all frame matrices
frames = [np.array(Image.open(f'frames/frame_{i:02d}.png').convert('L')) for i in range(16)]
stack = np.stack(frames, axis=0)

# Statistical metrics across the temporal axis
variance = np.var(stack, axis=0)
median = np.median(stack, axis=0)
std = np.std(stack, axis=0)

# Invariant pixels have near-zero variance
unchanging_mask = (variance < 1.0)
clean_flag = np.where(unchanging_mask, median, 0).astype(np.uint8)

Image.fromarray(clean_flag).save('frames/clean_flag.png')
```

## 4. Result & Flag Reconstruction

The temporal variance filter eliminates the animated dynamic noise, leaving behind the invariant text glyphs embedded across the frames (`clean_flag.png`):

```text
ctf{same_pixels_in_all_frames}
```

## 5. Security Takeaways
- Temporal dispersion steganography attempts to obscure payloads by exploiting human persistence of vision limitations.
- Mathematical reduction techniques (e.g. median temporal stacking and pixel variance thresholding) neutralize dynamic frame noise in constant time.
