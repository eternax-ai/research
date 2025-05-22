EternaX is an infrastructure layer blockchain network composed of a consensus chain with an EVM-compatible execution environment and an AI-powered cognition layer. 

## Virtual Machine

EternaX is Ethereum Virtual Machine (EVM)-compatible chain, which can be used to launch any existing Ethereum dApps and smart contracts with an extended AI-integrated precompile set and a new set of AI-native transactions. These precompiles are built-in functions that are used to integrate AI inference into the appchain's state transition function and enable native and verifiable on-chain agent execution. They support requesting inference from integrated AI providers, storing and retrieving data from the content layer for augmented generation (RAG or in-context learning), and storing and retrieving AI agent execution history for verifiability and accountability. On-chain agent execution is a new type of transaction that allows for the execution of arbitrary agentic logic on-chain, enabling a wide range of AI-native applications.

### Protocol-Level Autonomy

A fundamental primitive in the EVM runtime is the introduction of protocol-level autonomy through native scheduling. Instead of relying on external keeper networks or centralized automation services, EternaX integrates autonomous execution directly into the protocol. This architectural decision eliminates the need for third-party automation services and creates a foundation for truly self-sustaining smart contracts.

The native scheduling system enables smart contracts to autonomously coordinate future actions through consensus-guaranteed execution. This capability is essential for complex decentralized applications that require reliable, time-based operations without external triggers. By implementing scheduling at the protocol level, EternaX ensures that autonomous operations are as fundamental to the blockchain as transactions themselves.

The integration with the Cognition Layer further enhances the scheduling capabilities. AI providers can be leveraged for dynamic scheduling decisions, enabling adaptive execution based on model predictions and intelligent condition evaluation. Through TEE integration, these AI-enhanced scheduling operations maintain privacy while providing verifiable execution guarantees.

The Cognition Layer provides AI inference services, which are used to power the precompiles, with a robust and transparent verification process to ensure that inference responses (reasoning, prediction, generation, etc.) are derived from legitimate computation.

Smart contracts can now operate independently, adapt to changing conditions, and coordinate complex workflows across the network without relying on centralized coordination or external automation services.

## Cognition Layer

The cognition layer provides a backend to integrate a set of precompiles for AI workflows. The two main components of the cognition layer are:

- Compute: The AI provider registry, which is a marketplace for AI inference services.
- Data: The content layer, which is a fast and globally distributed data service that provides a low-latency and high-throughput data feed.

The two components are tightly integrated and work together to provide a seamless and secure AI inference experience. The AI providers can reach the content layer to retrieve data required for the inference request, such as private datasets, or public datasets like news articles, or other content which can be used for in-context learning or RAG.

### AI Providers

The AI providers are the core component of the Cognition Layer that enables secure and verifiable AI inference. Through a marketplace-style registry, providers offer AI model execution services with different levels of trust, including Trusted Execution Environments (TEEs), where all computations are verifiable and tamper-proof. The registry implements a stake-based security model where providers must lock up collateral, which can be slashed for misbehavior.

Inference requests are automatically matched to suitable providers based on model requirements, pricing, performance metrics or other app preferences.
For sensitive applications, the system ensures reliability through cryptographic attestation at both the provider level (proving secure infrastructure) and per-inference level (proving legitimate computation). This dual attestation approach, combined with economic incentives and continuous monitoring, creates a trustless environment for AI model execution.
Applications with preference for lower latency can either completely forfeit the requirement for verifiable per-inference attestation or utilize optimistic batching with time window attestation.

### Content Layer

The content layer can be seen as a chain-integrated version of a classic content delivery network (CDN) that is a fast and globally distributed data service. The purpose of the content layer is to provide a low-latency and high-throughput data feed. It is operated by a set of Context Nodes providing efficient access to a wide range of data, including AI models, private and public datasets or other content which can be queried and retrieved by AI workflows. Most content is stored off-chain in a distributed manner, with redundancy and geographic dispersion to ensure data availability and durability. Critical data, such as action records, inference attestations, proofs of execution, etc. is stored on-chain by the base layer nodes.

Users can register their content in the content layer and make it available to all applications for as long as they want or make it available to a specific contract for a limited time. They also have the option to store their content on-chain in the base chain, which is more expensive but permanent and provides strong guarantees on availability and durability.

## Consensus Chain

The consensus chain is responsible for achieving consensus between all types of nodes on the general state of the network and ensures a single shared source of truth for all nodes. It implements a variation of the Proof-of-Stake consensus algorithm, which ensures temporal linearity, immutability of the chain's history and permanent data availability without reliance on archival nodes.
