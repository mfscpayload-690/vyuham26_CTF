# Side Channel

- **Category:** Misc
- **Points:** 130
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 15:50:00 IST
- **Artifacts:** `tape.wav`, `tape_spec.png`

---

## 1. Challenge Overview

An acoustic audio capture (`tape.wav`) simulating magnetic tape playback or high-speed hardware telemetry. The acoustic emission contains rapid modulation bursts indicative of physical side-channel signal leakage (e.g., CPU coil whine, serial line modulation, or audio-frequency shift keying).

## 2. Signal Processing & Spectral Demodulation

Direct listening produces repetitive rhythmic chirps and tone bursts. To analyze the modulation characteristics, the signal is transformed into the frequency domain:

```bash
sox tape.wav -n spectrogram -Y 1500 -X 2400 -o tape_spec.png
```

Inspecting `tape_spec.png`:
- Regular carrier frequencies appear between 1 kHz and 5 kHz.
- Modulation pulses alternate in duration and amplitude, corresponding to a structured signal protocol (e.g. FSK / AFSK or Morse-style timing patterns).
- Distinct spectral line pulses encode digital high (`1`) and low (`0`) state transitions.

## 3. Demodulation Protocol & Flag Recovery

Extracting pulse timing or decoding the visual tone sequences yields the flag sequence.

```text
CTF{4c0ust1c_s1d3_ch4nn3l_d3c0d3d}
```

## 4. Key Takeaways
- Physical components emit involuntary acoustic and electromagnetic side-channel telemetry that can be decoded by remote sensors without physical tap access.
