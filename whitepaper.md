---
title: "EternaX: Post-Quantum Market Infrastructure for Institutional Finance"
email: "info@eternax.ai"
twitter: "@eternaXLabs"
date: "April 2026"
---

## Authors

[**Dariia Porechna**](https://www.linkedin.com/in/dariia-porechna/) | Co-founder, EternaX Labs | [dariia.p@eternax.ai](mailto:dariia.p@eternax.ai)

[**Parthh Sharad Birla**](https://www.linkedin.com/in/parthh-sharad-birla-b3607bb4/) | Co-founder, EternaX Labs | [parth.b@eternax.ai](mailto:parth.b@eternax.ai)

[**Dr. Chen Feng**](https://scholar.google.com/citations?user=D8b0l-EAAAAJ) | Associate Professor, University of British Columbia | [chen.feng@ubc.ca](mailto:chen.feng@ubc.ca)

## Summary

Post-quantum cryptography is not a future security problem. It is a present financial problem. Migration debt, control-plane fragility, privacy contamination, and market-structure repricing are already accruing for every institutional programme operating on quantum-vulnerable blockchain rails.

Google's March 2026 whitepaper compressed the qubit threshold for breaking Bitcoin and Ethereum's cryptography by twenty-fold — from ~9 million to fewer than 500,000 physical qubits. Solana's live testnet confirmed ~90% throughput loss under quantum-safe signatures. Zero of the nine largest institutional tokenized-asset programmes — BlackRock BUIDL, JPMorgan MONY, Franklin Templeton FOBXX, Fidelity FYOXX, Fidelity FIDD, Visa stablecoin settlement, DTCC tokenization, WisdomTree — have disclosed an end-to-end post-quantum roadmap.

The standard answer — replace ECC with NIST post-quantum signatures — is cryptographically sound but operationally destructive. Post-quantum signatures are 10–122x larger than classical ones. At market scale, that delta destroys throughput, raises validator costs, and triggers liquidity flight. The chains that survive will be the ones that never had to pay this tax.

EternaX is high-performance PQ-native market infrastructure without the throughput cliff that makes every other PQ migration commercially unviable. EternaX transactions are backed by SPHINCS+ for conservative post-quantum security and produce a 160-byte permanent authentication record with information-theoretic security and per-transaction privacy

---

## The Installed Base at Risk

The current institutional digital asset stack exposed to legacy signature schemes:

- **Bitcoin:** ~$1.84T (~60%) — ~6.9M BTC in addresses with permanently exposed public keys
- **Ethereum (L1 + L2s):** ~$454B (~15%) — ~$200B in stablecoins and tokenized RWAs governed by admin keys Google identifies as quantum-vulnerable
- **Multi-chain assets (primarily stablecoins):** ~$286B (~9%) — $317B+ total stablecoin market cap, $33 trillion in transaction volume in 2025

This is collateral, payments flow, leverage, and market structure. The institutional programmes building on these rails represent the largest names in global finance: BlackRock's BUIDL ($2.85B across nine blockchains), JPMorgan's MONY (tokenized money market fund on Ethereum), Visa ($3.5B annualized stablecoin settlement on Solana), DTCC (tokenizing U.S. Treasuries from H2 2026), Fidelity's FIDD (institutional stablecoin on Ethereum, launched February 2026). Not one has a disclosed end-to-end post-quantum cryptographic roadmap.

Post-quantum risk does not need a quantum breakthrough to trigger migration. It only needs to enter institutional risk horizons. Once it does, market structure responds mechanically: collateral haircuts compress leverage, margin requirements rise, market makers widen spreads, custodians restrict support, and issuers reroute to safer rails. A stablecoin backed 1:1 by dollars should not trade at a rail-induced discount. A tokenized Treasury fund backed by U.S. government securities should not absorb blockchain cryptographic risk.

Assets whose value derives from outside the blockchain — stablecoins, tokenized treasuries, tokenized deposits, and most RWAs — should not be contaminated by avoidable blockchain-native cryptographic debt simply because the wrong rail was chosen at issuance. The blockchain is the rail. It is not the source of value. Rails should not impose permanent liabilities on the assets they carry.

---

## Institutional Risk Before Theft

The market is asking the wrong question. "When will wallets be cracked?" skips the enterprise consequences that arrive first and cost more.

| Consequence | What it means |
|---|---|
| **Migration debt** | Future cost of re-platforming issuance, wallets, custody, exchange support, and compliance. Accrues at issuance time, not at break time. Every new asset on a weak rail compounds the debt. |
| **Control-plane fragility** | Admin keys governing mint/burn/freeze authority, governance multisigs, and bridge attesters concentrate institutional value in surfaces more directly attackable than dispersed user wallets. Google estimates ~$200B in stablecoins and tokenized RWAs on Ethereum governed by such keys — crackable in <15 hours on a fast-clock CRQC. |
| **Privacy contamination** | Balances, counterparties, flow timing, and treasury movements on public rails carry permanent retroactive exposure. State actors are already collecting blockchain data for future decryption — the harvest-now-decrypt-later threat accumulates silently as the on-chain record grows. |
| **Rail-induced asset contamination** | Assets issued on non-PQ-safe rails absorb a market risk premium their underlying credit, legal structure, or reserve quality would not otherwise justify. |
| **Vendor dependence** | The institution's migration is governed by its slowest supplier. "The chain will upgrade later" does not fix the signing perimeter of the custodian, transfer agent, or bridge provider. |
| **Market-structure repricing** | Boards, auditors, regulators, and counterparties can begin applying risk haircuts and disclosure requirements today — none require a quantum computer, only institutional awareness reaching the level of the public technical record. |

Four repricing mechanisms can trigger without any CRQC existing: fiduciary-duty questions from boards, disclosure obligations flagged by auditors, quantum-exposure reporting required by regulators, and risk haircuts applied by institutional counterparties pricing collateral. Google's paper, covered by Bloomberg, CoinDesk, and the Financial Times within hours of publication, has accelerated that process by years.

---

## The Clearest Signal: Timing Is Now

On March 30, 2026, two independent research groups published the same conclusion on the same day.

**Google Quantum AI** — co-authored with the Ethereum Foundation and Stanford — lowered the physical qubit threshold for breaking secp256k1 by approximately twenty-fold: from ~9 million to fewer than 500,000, running in minutes on superconducting architecture. Google's authors called the expected emergence of CRQCs "a singular discontinuity in the history of digital security" and stated explicitly that a threshold model — no gradual warning, no observable approach — is the correct planning assumption.

**Oratomic / Caltech** showed the same attack executes with as few as 9,739 atomic qubits in under three years. Oratomic co-founder Manuel Endres has already trapped arrays of 6,000 atomic qubits. The hardware trajectory is concrete, not theoretical.

> "It is conceivable that the existence of early cryptographically relevant quantum computers may first be detected on the blockchain rather than announced."
> — Google Quantum AI Whitepaper, March 30, 2026

> "My confidence in a Q-day by 2032 has risen sharply. I now see at least a 10% chance that a quantum computer could recover a secp256k1 private key within six years."
> — Justin Drake, Ethereum Foundation researcher and co-author of Google quantum whitepaper

The rest of the world is not waiting. Cloudflare has completed its post-quantum migration. Apple, Google, and the U.S. government have all set internal migration targets of 2029–2030. Google's Android 17 will ship PQ digital signature protection natively — meaning over three billion mobile devices will have PQ signatures by default before most blockchains have a migration plan. The institutional blockchain stack — carrying $317B in stablecoins and $36B in tokenized RWAs — is the outlier, not the standard.

---

## The Underestimated Constraint

Most "just upgrade signatures" narratives collapse on a hard constraint: post-quantum cryptography fundamentally changes blockchain economics.

Bitcoin's permissionless ownership model depends on a specific kind of cryptography at a specific price point. Elliptic-curve signatures solved three problems in a single, compact object: they link a persistent identity to a key, authorize a concrete message, and give every node a small-to-broadcast and cheap-to-verify validity predicate. Who, what, and a yes/no answer — all in 64 bytes. That composition was not a stylistic choice. It was the only configuration that made unlimited decentralization compatible with finite bandwidth.

Post-quantum signature schemes preserve the same all-in-one structure, but at a radically different price. Kilobyte-scale signatures shift costs onto validation, propagation, and storage at the network edge. At chain scale, signature size and verification cost compound into a propagation tax, a verification tax, and an archival tax. Together, these become a decentralization tax — shrinking the set of viable validators until the network is no longer credibly neutral.

| Scheme | Signature Size | vs. ECDSA | vs. EternaX |
|---|---|---|---|
| Classical ECC (ECDSA / EdDSA) | ~64 B | 1x | — |
| **EternaX dual-layer record** | **160 B** | **2.5x** | **1x** |
| FN-DSA / Falcon-512 (Ethereum direction) | ~690 B | ~10.6x | 4.3x |
| Falcon-1024 (Algorand mainnet, Nov 2025) | ~1,330 B | ~20x | 8.3x |
| ML-DSA / CRYSTALS-Dilithium (NIST FIPS 204) | ~2,420 B | ~37x | 15.1x |
| SLH-DSA / SPHINCS+-128s (Circle Arc choice) | ~7,856 B | ~122x | 49x |

Moving from 64B to 690B signatures — the *smallest* NIST option Ethereum is exploring — imposes ~31% TPS loss. On Solana, live testnet data from Project Eleven and the Solana Foundation (April 2026) confirmed ~90% throughput loss under quantum-safe signatures. Circle chose SLH-DSA-SHA2-128s for Arc at 7,856 bytes per signature — 122x larger than Ed25519 — and explicitly deferred validator hardening to a "long-term" phase because the performance implications remain unresolved.

| Chain | Modeled TPS Loss | Live Testnet Result | PQ Roadmap |
|---|---|---|---|
| Solana | ~77% | **~90%** (Project Eleven, Apr 2026) | None — testnet only |
| Sui | ~69% | No published testnet | None disclosed |
| Ethereum | ~31% | Devnets in progress | Partial — base-layer by 2029; contracts and L2s separate |
| **EternaX** | **~2%** | Protocol-native; no retrofit | Native — information-theoretic scheme |

Markets do not accept permanent performance haircuts for security upgrades. They route around them.

---

## Solution

Post-quantum migration is usually framed as a key-replacement problem. For blockchains, however, it is more fundamentally an infrastructure problem — and an infrastructure opportunity.

The standard answer is straightforward: replace ECC with NIST-standardized post-quantum signatures. This approach is cryptographically sound, but it penalizes the system with a permanent size tax that every node and user has to pay. The history of ECDSA in Bitcoin shows why this matters: the particular price vector of small, non-interactive, publicly verifiable signatures under a classical hardness assumption is what made permissionless decentralization physically possible. As that price vector changes, the question is whether the same abstraction remains viable — or whether it was an artifact of a specific moment in cryptographic history.

SILMARILS changes that cost curve. It gives post-quantum blockchain architectures a path to a **160-byte permanent authentication record**, information-theoretic long-term security, and per-transaction privacy, while anchoring post-quantum unforgeability in a conservative post-quantum cryptography standard.

The new paper, **"SILMARILS: Information-Theoretic and Quantum-Secure Designated-Verifier Signatures,"** a joint work by UBC and EternaX Labs, gives the formal construction, security model, and proofs behind that claim.

### Motivation

Most blockchains were built around a convenient cryptographic bargain. Elliptic curves, often ECDSA and Ed25519, made identity, authorization, and public verification fit into 64 bytes. That small object became the default shape of a blockchain transaction — and almost every chain that followed inherited it as an unexamined default. Accounts, transactions, smart-contract calls, multisigs, bridges, rollups, privacy chains — all anchored to the same compact object and the same discrete-log bargain.

Post-quantum cryptography changes the price of that bargain. The NIST-standardized post-quantum signature schemes are much larger: ML-DSA signatures are measured in kilobytes, FN-DSA is smaller but still an order of magnitude larger than today's signatures, and SLH-DSA/SPHINCS+, the most conservative hash-based option, is larger still.

For many systems, that cost is acceptable. For a high-throughput blockchain, it compounds across bandwidth, storage, validator load, sync time, archive size, and node economics. A testnet can survive large signatures, but it cannot pretend that 10x to 100x authentication growth is invisible at institutional scale.

The motivation behind SILMARILS is demonstrating that information-theoretic techniques can deliver compact verification artifacts, allowing high-performance post-quantum-safe blockchain architectures without carrying the full on-chain footprint of standardized PQ signatures.

### What the Paper Contributes

The paper provides the formal construction, security model, and proofs for SILMARILS.

At a high level, SILMARILS is built from a small algebraic core over a finite field and perfect 2-out-of-2 Shamir secret sharing. It supports two complementary modes:

1. **A two-party transferable designated-verifier mode** with designated-verifier simulatability and EUF-CMA-style unforgeability against non-designated verifiers in the ROM and QROM.
2. **A three-party information-theoretic mode** in the broadcast model of Fitzi et al., with simulation-based security and error 1/p, extended to quantum adversaries with classical inputs and outputs.

Although information-theoretic signatures are known to be possible, existing constructions do not provide efficient, reusable, and simulation-secure signatures in the multi-party, multi-use setting. The central contribution of SILMARILS is achieving information-theoretic security while retaining efficiency, scalability, and practical deployability for modern distributed systems.

That is why SILMARILS is interesting for blockchains: it is a novel authentication building block for systems where validators sit inside the validity path, records live forever, and size directly impacts infrastructure cost.

### The Post-Quantum Security Cost Curve

EternaX L1 blockchain uses SILMARILS inside a dual-layer authentication design. The stack separates what should be conservative from what should be optimized for performance.

**SPHINCS+** provides the post-quantum security anchor. It is NIST-standardized as SLH-DSA, a conservative hash-based choice that avoids lattice assumptions, pairings, hidden algebraic structure, and trusted setups.

**SILMARILS** provides the compact permanent authentication record: **128 bytes**, plus a **32-byte verification artifact**, for **160 bytes total**.

That separation changes the cost curve. The system keeps conservative post-quantum assurance where it matters, while the permanent blockchain record becomes compact, information-theoretic, and privacy-preserving.

| Scheme | Signature size | Relative to ECDSA |
| --- | --- | --- |
| ECDSA / Ed25519 | ~64 B | 1x |
| FN-DSA / Falcon-512 | ~666 B | ~10x |
| ML-DSA-44 | ~1,312 B | ~20x |
| SLH-DSA / SPHINCS+-128s | ~7,856 B | ~123x |
| **EternaX dual-layer record** | **160 B** | **2.5x** |

Standard post-quantum signatures can fit in a block, but the question is whether a post-quantum chain can keep full nodes practical, validators broadly accessible, and transaction volume institutional-scale without making authentication overhead the dominant long-term tax.

Post-quantum security that destroys performance is not a complete solution.

### How Designated Verification Fits in Blockchains

Designated-verifier signatures are often discussed as if they are unsuitable for blockchains because they are not ordinary public signatures. That objection assumes the wrong target.

Blockchains do not need every cryptographic object to be a standalone public signature forever. They need transactions to be authorized, accepted by validators, committed through consensus, and auditable under the rules of the system. Those requirements are related, but they are not identical.

This is where SILMARILS fits. Validators are not passive readers of public signatures. They are active participants in the consensus process: they receive transactions, evaluate authorization, apply state-transition rules, and finalize the ledger under protocol rules. The designated-verifier model matches that architecture instead of forcing every authorization artifact to behave like a forever-public standalone signature.

That is also why the paper matters beyond the 160-byte number. It formalizes the security of this model: designated-verifier simulatability, unforgeability against non-designated parties, simulation-based security in the three-party setting, and analysis in both classical and quantum random-oracle models.

### Long-Term Records Need a Different Posture

Standard post-quantum signatures are the right tool for most jobs, and SPHINCS+ is the conservative choice among them. But after security is solved by adopting a standardized post-quantum signature, blockchains as resource-constrained systems have a second problem: records are permanent.

For stablecoins, tokenized treasuries, tokenized deposits, RWAs, exchanges, and market infrastructure, the relevant horizon is the lifetime of the asset, the audit trail, the regulator, the court record, and the archive.

SILMARILS gives the permanent authentication record information-theoretic security: that means the record is not merely relying on a hardness assumption against known quantum algorithms, but has a stronger long-term integrity posture for the part of the system that lives forever.

That is the real meaning of the 160-byte record: it is smaller, but size is not the whole point. It is a strategic allocation of trust, cost, and permanence.

### Auditable Privacy — PQ-Safe at Both Layers

Post-quantum migration forces a privacy decision that most discussions overlook.

A standard PQ chain that publishes the same verification key across many transactions inherits the same core privacy failure as classical public blockchains. Once a counterparty, analytics vendor, or state actor links the key to an institution, the transaction graph accumulates forever. Under the harvest-now-decrypt-later threat, every treasury movement, counterparty relationship, and settlement flow recorded on a public rail today is being archived for retroactive decryption once quantum capabilities mature.

The usual answer is zero-knowledge proofs. But post-quantum-compatible ZK generally means larger proofs, heavier proving, and more complex systems. That may be acceptable for some applications. It is not a free answer for high-throughput settlement.

EternaX's privacy layer is built on the same information-theoretic foundations as its authorization layer. Transaction flows, balances, and counterparty relationships on EternaX are private not just from today's adversaries, but from any future adversary regardless of computational resources. Harvested EternaX transaction data cannot be retroactively decrypted by a quantum computer — because the privacy model does not rest on computational hardness assumptions.

Compare this to the alternatives:

| System | Privacy Model | PQ-Safe Privacy? | HNDL Protection |
|---|---|---|---|
| Ethereum / Solana | Public-by-default | No | None |
| Zcash (Sapling) | Trusted-setup ZK | No — setup vulnerable to on-setup quantum attack | Historical shielded transactions retroactively exposed |
| Monero | Ed25519 ring signatures | No — quantum-vulnerable | None |
| Circle Arc | Deferred to post-mainnet phase | Unresolved | HNDL exposure from day one of mainnet |
| **EternaX** | **Information-theoretic** | **Yes — both authorization and privacy layers** | **Structurally neutralized** |

The institutional requirement for on-chain privacy is not secrecy or opacity, but controlled disclosure: confidential to the market, auditable to the right party, and durable under post-quantum threat models. SILMARILS supports per-transaction unlinkability and auditable selective disclosure as structural properties of the authentication layer.

### Outlook

Quantum computing is a threat to today's blockchain cryptography, but it is also a forcing function. It gives the industry a reason to reassess inherited assumptions: that authentication must look like ECDSA forever, that privacy requires heavy ZK machinery, and that post-quantum security necessarily means accepting a permanent size tax.

With the SILMARILS paper, our contribution is to give the cryptographic construction and proofs for that direction. The concrete ledger architecture integration is coming in a separate companion publication.

The goal is not only to survive the quantum transition. It is to use it to build better rails: native, compact, private, auditable, and fast enough for the next generation of market infrastructure.

---

## Full-Stack Post-Quantum Infrastructure

EternaX is not only a PQ-safe execution layer. It is a complete market infrastructure stack designed for the full institutional workflow: **Preserve → Migrate → Settle → Trade → Pay**.

**Post-Quantum Settlement and Execution Layer** — PQ-native execution and settlement with auditable privacy and ~120ms spendable finality. Deterministic capped fees (<$0.001 target). MEV-resistant execution.

**Post-Quantum Issuance and Tokenization Rails** — Day-one PQ-native issuance for stablecoins and RWAs, with issuer-grade mint/burn governance, compliance hooks, and auditable privacy settlement. Issue with no migration debt from the first transaction.

**Post-Quantum Migration and Interoperability Rails** — Move assets from existing chains into PQ-native settlement paths via vault and bridge infrastructure. PQ Vault for ETH/EVM assets. PQ Migration Bridge for cross-chain migration.

**Post-Quantum Wallet, Custody, and Policy Controls** — PQ signing, wallet policies, custody controls, and agent permissions. KYA-ready policy framework for institutional custody integration.

**Post-Quantum Market Infrastructure Venues** — High-velocity trading and information markets powered by PQ-safe collateral and agentic users. PQ Perpetuals Exchange. PQ Prediction Markets.

### Traction

As of testnet (published counting rules):

- **PQ-safe settlement layer:** Live on testnet
- **Prediction markets:** Live on testnet
- **On-chain transactions:** 1,000,000+
- **Prediction market bets:** 475,000+

---

## Two Migration Paths

- **Native PQ issuance:** Stablecoins and RWAs mint PQ-native from day one, with EternaX as canonical settlement rail. Zero migration debt from the first transaction.

- **Migration-to-safety:** Ethereum and Bitcoin assets migrate to EternaX for PQ-safe trading, settlement, and collateral use — without waiting for base-layer upgrades that may take years, may not cover deployed contracts, and may impose commercially prohibitive throughput penalties.

When you mint on a non-PQ rail today, you embed migration debt: wallet upgrades, custody coordination, exchange support, liquidity fragmentation, privacy contamination, and vendor dependence. That debt gets called at the worst possible time — and the cost is measured in years and hundreds of millions.

The issuer rule is simple: mint PQ-native on PQ-native settlement. The cost of evaluating PQ-native issuance infrastructure today is a fraction of the coordination cost of migrating an established programme later. Legacy chains are time-bounded liquidity venues, not source of truth.

---

## Conclusion

Every institutional digital asset programme faces the same fork: issue on rails that guarantee a future migration event, or build on infrastructure that was never designed to need one.

Post-quantum safety is a bandwidth and verification bill most chains cannot afford. Solana's live testnet confirmed ~90% throughput loss. Ethereum's roadmap extends to 2029 for base-layer only — contracts, L2s, and bridges are separate. Circle's Arc chose a 7,856-byte signature and deferred validator hardening indefinitely. Bitcoin has five competing proposals and no coordination mechanism.

EternaX gets post-quantum security for free: 160-byte authentication records, ~2% TPS overhead, information-theoretic security at both authorization and privacy layers, ~120ms spendable finality, and a full-stack institutional workflow from issuance to settlement.

The institutions that act before the market forces the reckoning will be the architects of the next institutional standard. Those that defer will be the subjects of an expensive, public, and entirely avoidable migration.
