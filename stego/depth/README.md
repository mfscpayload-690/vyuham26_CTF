# Depth

- **Category:** Steganography
- **Points:** 150
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 12:25:00 IST
- **Artifacts:** `depth.png`, `solver.py`, `depth_map.png`, `depth_sgbm.png`, `flag_perfect.png`

---

## 1. Challenge Overview

An autostereogram image (`depth.png`) concealing 3D stereoscopic depth information. The challenge simulates classic "Magic Eye" single-image random dot stereograms (SIRDS / SIS).

## 2. Theoretical Background

Single-Image Autostereograms encode 3D elevation maps ($Z$) into a 2D repeating texture pattern. The apparent depth is controlled by subtle horizontal phase shifts ($\Delta x$) between adjacent repeating stripes:

$$\Delta x = W_{\text{base}} - c \cdot Z(x, y)$$

Where $W_{\text{base}}$ represents the fundamental repetition period of the texture pattern.

## 3. Algorithmic Solution & Autocorrelation

To automatically decode the depth plane without manual stereoscopic viewing:
1. **Autocorrelation Analysis:** Compute the 1D spatial autocorrelation along horizontal scanlines using Fast Fourier Transform (`fftconvolve`) to pinpoint the repeating stripe period:

```python
img_mean_subtracted = img - img.mean()
ac = fftconvolve(img_mean_subtracted, np.flipud(np.fliplr(img_mean_subtracted)), mode='same')
# Peak detection identifies fundamental period: ~114 - 120 pixels
```

2. **Phase Shift Differencing:** Shifting the matrix horizontally by the fundamental pattern width ($\Delta = 114$ to $120$) and subtracting from the original image cancels out identical background wallpaper patterns, isolating edge boundaries where disparity changes:

```python
shifted = np.roll(img, -gap, axis=1)
disparity = np.abs(img - shifted)
```

3. **Semi-Global Block Matching (SGBM):** Using computer-vision disparity estimation (`depth_sgbm.png`) and Prewitt gradient filtering with histogram equalization (`post_process()`), the concealed depth silhouette is extracted.

## 4. Pipeline Execution (`solver.py`)

The automated solver in `solver.py` provides interactive and batch reconstruction:

```bash
python3 solver.py
```

Outputs:
- `depth_map.png`: Recovered disparity contour.
- `flag_perfect.png`: High-contrast thresholded extraction clearly displaying the flag.

## 5. Flag Recovery

The rendered high-contrast depth map unmasks the flag glyphs:

```text
CTF{m4g1c_3y3_d3pth_p3rc3pt10n}
```

## 6. Security Insights
- Visual steganography exploiting binocular disparity can conceal high-dimensional patterns within seemingly innocuous repeating textures.
- Automated autocorrelation and disparity gradient analysis defeat human-perception-based optical obfuscation.
