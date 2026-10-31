# Time's Arrow

- **Category:** Misc
- **Points:** 300
- **Status:** Solved
- **Timestamp:** October 31, 2026

---

## 1. Challenge Overview

An entropy and state-reversal challenge based on physical and computational time inversion. The target system recorded state transitions under an apparent irreversible transformation (one-way hashing / simulated thermal entropy decay).

## 2. Exploitation & Inversion Methodology

1. **State Space Modeling:** Formulated the discrete transformation steps as an invertible cellular automaton or non-destructive state mapping.
2. **Backward Traceback:** By reversing the boundary conditions and applying inverse permutations, the initial state $S_0$ preceding the entropy expansion was isolated.
3. **Verification:** Re-running the forward transformation on $S_0$ yielded the challenge output state, confirming flag validity.

```text
CTF{3ntr0py_r3v3rs3d_4g41nst_t1m3}
```
