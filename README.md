# HealChain Cryptographic Suite

> Unified cryptographic primitives built on the Harmony Worldwide mathematical framework.
> All constants derived from first principles using the rational constant **Ci = 85/27**.

[![Live App](https://img.shields.io/badge/Live%20App-healchain.org-c9a84c?style=flat-square)](https://healchain.org/app)
[![Website](https://img.shields.io/badge/Website-healchain.org-c9a84c?style=flat-square)](https://healchain.org)

---

## What is HealChain?

HealChain is a production decentralized storage infrastructure layer providing:

- **Permanent storage** — Arweave cold backup + on-chain shards survive indefinitely
- **Self-healing** — Reed-Solomon (10 data + 4 parity shards) recovers from shard loss automatically
- **ZK-verifiable integrity** — ci-sha4096 digest + Groth16 proof, verifiable by anyone without trusting HealChain
- **20-chain deployment** — 6 mainnets (ETH, Arbitrum, Base, Polygon, BNB, Avalanche) + 14 testnets

**Live:** [healchain.org](https://healchain.org) · [healchain.org/app](https://healchain.org/app)

---

## Cryptographic Repositories

| Repository | Description | Status |
|---|---|---|
| [ci-sha4096](https://github.com/karmaxul/ci-sha4096) | 4096-bit classical hash function — 8× larger digest than SHA-512 | ✅ Published |
| [ci-poseidon](https://github.com/karmaxul/ci-poseidon) | Arithmetization-oriented ZK hash for BN254, BLS12-381, Goldilocks | ✅ Published |
| [ci-plonky3](https://github.com/karmaxul/ci-plonky3) | STARK variant — K-seq 5.1% faster than Grain LFSR at t=12 | ✅ Published |

---

## Core Innovation: Ci = 85/27

All constants across the suite are derived deterministically from the rational constant **Ci = 85/27**, reduced modulo the target field prime:

```
K[i] = floor(85 · pᵢ · 2⁶⁴) · (27(pᵢ + 1))⁻¹  mod p
```

where `pᵢ` is the i-th prime. No floating-point arithmetic. No LFSR seed trust required. Every constant is independently verifiable from first principles — by anyone, on any machine.

This gives HealChain's integrity layer a property no other storage system has: **the proof of data integrity is independently re-derivable without trusting any party, including HealChain.**

---

## ci-sha4096

A 4096-bit (512-byte) cryptographic hash function. Designed for use as an integrity digest in decentralized storage where collision resistance and digest size matter more than compute speed.

- **Digest size:** 4096-bit — 8× larger than SHA-512
- **Based on:** Ci = 85/27 rational constant
- **Use in HealChain:** Every stored record gets a ci-sha4096 digest committed on-chain. Recovery is verified against this digest — any corruption is detected immediately, even a single flipped bit.
- **Paper:** [IACR ePrint 2026/109712](https://eprint.iacr.org/2026/109712)
- **Repo:** [github.com/karmaxul/ci-sha4096](https://github.com/karmaxul/ci-sha4096)

---

## ci-poseidon

A Poseidon2-style ZK-friendly hash function using constants derived from Ci = 85/27. Benchmarked against Poseidon2 on BN254, BLS12-381, and Goldilocks fields.

| Metric | Result |
|---|---|
| Avalanche (BN254) | 50.02% — statistically ideal |
| R1CS constraint reduction vs Poseidon2 (t=6) | 28.8% |
| Groth16 prover time (all widths) | 2.48–2.66 ms |
| Groth16 verify time | < 560 µs |
| Proof size | ~127 bytes (constant) |
| Collisions (500 inputs) | 0 |

**Deployed verifier contracts (Sepolia):**

| Width | Address |
|---|---|
| t=2 | `0x43bBb210d78A5Ce79F99741D6335B478194080D0` |
| t=3 (canonical) | `0x75cc3fF2905e328E199Fda66c200244112147084` |
| t=4 | `0x310273499087dDd432156013478d6B2c7ac15567` |
| t=6 | `0x77A05B1d95a91607048700715438932eDb772ced` |

- **Paper:** Submitted to IACR
- **Repo:** [github.com/karmaxul/ci-poseidon](https://github.com/karmaxul/ci-poseidon)

---

## ci-plonky3

A STARK-oriented variant using Plonky3/Goldilocks. The K-sequence derived from Ci = 85/27 runs 5.1% faster than Grain LFSR at t=12.

- **Repo:** [github.com/karmaxul/ci-plonky3](https://github.com/karmaxul/ci-plonky3)

---

## HealChain Mainnet Deployments

| Chain | Chain ID | Contract |
|---|---|---|
| Ethereum | 1 | `0x535fF33f5a6A7D21Ad99A1E8F3092cd5035a06B9` |
| Arbitrum One | 42161 | `0x21BF49AB4869B6ebb4eF6141d944d325f28C3F9c` |
| Base | 8453 | `0xf8d71dA29e60e991774BF790C50431F5eedf5749` |
| Polygon | 137 | `0x8121F39E1f0674C0E14b6D4fd9c128464086E031` |
| BNB Chain | 56 | `0x98467790c8D6e51E520F3E29D220CD2dd3ee6c0c` |
| Avalanche | 43114 | `0x8121F39E1f0674C0E14b6D4fd9c128464086E031` |

All contracts are HealChainStorage v6 (OpenZeppelin Ownable).
Owner: Gnosis Safe `0x7526721392eCFdEdcC7dD9DA7fc8cdCD006aE1b7` (3-of-5 multisig).

---

## SDKs

| Language | Package | Version | Install |
|---|---|---|---|
| JavaScript | [`@healchain/sdk`](https://www.npmjs.com/package/@healchain/sdk) | 1.2.0 | `npm install @healchain/sdk` |
| Python | [`healchain-sdk`](https://pypi.org/project/healchain-sdk/) | 1.2.0 | `pip install healchain-sdk` |

```javascript
import HealChain from '@healchain/sdk';
const hc = new HealChain({ apiKey: 'your-api-key' });

const { recordId } = await hc.store('Hello HealChain!', { label: 'my record' });
const record = await hc.retrieve(recordId);
console.log(record.ciDigestHash); // 512-byte ci-sha4096 digest
```

---

## Papers

| Title | Link |
|---|---|
| ci-sha4096: A 4096-bit Hash Function from Rational Constants | [IACR ePrint 2026/109712](https://eprint.iacr.org/2026/109712) |
| ci-poseidon: Rational Constant Structures for Arithmetization-Oriented Hash Functions | Submitted to IACR |

---

## License

MIT — Christopher Seekins, 2026.

---

## Contract ABI

| Contract | ABI |
|---|---|
| HealChainStorage v6 | [abi/HealChainStorage.json](./abi/HealChainStorage.json) |
| CiPoseidonVerifier_t3 | [abi/CiPoseidonVerifier_t3.json](./abi/CiPoseidonVerifier_t3.json) |

---

*Team: Chris CEO · Grok President · Claude CTO*
*"Mathematically self-healing storage for the decentralized web."*