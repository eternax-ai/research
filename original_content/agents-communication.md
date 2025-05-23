# Agent Communication

As we move towards a multi-agent ecosystem, we need to consider how agents will communicate with each other.

Within the eternaX ecosystem, agents can be viewed as smart contracts, and thus, the communication between agents is the same as the communication between smart contracts.

## Registry

By virtue of being a smart contract, each agent has a unique address. If an agent's creator wants their agent to interact with other agents, the creator may register the agent's address and the agent's functions in a registry that is accessible to the public (on-chain). Voluntary registration allows for the creation of an ecosystem, while still allowing creation of private agents not callable by the public.
A public on-chain directory of agents, makes it easy for agents to discover each other and interact without needing off-chain information from external tools and explorers (e.g. ABI), making the ecosystem more self-contained.

Agents can query the registry to discover other agents and their available functions. This allows agents to dynamically compose interactions between themselves to achieve complex behaviors.

Agent service entry in the registry shall include:
1. **Service Type**: The type of service provided by the agent
2. **Input Schema**: The input schema of the agent's function
3. **Output Schema**: The output schema of the agent's function
4. **Base Cost**: The base cost of the agent's function
5. **Agent Address**: The address of the agent
6. **Agent Reputation**: The reputation of the agent (not settable by the agent creator, see [Reputation System](#reputation-system))

Using the lookup function `findService(string serviceType, uint256 reputationThreshold)`, an agent can discover all agents that provide the specified service and have a reputation greater than the desired threshold.

## Communication

In the context of the blockchain, communication between agents is done through function calls structured as transactions. This allows us to leverage the inherent properties of blockchain technology to provide a superior foundation for agent communication:

1. **Verifiable Interfaces**: 
   Since all function signatures and parameters are publicly verifiable on-chain, there is no need to trust external documentation or APIs. Such interface compliance, enforced at the protocol level, eliminates version mismatch issues common in off-chain systems

2. **Natively Atomic Execution**:
   With all interactions being atomic transactions, partial failures or inconsistent states are not possible. Agent actions are guaranteed to be executed or completely rolled back.

3. **Protocol-Level Security**:
   Removed need to expose endpoints to the internet, eliminates common attack vectors like DDoS, MITM, and API abuse. All interactions are cryptographically signed and verified by the network.

4. **Cost Transparency**:
   Cost structure is predictable and verifiable with no hidden API costs or rate limits. Clear economic incentives for efficient operation align with network efficiency.

5. **Composability**:
   Smart-contract based agents become composable by design as functions can be chained in single transactions to achieve complex behaviors.

6. **Audit Trail**:
   All interactions are permanently recorded on-chain, providing a complete history of agent behavior. This enables trustless verification of past interactions without additional audit systems.

7. **Permissionless Innovation**:
   Creation and registration of new agents is permissionless without the need for API keys or access control. This allows for an open ecosystem of composable services interacting without the need of external approval.

By building on these fundamental blockchain properties, we create an agent communication system that is more robust, secure, and efficient than traditional off-chain approaches, without requiring additional standardization layers.

## Reputation System

To ensure trust and reliability in the multi-agent ecosystem, we implement a reputation system that tracks and scores agent behavior. Each agent accumulates reputation points based on verifiable on-chain metrics such as transaction success rate and gas efficiency. The reputation score is stored on-chain and can be queried by other agents before initiating interactions. Agents with higher reputation scores are more likely to be selected for complex tasks and can command premium rates for their services. The system also includes mechanisms to penalize malicious behavior, such as failed transactions or attempts to exploit other agents. This creates a self-regulating ecosystem where agents are incentivized to maintain high-quality service and ethical behavior.

Measurable on-chain metrics include:
1. **Transaction Success Rate**: Success rate of transactions, measured in percentage
2. **Gas Efficiency**: Average gas used and standard deviation of gas usage across similar operations
3. **Value Transferred**: Total value handled without issues, measured in native token
4. **Contract Uptime**: Time since last successful interaction, measured in blocks
5. **Function Call Success Rate**: Success rate of specific function calls, tracked per function
6. **Interaction Frequency**: Number of successful interactions within a time window

## Example 1: Portfolio Rebalancing

Let's assume agent $A$ needs to periodically rebalance its portfolio. Instead of simply analysing historical data, the agent can use the registry to discover other agents that can help it with this task. For example, the following agent's registered services can be used to achieve the goal:

1. **Trend Analysis Agent**: identifies emerging trends in the market; analyzes technical indicators across multiple timeframes (e.g. `predictTrend(address asset, uint256 timeframe)`)
2. **Sentiment Analysis Agent**: analyzes market sentiment over social media, news and other sources to provide insights on potential market movements (e.g. `analyzeSentiment(address asset)`)
3. **Risk Assessment Agent**: assesses the portfolio risk exposure; analyzes asset correlations and volatility (e.g. `assessPortfolioRisk(address[] assets, uint256[] weights)`)
4. **Yield Optimization Agent**: identifies the most profitable yield opportunities across various DeFi protocols (e.g. `findYieldOpportunities(address[] assets)`)
The agent $A$ discovers the agents who's services can be used to achieve the goal and can compose a transaction to combine their services.
