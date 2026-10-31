# Tiny VM

- **Category:** Reverse Engineering
- **Points:** 100
- **Status:** Solved
- **Timestamp:** October 31, 2026

---

## 1. Challenge Overview

A virtual machine obfuscation challenge implementing a custom software interpreter (virtual architecture) executing embedded bytecode instructions.

## 2. Architecture & Virtual Instruction Set (ISA)

1. **Virtual Machine State:** The interpreter manages a virtual CPU state containing virtual registers ($V_0 \dots V_7$), a program counter ($V_{\text{PC}}$), a virtual call stack, and memory buffers.
2. **Opcode Dispatcher:** A `switch-case` dispatch loop fetches 1-byte opcodes and unpacks register indices and immediate operands.
   - Arithmetic: `V_ADD`, `V_XOR`, `V_SUB`, `V_ROL`
   - Flow control: `V_JZ`, `V_JNZ`, `V_CALL`, `V_RET`
   - Memory: `V_LOAD`, `V_STORE`
3. **Bytecode Disassembler:** Wrote a custom disassembler script to translate raw bytecode into human-readable assembly instructions.
4. **Logic Recovery:** The bytecode performed a cyclic modular rolling-key check over the flag characters. Reversing the operations yielded the input key.

```text
CTF{t1ny_v1rtu4l_m4ch1n3_d3c0mp1l3d}
```
