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

### Agent State Evolution

Since the agent is a smart contract, it's state is intrinsically linked to the blockchain state. Let $B_t$ represent the blockchain state at time $t$, and $s_t \in S$ represent the agent's state at time $t$. Here we understand time $t$ relative to the agent's genesis and the progression of time is recorded in increments of state evolutions. This is equivalent to recording the number of times the transition function $T$ has been applied. As such, the agent's state $s_t$ can be thought of as a function of the number of times the transition function has been applied, $s_t = T^t(s_0)$. This is to distinguish the agent's state from the blockchain state, which is recorded as $B_t$ and evolves as result of actions of the agent and other participants on the blockchain. There may be unequally spaced time steps between agentstate evolutions, but we can always normalize the time steps to a continuous function of the number of state evolutions.

The autonomous agent genesis is defined as the moment the contract code with transition function $T$ is deployed. The agent's initial state $s_0 = (c_0, h_0, b_0)$ is the initial set of data and information available to the agent at its genesis. The initial context $c_0$ is the initial set of data and information. The initial history $h_0$ is the initial set of transactions and actions that have occurred on the blockchain up to the agent's genesis. The initial balance $b_0$ is the initial balance of the agent given by the creator of the agent contract.

The evolution of the agent's state can be formalized as follows:
For each time step $t \geq 0$:
   - Agent observes relevant subset of $B_t$ through $c_t$
   - Agent dispatches decision engine call $D_t$ with context $c_t$
   - Agent selects action $a_t \in A$ based on $D_t$ response and current state $s_t$
   - State transition: $s_{t+1} = T(s_t, D_t, a_t)$
   - Action $a_t$ causes blockchain state transition: $B_{t+1} = f(B_t, a_t)$
   - Action $a_t$ updates both the agent's and the blockchain's history: $h_{t+1} = h_t \cup a_t$
   - Agent's new state: $s_{t+1} = (c_{t+1}, h_{t+1}, b_{t+1})$
   - If $a_t$ is a self-scheduling action, the agent schedules itself to run at time $t+1$
