# Ember Jar

- **Category:** Web 3.0
- **Points:** 90
- **Status:** Attempted / Reentrancy Exploitation Analysis

---

## 1. Challenge Overview

A decentralized finance (DeFi) vault contract allowing users to deposit ETH tokens into an "Ember Jar" and withdraw yields based on time-weighted stakes.

## 2. Exploitation Vectors

1. **Classic / Cross-Function Reentrancy:** The `withdraw()` routine transferred native ETH via `msg.sender.call{value: amount}("")` prior to decrementing the user's recorded ledger balance.
2. **Exploit Construct:** Deployed an attacking smart contract implementing a `fallback()` / `receive()` function that re-invoked `withdraw()` recursively until draining the vault balance.
