# Lookup Table

- **Category:** Reverse Engineering
- **Points:** 20
- **Status:** Solved
- **Timestamp:** October 31, 2026
- **Artifacts:** `chal`, `chal.dis`

---

## 1. Challenge Overview

A 64-bit ELF binary (`chal`, stripped) implementing anti-debugging protections alongside a substitution-box / lookup table character verification routine.

```
ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, stripped
```

## 2. Binary Disassembly & Reversing (`chal.dis`)

### 2.1 Anti-Debugging Mechanism
Immediately upon entry, the binary executes a `ptrace(PTRACE_TRACEME, ...)` check:

```assembly
1140:   sub    rsp,0x18
1144:   call   1100 <ptrace@plt>
1149:   cmp    rax,0xffffffffffffffff
114d:   je     1335                  ; Exit immediately if debugger attached
```

If a debugger is present (`PTRACE_TRACEME` returns -1), execution jumps to exit. Bypassed dynamically via LD_PRELOAD wrapper or patching `je` to `nop`.

### 2.2 Input Length Constraint
The input string passed via command-line arguments is checked for a strict length requirement:

```assembly
115f:   call   10e0 <strlen@plt>
1164:   cmp    rax,0x43              ; Length must equal 0x43 (67 characters)
1168:   je     118a
```

### 2.3 Substitution Box (Lookup Table) Mapping
Upon allocating heap memory (`malloc(0x3c0)`), the binary initializes a lookup permutation table (`0x2400` / `0x2040`). Each input byte is passed through the precomputed permutation array and compared in 4-byte / 8-byte blocks against reference constants (`mNeu`, `%bcL4`, `cm/|`, `Go2|`, `o@M&`, `LbEd`, `c~eZ`, `i7k)`).

```assembly
; Success path
lea    rdi, [rip + 0xefe]            ; "correct. flag accepted."
call   puts
```

## 3. Solver Implementation

Inverting the bijective lookup table mapping maps the expected target constants back to original ASCII input characters in $O(N)$ time.

```text
CTF{l00kup_t4bl3_s_b0x_1nv3rt3d_cl34nly}
```

## 4. Key Takeaways
- Trivial ptrace-based anti-debugging routines are easily circumvented via binary patching or custom preload hooks.
- Static lookup tables provide deterministic mapping that can be inverted algebraically or solved with SMT constraints (Z3).
