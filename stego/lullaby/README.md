# Lullaby

- **Category:** Steganography
- **Points:** 200
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 12:42:00 IST
- **Artifacts:** `lullaby.wav`, `diff.wav`, `spectrogram.png`

---

## 1. Challenge Overview

A two-channel stereophonic audio file (`lullaby.wav`). Standard acoustic playback delivers a soft ambient music track with no perceptible anomalies.

## 2. Audio Channel Dissection

Analyzing header metadata and audio properties:
- **Channels:** 2 (Stereo &mdash; Left, Right)
- **Sample Rate:** 22,050 Hz
- **Sample Width:** 16-bit signed PCM
- **Frames:** 492,466

In standard stereo production, acoustic signals share spatial commonality. Adversaries often embed hidden data by modulating the differential phase between left and right channels, keeping the mono mix audible while concealing the payload in the out-of-phase component.

## 3. Stereo Phase Cancellation Attack

To isolate the differential phase signal, channel subtraction ($L - R$) is performed across all samples:

$$\text{Sample}_{\text{diff}}[i] = \text{Sample}_{\text{Left}}[i] - \text{Sample}_{\text{Right}}[i]$$

Implemented via Python `wave` / `numpy`:

```python
import wave, numpy as np

with wave.open('lullaby.wav', 'rb') as w:
    params = w.getparams()
    frames = w.readframes(params.nframes)

audio = np.frombuffer(frames, dtype=np.int16).reshape(-1, 2)
left, right = audio[:, 0], audio[:, 1]

# Compute stereo difference
diff = (left.astype(np.int32) - right.astype(np.int32)).clip(-32768, 32767).astype(np.int16)

with wave.open('diff.wav', 'wb') as out:
    out.setnchannels(1)
    out.setsampwidth(2)
    out.setframerate(params.framerate)
    out.writeframes(diff.tobytes())
```

The resulting `diff.wav` completely strips the ambient music track, leaving only a faint high-frequency acoustic whistle.

## 4. Spectral Demodulation

Generating a high-resolution Fourier spectrogram of `diff.wav`:

```bash
sox diff.wav -n spectrogram -Y 1800 -X 2400 -o spectrogram.png
```

The frequency waterfall display in `spectrogram.png` reveals visual glyphs drawn into the audio frequency spectrum:

```text
CTF{st3r30_ph4s3_c4nc3ll4t10n_succ3ss}
```

## 5. Security Insights
- Stereo phase manipulation allows audio steganography to survive mono downmixing and casual perceptual audition.
- Phase-differential decomposition is an essential first-order procedure when auditing multi-track audio assets.
