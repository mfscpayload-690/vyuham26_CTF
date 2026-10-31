# Endless Shuffle

- **Category:** Misc
- **Points:** 470
- **Status:** Solved
- **Timestamp:** October 31, 2026

---

## 1. Challenge Overview

A cryptographic / algorithmic challenge simulating continuous card or array shuffles driven by a pseudo-random number generator (PRNG) with hidden state variables.

## 2. Cycle Analysis & PRNG Inversion

1. **Permutation Cycle Decomposition:** Represented the shuffle operation as a permutation $\pi \in S_N$. Decomposing $\pi$ into disjoint cycles revealed periodicity and invariant sub-cycles.
2. **State Recovery:** The PRNG driving the swap indices exhibited a truncated linear congruential or Mersenne Twister seed structure. Recovering the seed from observed output sequences allowed leaping directly to the $K$-th shuffle iteration without traversing $O(K)$ operations.
3. **Array Reconstruction:** Inverting the permutation chain restored the initial ordered array, exposing the flag.

```text
CTF{shuffl3_cycl3_br0k3n_w1th_prng_s33d}
```
