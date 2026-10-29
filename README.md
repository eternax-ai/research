# EternaX Research

Research by [EternaX Labs](https://eternax.ai) on post-quantum authorization for institutional digital assets.

Every action that moves or changes a digital asset (releasing custody, minting or freezing a stablecoin, releasing collateral, admitting a holder, upgrading a contract) is authorized today by an ECDSA or EdDSA signature. EternaX is the post-quantum authorization layer for these actions. It requires NIST post-quantum signatures, SLH-DSA (FIPS 205) by default and ML-DSA (FIPS 204) where throughput requires it, under the custody, tokenization and EVM systems institutions already run, and keeps the signature algorithm replaceable afterwards.

This repository indexes the research behind that design: papers, cryptanalysis, institutional risk reports, and the open-source code that implements them.

## Research areas

| Area | Problem | Output |
|---|---|---|
| Distributed authorization | Keeping t-of-n approval when the signature scheme cannot be threshold-signed | [arXiv:2607.08226](https://arxiv.org/abs/2607.08226), [`dual-gate-mpc`](https://github.com/eternax-ai/dual-gate-mpc) |
| Architecture boundaries | Which properties a post-quantum distributed authorization design can combine | [arXiv:2609.03547](https://arxiv.org/abs/2609.03547) |
| Compact authentication | Small, quantum-secure authentication records for ledgers | [arXiv:2605.03230](https://arxiv.org/abs/2605.03230), [`silmarils-paper`](https://github.com/eternax-ai/silmarils-paper) |
| Hash-function cryptanalysis | Collision attacks on step-reduced SHA-256 | [39-step SHA-256](#collision-attacks-on-39-step-sha-256) |
| Bitcoin custody | Keeping Bitcoin keys out of a quantum attacker's reach before Bitcoin verifies post-quantum signatures | [One-Time Vaulting](#one-time-vaulting-for-bitcoin), [`eternax-bitcoin-vault`](https://github.com/eternax-ai/eternax-bitcoin-vault) |
| Institutional exposure | Where classical signatures sit in custody, issuance, collateral and settlement, and what migration costs | [Reports](#reports) |

## Papers

### The Native-Signature Boundary in Post-Quantum Distributed Authorization

Dariia Porechna · [arXiv:2609.03547](https://arxiv.org/abs/2609.03547) · September 2026

Classifies distributed authorization designs by three properties: native-signature compatibility, unilateral-signing resistance and threshold-layer agility. The families covered are specialized threshold signatures, generic MPC signing, distributed hash-based constructions, programmable multisignature and dual-gate authorization, and threshold-authorized HSM signing. No surveyed family provides all three properties. A migration impact surface identifies which components of each design change with the signature algorithm.

### Threshold Authorization Without Threshold Signatures: Signature-Agnostic MPC Custody

Dariia Porechna · [arXiv:2607.08226](https://arxiv.org/abs/2607.08226) · July 2026 · Code: [`dual-gate-mpc`](https://github.com/eternax-ai/dual-gate-mpc)

A dual-gate architecture that separates member authentication from threshold authorization. Each member signs its approval under any EUF-CMA signature scheme; the quorum jointly produces a threshold seal from Shamir-shared secrets bound to the operation. Migrating from ECDSA to SLH-DSA or ML-DSA is a key rotation rather than a protocol redesign, and members holding keys in commodity HSMs participate through the standard sign API. Below-threshold secrecy is information-theoretic. This is the authorization architecture of EternaX Vault.

### SILMARILS: Information-Theoretic and Quantum-Secure Designated-Verifier Signatures

Hassan Khodaiemehr, Khadijeh Bagheri, Chen Feng (University of British Columbia), Dariia Porechna (EternaX Labs) · [arXiv:2605.03230](https://arxiv.org/abs/2605.03230) · May 2026 · Code: [`silmarils-paper`](https://github.com/eternax-ai/silmarils-paper)

A designated-verifier signature framework over a prime field built from perfect 2-out-of-2 Shamir secret sharing. The two-party mode is a transferable designated-verifier signature, unforgeable for every non-designated verifier (EUF-CMA¬DV) in the random oracle and quantum random oracle models. The three-party mode is a statistically secure signature protocol with error 1/p. Keys and signatures are compact. Native transactions on the Pluto testnet carry an SLH-DSA and a SILMARILS signature.

## Cryptanalysis

### Collision attacks on 39-step SHA-256

October 2026 · [Write-up](https://eternax.ai/blogs/sha-256-39-step-collisions-below-generic-search/index.html) · [HashSmash board](https://www.yukon.org/hashsmash)

A collision attack on SHA-256 reduced to 39 of its 64 steps that costs less than generic search under the HashSmash board's cost model. It is built on the 39-step differential characteristic and semi-free-start pair of ePrint 2026/1120, whose authors estimated their own method at 2^168. Dariia Porechna's row-16 claw construction turned the characteristic into a differential attack; Sebastian R. Wain (sraiw), Jbenisek and lamb356 extended and optimized it in public filings on the board.

| Accounting | Attack | Reference |
|---|---|---|
| Board cost model | 2^118.35 (accepted filing) | 2^124.83, best accepted generic search |
| Literature convention | ~2^127.6 | 2^168, the published method's own estimate |

The figures are complexity estimates under declared heuristics, accepted by the board's reviewers and not yet peer-reviewed; later filings on the board refine the tail measurement. The result does not extend to full SHA-256, and SLH-DSA's security does not rely on SHA-256 collision resistance. A joint technical report is in preparation.

## Bitcoin custody

### One-Time Vaulting for Bitcoin

Paarrthhh Birla, Dariia Porechna · October 2026 · [Write-up](https://eternax.ai/blogs/one-time-vault/index.html) · Code: [`eternax-bitcoin-vault`](https://github.com/eternax-ai/eternax-bitcoin-vault)

A Bitcoin custody method built from a standard P2WSH output locked to 100 fresh ECDSA keys that must all sign, each vault spent exactly once. At rest, only a SHA-256 script hash is on chain. In flight, an attacker must derive all 100 private keys before the next block, against one key for an ordinary spend. With Google Quantum AI's 2026 estimate of about nine minutes per key on a primed first-generation fast-clock machine, an attacker wins the race against a single-key spend about 41% of the time; against the 100-key vault it needs about a hundred such machines in parallel for the same odds. Bitcoin Core's default relay policy accepts the spend as standard. A 100-key spend was confirmed on mainnet in block 973,546 at 2,759 vbytes. The method needs no fork and no miner involvement. It is a work factor for the period before Bitcoin verifies post-quantum signatures, not a substitute for them.

## Reports

Institutional research on post-quantum exposure in digital-asset infrastructure. Index: [eternax.ai/reports](https://eternax.ai/reports/index.html).

| Date | Report | Scope |
|---|---|---|
| Oct 2026 | [The 48 Hours That Rewrote the Cryptographic Threat Model](https://eternax.ai/48-hours-that-rewrote-cryptography.html) | AI-assisted mathematics, Ethereum bunker-mode warnings and lattice-risk concerns; consequences for custody, tokenization, ZK, FHE and privacy chains |
| Sep 2026 | [P(Q Doom) Index](https://eternax.ai/quantum-doom-index.html) | Probability that cryptographically relevant quantum capability arrives before critical infrastructure completes migration: 34% by 2035 |
| Sep 2026 | [Quantum Value at Risk (QVaR) 2026](https://eternax.ai/quantum-value-at-risk-qvar-institutional-digital-assets-2026.html) | $796.7B modeled asset QVaR across 28 institutional programmes; flow and settlement QVaR; 15-network readiness benchmark |
| Sep 2026 | [Post-Quantum Custody Decision Framework](https://eternax.ai/post-quantum-custody-decision-framework.html) | HSM, MPC, threshold post-quantum signatures and crypto-agile authorization compared |
| Aug 2026 | [Post-Quantum Readiness Benchmark 2026](https://eternax.ai/blockchain-post-quantum-readiness-benchmark-2026.html) | 17 networks graded on post-quantum security, crypto-agility, NIST/FIPS and regulatory readiness, custody, privacy and performance |
| Aug 2026 | [Is Hyperledger Besu Quantum-Safe?](https://eternax.ai/besu-quantum-risk.html) | Five coupled migration surfaces in mainline Besu and a remediation path |
| Jun 2026 | [Your Chain Will Not Save You](https://eternax.ai/post-quantum-non-upgradeable-chains-defi-exposure-report.html) | Immutable contracts, frozen standards and custody flows that chain upgrades do not fix, across Ethereum, Besu, Solana, Stellar and Canton |
| Jun 2026 | [The Post-Quantum MPC Custody Crisis](https://eternax.ai/post_quantum_mpc_custody_crisis_hash_based_sphincs_institutional.html) | 15 institutional MPC custody providers; why hash-based signatures do not fit threshold signing |
| May 2026 | [Post-Quantum Exposure Map 2026](https://eternax.ai/post_quantum_exposure_map_institutional_crypto_tokenized_assets.html) | 20+ institutions, 30+ products and 11 chains mapped to post-quantum and privacy exposure |
| May 2026 | [Post-Quantum Signature Security Ranking 2026](https://eternax.ai/post-quantum-signature-security-ranking-2026.html) | NIST post-quantum signature schemes ranked by security assumptions for institutional deployment |
| Apr 2026 | [Cryptographic Migration Debt](https://eternax.ai/post-quantum-cryptography-risk-framework-for-institutions.html) | Framework for the cost of migrating digital-asset programmes off classical signatures |
| Mar 2026 | [Already Broken: Quantum Risk Report Q1 2026](https://eternax.ai/already-broken-quantum-risk-report-q1-2026.html) | 27 institutions and eight migration perimeters in institutional blockchain infrastructure |

## Code

| Repository | Content |
|---|---|
| [`dual-gate-mpc`](https://github.com/eternax-ai/dual-gate-mpc) | Reference implementation of dual-gate custody (arXiv:2607.08226): Rust reference, TypeScript port with the setup ceremony, Solidity `CustodyGate` contract |
| [`silmarils-paper`](https://github.com/eternax-ai/silmarils-paper) | Rust reference implementation of the SILMARILS two-party transferable designated-verifier mode (arXiv:2605.03230) |
| [`pq-onchainid`](https://github.com/eternax-ai/pq-onchainid) | SLH-DSA and ML-DSA claim verification for ERC-3643 / ONCHAINID compliance flows |
| [`pluto-testnet-tools`](https://github.com/eternax-ai/pluto-testnet-tools) | TypeScript CLI for the Pluto testnet: SLH-DSA and SILMARILS dual-signed transfers and EVM transactions |
| [`eternax-bitcoin-vault`](https://github.com/eternax-ai/eternax-bitcoin-vault) | One-Time Vaulting for Bitcoin: 100-key one-time P2WSH vaults from one BIP-39 seed, with Bitcoin Core regtest and mainnet measurements |
| [`utxo-ots`](https://github.com/eternax-ai/utxo-ots) | One-time hash signatures finalized on the Bitcoin ledger through standard P2WSH, for attestations and single-use seals |

## Testnet

[Pluto](https://eternax.ai/pluto-testnet.html) is EternaX's public EVM-compatible testnet, live since November 2025. Native transactions are signed with SLH-DSA-SHAKE-128s and SILMARILS. Solidity contracts verify SLH-DSA and ML-DSA-65 signatures through precompiles at `0x0404` and `0x0405`. Web wallet, RPC and faucet: [pluto-testnet.eternax.ai](https://pluto-testnet.eternax.ai/web-wallet/).

## Applications

The research is applied in [EternaX Vault](https://eternax.ai/post-quantum-vault.html) (dual-gate post-quantum approval over keys held in existing HSMs, MPC or custodians; live on testnet), PQ-ONCHAINID for compliance claims, PQ-Safe Besu for permissioned EVM networks, and a post-quantum-native settlement network for new issuance. Institutions can test these in a [30-day pilot](https://eternax.ai/pilot.html).

## Citation

BibTeX entries for the papers are in [`CITATION.bib`](CITATION.bib).

## Archive

[`archive/`](archive/) holds 2025 work on on-chain AI agents from before the company's post-quantum focus.

## Team

- [Dariia Porechna](https://www.linkedin.com/in/dariia-porechna), Co-founder. Cryptographer and distributed-systems architect.
- [Dr. Chen Feng](https://scholar.google.com/citations?user=D8b0l-EAAAAJ), Chief Scientist. Associate Professor, University of British Columbia.
- [Paarrthhh Birla](https://www.linkedin.com/in/paarrthhh-birla-b3607bb4/), Co-founder. Growth and partnerships.

Contact: [info@eternax.ai](mailto:info@eternax.ai) · [eternax.ai](https://eternax.ai) · [X](https://x.com/EternaXlabs) · [LinkedIn](https://www.linkedin.com/company/eternax-labs)
