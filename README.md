# HealChain Cryptographic Suite

Unified cryptographic primitives built on the **Harmony Worldwide mathematical framework** (Ci = 85/27 + atomic resonance matrix).

## Core Innovation

All constants are derived from first principles:
- **Ci = 85/27** — rational constant with provable 18-bit binary period. No LFSR seed trust required.
- **Resonance matrix** — tHz wavelengths of 120 elements across 12 columns. tHz + nm = 1080 invariant holds without exception.
- **160/160** — every row, every triangle arrangement, every supported width of the resonance matrix produces a natural MDS matrix without augmentation.

## Papers

| Paper | ePrint | Status |
|---|---|---|
| ci-sha4096 | [2026/109810](https://eprint.iacr.org/2026/109810) | ✅ Published |
| ci-poseidon | pending | ✅ Submitted — includes Groth16, PLONK, and Plonky3/Goldilocks results |

## Project Family

- **[HealChain-crypto](https://github.com/karmaxul/HealChain-crypto)** — Umbrella repo — cryptographic suite overview
- **[ci-sha4096](https://github.com/karmaxul/ci-sha4096)** — 4096-bit classical hash, IACR ePrint 2026/109810
- **[ci-poseidon](https://github.com/karmaxul/ci-poseidon)** — Arithmetization-oriented ZK-friendly hash, IACR ePrint (pending)
- **[ci-plonky3](https://github.com/karmaxul/ci-plonky3)** — STARK variant over Goldilocks/Plonky3 — K-sequence 5.1% faster than Grain LFSR at t=12
- **[ci-quantum-storage](https://github.com/karmaxul/ci-quantum-storage)** — Classical stabilizer / reference implementation
- **[HealChain](https://healchain.org)** — Production deployment using ci-poseidon for on-chain ZK commitments

## Deployed Verifier Contracts (Sepolia)

| Width | Address |
|---|---|
| t=2 | `0x43bBb210d78A5Ce79F99741D6335B478194080D0` |
| t=3 | `0x75cc3fF2905e328E199Fda66c200244112147084` |
| t=4 | `0x310273499087dDd432156013478d6B2c7ac15567` |
| t=6 | `0x77A05B1d95a91607048700715438932eDb772ced` |

All four verified on Sepolia Etherscan. Call `verifyProof(uint256[2],uint256[2][2],uint256[2],uint256[1])` returns `bool`.

*"The symmetry is not in the presentation. It is in the structure of matter itself."*