# Formal eternaX Agent Definition

In this document, we formally define the fully autonomous agent operating in the eternaX ecosystem. This formulation allows us to reason about the agent's behavior and interactions and state the security requirements and attack surfaces for this new class of network entities.

## Autonomous On-Chain Agent

Informally, we define an autonomous on-chain agent as a program that can autonomously retrieve data, make decisions using an LLM, and take actions on the blockchain. By "autonomous", we mean that the agent can act without human intervention, and by "on-chain", we mean that the agent is a smart contract deployed on a blockchain. On-chain is a necessary condition for the agent to be autonomous, as it allows the agent to take actions on the blockchain without relying on human for access, ownership, or resources.

## Levels of Autonomy

Current state-of-the-art agents (like ai16z, Truth Terminal, etc.) operate at a lower level of autonomy:
- Require continuous operation of a single computer/server
- Need human oversight and intervention
- Depend on external scheduling mechanisms
- Can only operate when their host infrastructure is running

Our on-chain agent achieves true autonomy through:
- Self-contained execution on the blockchain
- Built-in scheduling at the protocol level
- Continuous operation independent of any single infrastructure
- No requirement for human oversight or external orchestration

## Agent Definition

Formally, an autonomous on-chain agent is defined by the following tuple:

$$A = (S, D, A, T)$$

Where:

- $S$ is the set of possible states of the agent, where each state is a tuple of $(c_t, h_t, b_t)$
  - $c_t$: agent's context at time $t$
  - $h_t$: history of transactions and actions up to time $t$
  - $b_t$: balance of the agent at time $t$
- $D$ is the set of decision engine calls available to the agent (i.e. LLM)
- $A$ is the set of possible actions of the agent, including:
  - Core business logic actions
  - Self-scheduling actions 
  - State management actions
- $T$ is the transition function $T: S × D × A → S$ that defines:
  - How the agent's state updates after actions
  - How the LLM outputs are processed
  - The sequence of contract function calls
  - State transitions based on blockchain events

At each time step $t$, the agent takes its current state $s_t$ and updates it according to the transition function $T$ with the current decision engine $D$ and action $a_t$. The action inflicts a state transition on the agent's state to $s_{t+1}$ and updates the blockchain state. 

The transition function $T$ encodes the actual smart contract code that:
1. Retrieves necessary data (part of $S$)
2. Calls the LLM ($D$)
3. Processes the LLM output
4. Executes the appropriate actions ($A$) including self-scheduling actions
5. Updates the contract state

We define a subset of all possible actions $A$ as the self-scheduling actions $A_{ss}$. When the transition function $T$ is implemented with a self-scheduling action, $T: S × D × A_{ss} → S$, we call $T$ an autonomy loop. The presence of the self-scheduling action allows the agent to schedule itself to run at a future time. This is a key feature of the agent's autonomy, as it allows the agent to plan for future actions and state transitions without relying on human intervention or external orchestration.

## Agent State Evolution

Since the agent is a smart contract, it's state is intrinsically linked to the blockchain state. Let $B_t$ represent the blockchain state at time $t$, and $s_t \in S$ represent the agent's state at time $t$. Here we understand time $t$ relative to the agent's genesis and the progression of time is recorded in increments of state evolutions. This is equivalent to recording the number of times the transition function $T$ has been applied. As such, the agent's state $s_t$ can be thought of as a function of the number of times the transition function has been applied, $s_t = T^t(s_0)$. This is to distinguish the agent's state from the blockchain state, which is recorded as $B_t$ and evolves as result of actions of the agent and other participants on the blockchain. There may be unequally spaced time steps between agentstate evolutions, but we can always normalize the time steps to a continuous function of the number of state evolutions.

The autonomous agent genesis is defined as the moment the contract code with transition function $T$ is deployed. The agent's initial state $s_0 = (c_0, h_0, b_0)$ is the initial set of data and information available to the agent at its genesis. The initial context $c_0$ is the initial set of data and information. The initial history $h_0$ is the initial set of transactions and actions that have occurred on the blockchain up to the agent's genesis. The initial balance $b_0$ is the initial balance of the agent given by the creator of the agent contract.

The evolution of the agent's state can be formalized as follows:
For each time step $t \geq 0$:
   - Agent observes relevant subset of $B_t$ through $c_t$
   - Agent dispatches decision engine call $D_t$ with context $c_t$
   - Agent selects action $a_t \in A$ based on $D_t$ response $r_t$ and current state $s_t$
   - State transition: $s_{t+1} = T(s_t, D_t, a_t)$
   - Action $a_t$ causes blockchain state transition: $B_{t+1} = f(B_t, a_t)$
   - Action $a_t$ updates both the agent's and the blockchain's history: $h_{t+1} = h_t \cup a_t$
   - Agent's new state: $s_{t+1} = (c_{t+1}, h_{t+1}, b_{t+1})$
   - If $a_t$ is a self-scheduling action, the agent schedules itself to run at time $t+1$

## Decision Engine

The decision engine $D: S \times B \rightarrow A$ is a function that takes in the agent's state $s_t$ and the blockchain state $B_t$ and outputs a decision, a selection of an action $a_t \in A$. The decision engine is a black box that is not part of the agent's state. The decision engine is responsible for the agent's behavior and decision making.
A call to a decision engine is a transaction to a compute provider that is responsible for the actual computation, which is typically a large language model (LLM) with RAG and vector DB capabilities. 
Compute providers are listed on-chain with their offered models and associated costs and are selected by the agent based on the cost, speed, reputation, availability of verifiable inference (e.g. TEE), and other criteria. 

### Non-Determinism

Let $D_t$ be a decision engine call at time $t$. The result of $D_t$ is non-deterministic, as it depends on the stochastic nature of the underlying LLM. This creates a fundamental tension with the deterministic nature of blockchain state transitions.

Current industry approaches attempt to resolve this tension through verification mechanisms:

1. Zero-Knowledge Verification:
   Let $D_t$ produce result $r_t$ with proof $\pi_t$. Verification requires:
   
   $$verify(\pi_t, r_t) = true$$

   The computational overhead is:
   
   $$O_{zk} = O(n_{params} \cdot n_{ops})$$

   where $n_{params}$ is the number of model parameters and $n_{ops}$ is the number of operations. This approach, while providing cryptographic guarantees, imposes a high computational overhead over the inference cost and scales poorly with model size.

2. Optimistic Verification:
   Let $D_t$ be a decision engine call with result $r_t$. The result is accepted after a challenge period $c$ unless disputed:
   
   $$accept(r_t) = \begin{cases} 
   true & \text{if no dispute within } c \\
   false & \text{otherwise}
   \end{cases}$$

   The computational overhead is:
   
   $$O_{opt} = n_{watchers} \cdot O_{inference}$$

   where $n_{watchers}$ is the number of watchers. This approach introduces latency proportional to $c$ and requires $n_{watchers} \geq 1$ honest watchers. The overhead is $O_{opt} \geq n_{watchers}x$ inference cost. While requiring less computational resources than zero-knowledge verification, this approach uses interactive fraud proofs in case of disputes that are infamously difficult to implement and test, limiting the utility of the approach.

3. Quorum Verification:
   Let $Q = \{D_1, D_2, ..., D_n\}$ be a set of $n$ decision engine calls. The result is accepted if:
   
   $$| \{D_i \in Q | result(D_i) = result(D_j)\} | \geq k$$

   where $k$ is the quorum threshold. The cost overhead is:
   
   $$O_{q} = n \cdot O_{inference}$$

   This approach allows selecting the security level $n$ according to the application requirements with the resulting inference cost being linear in $n$. 

These verification-centric approaches are fundamentally limited because of the imposed overhead and inability to scale to state-of-the-art models. Most importantly, however, they focus on verifiability rather than utility and creativity of the decision engine, and are thus unsuitable for the decision making process of an autonomous agent. Instead, we would like to view the agent akin to a human decision maker that can take actions based on their utility function, which is a function of the decision engine's output. In this paradigm, the actual reasoning behind a decision is not important, but the decision's utility to the agent is. By virtue of being a smart contract, the action space of the agent is already constrained by the transition function $T$, the blockchain protocol, and the agent's balance. Any action taken by the agent as result of a decision engine call is valid as long as the agent can afford to take it. As an example, a human user can decide to take an on-chain action based on it's own decision making process, even if the reasoning is not rational or incorrect. A human user may decide to swap $10 ETH$ for $USDC$ for any reason, and the action is valid as long as the user has the funds to do so. We would like to extend this paradigm to the agent's decision making process.

To achieve this, we propose a utility-centric approach that embraces the non-deterministic nature of $D_t$ and focuses on the utility of the decision engine's output. On the side of the compute providers, we propose a reputation-based approach that incentivizes them to honestly provide their inference services combined with TEEs to ensure the integrity of the inference for sensitive data. Such approach is justified by the fact that for most applications, the utility of the decision engine's output is more important than the actual reasoning behind the output. This is evidenced by the success of current industry giants like OpenAI, Google, and Anthropic, which are all based on reputation of their inference services that are not verifiable by any means. 

In an on-chain setting, we utilize a limited set of whitelisted compute providers that are required to register the models they offer, associated costs, and inference speeds and put up collateral in the form of staked tokens. TEE-based verification incurs an overhead of:

$$O_{tee} = (1 + \epsilon) \cdot O_{inference}$$

where $\epsilon \approx 0.1$ represents the TEE overhead. This overhead is significantly lower than the verification-centric approaches:

$$O_{tee} \ll O_{zk} \approx 1000x$$

$$O_{tee} \ll O_{opt} \geq n_{watchers}x$$

$$O_{tee} \ll O_{q} = nx$$

while providing practical security guarantees.

## Action Space

The action space is the set of all possible actions that the agent can take defined by the agent's transition function $T$ within the broader context of the blockchain.

