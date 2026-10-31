# Whisper Vault

- **Category:** Web 3.0
- **Points:** 70 / 90
- **Status:** Attempted / EVM Smart Contract Auditing
- **Artifacts:** `code_0.hex` through `code_6.hex`

---

## 1. Challenge Overview

An Ethereum Virtual Machine (EVM) smart contract challenge involving 7 interconnected contract bytecode components (`code_0.hex` through `code_6.hex`) compiled with Solidity `v0.8.28`.

## 2. EVM Bytecode & Decompilation

Inspecting `code_0.hex` metadata confirms Solidity compiler signature:
```
solc v0.8.28 (0x00081c)
```

Disassembling the contracts exposes the core storage and control flow architecture:
- Function dispatchers matching standard 4-byte selectors.
- State variable layout mapping internal balances and encrypted key fragments stored in private storage slots.

## 3. Vulnerability Vectors

1. **Storage Collision / Private Storage Reading:** In EVM architecture, "private" variables are only hidden from other smart contracts, not from external observers. Querying raw storage slots via `eth_getStorageAt` allows direct retrieval of secret phrases and vault keys.
2. **Delegatecall Injection / State Overwrite:** Investigated proxy contracts forwarding execution via `delegatecall` without proper storage alignment, allowing arbitrary overwrite of the owner variable.
