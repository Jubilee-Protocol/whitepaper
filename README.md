# The Jubilee Protocol Whitepaper

## A Hybrid L2/L3 Architecture for Decentralized Asset Management and Permanent Provenance

---

## Abstract

The Jubilee Protocol is a hybrid Layer 2/Layer 3 architecture designed to unify Ethereum's programmability with Bitcoin's permanence. It operates as an EVM-compatible ZK-Rollup (L2) on Ethereum, enabling a high-performance environment for a suite of sophisticated, yield-generating financial products and decentralized applications. Its defining feature is a novel Layer 3 (L3) data provenance layer that periodically anchors cryptographic hashes of L2 state to the Bitcoin blockchain via OP_RETURN. This creates an immutable, permanent audit trail for critical data. By bridging native assets like ETH (jETH) and BTC (jBTC) and introducing automated index products (jBTCi, jETHs, jUSDi), Jubilee unlocks new forms of capital efficiency and provides a dual-security proposition previously unseen in the blockchain ecosystem. The protocol's index strategies deploy across multiple blockchain environments including zkSync and Base, maximizing accessibility and capital efficiency while maintaining security through careful cross-chain design considerations.

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Protocol Architecture](#2-protocol-architecture-a-three-layer-stack)
3. [Core Technical Components](#3-core-technical-components)
4. [Core Products](#4-core-products-the-jubilee-asset-suite)
5. [The Economic Engine](#5-the-economic-engine-value-accrual-and-distribution)
6. [Governance](#6-governance-the-jubilee-council)
7. [Security and Risk Factors](#7-security-and-risk-factors)
8. [Roadmap and Tokenomics](#8-roadmap-and-tokenomics)
9. [Conclusion](#9-conclusion)
10. [Disclaimer](#10-disclaimer)
11. [Definitions](#11-definitions)
12. [References](#12-references)

---

## 1. Introduction

### 1.1. The Great Divide: A Foundational Compromise

The decentralized web has evolved along two parallel, powerful, yet largely separate, tracks. Ethereum emerged as the undisputed leader for smart contract execution, fostering a vibrant ecosystem of decentralized applications (dApps), DeFi, and NFTs. Its strength lies in its Turing-complete EVM, enabling boundless innovation and complex financial primitives. Developers and users are drawn to its rich ecosystem, extensive tooling, and the promise of a globally accessible, programmable financial layer.

In contrast, Bitcoin has solidified its position as the world's most secure, decentralized, and immutable ledger. Its proof-of-work consensus, simple UTXO model, and robust design make it the ultimate store of value and the final arbiter of digital truth. Bitcoin's unparalleled security and censorship resistance are derived from its massive energy consumption and distributed mining network, making it incredibly difficult to alter its historical record.

This bifurcation has created inherent limitations and a foundational compromise. Developers and users are often forced into a trade-off: build on a highly programmable but singular security model (Ethereum), or anchor to an immutable but non-programmable one (Bitcoin). This results in siloed liquidity, where assets are difficult to deploy across ecosystems, and a fragmented security posture, where no single application can easily leverage the strengths of both networks. The capital efficiency of the broader crypto market is hampered by this separation, as significant value remains locked in one ecosystem, unable to participate fully in the other.

### 1.2. The Jubilee Solution: A Symbiotic Superstructure

The Jubilee Protocol is designed to bridge this divide, not by replacing either network, but by creating a symbiotic superstructure that harmonizes them. It offers a "best-of-both-worlds" solution by operating as a high-speed, low-cost, and programmable ZK-Rollup on Ethereum (L2) while simultaneously leveraging Bitcoin as its final settlement and data provenance layer (L3). This unique architecture allows Jubilee to provide the fast, low-cost, and programmable environment necessary for modern DeFi, while anchoring critical data to the most secure and immutable ledger ever created.

Jubilee's approach is to extend the capabilities of both Ethereum and Bitcoin, creating a unified financial ecosystem where assets can flow freely and security is maximized through a multi-layered approach. This symbiotic relationship aims to unlock new forms of capital efficiency, enhance overall system resilience, and provide a truly decentralized platform for the next generation of financial applications.

The development of the Jubilee Protocol is stewarded by the **Hundredfold Foundation**, a non-profit organization dedicated to building resilient, open, and equitable financial infrastructure. Our commitment is to the long-term success and progressive decentralization of the protocol, ensuring it remains a public good that serves its community.

---

## 2. Protocol Architecture: A Three-Layer Stack

Jubilee's core innovation is its hybrid, multi-layered architecture that ensures scalability, security, and permanence through a clear separation of concerns. This design leverages the strengths of each underlying blockchain, creating a robust and resilient system.

### 2.1. L1: The Security & Settlement Layer (Ethereum)

Ethereum serves as the foundational layer and the ultimate source of truth for the Jubilee Protocol. Its role is absolute and encompasses several critical functions, providing the bedrock of security and finality for the entire system. Jubilee inherits Ethereum's robust security guarantees, including its decentralized validator set, censorship resistance, and battle-tested smart contract environment.

**State Verification**: As a ZK-Rollup, Jubilee's state transitions are only considered valid after a cryptographic proof (a Zero-Knowledge Succinct Non-Interactive Argument of Knowledge, or ZK-SNARK; or a Zero-Knowledge Scalable Transparent Argument of Knowledge, or ZK-STARK) is submitted to and verified by a verifier smart contract deployed on Ethereum L1. This mathematical verification ensures the integrity and correctness of every transaction that occurs on the L2 without requiring L1 nodes to re-execute them. This off-chain computation and on-chain verification significantly reduce the computational load on Ethereum, enabling higher throughput on Jubilee.

**Data Availability**: To guarantee that the L2 state can always be reconstructed independently (a crucial property for censorship resistance and user fund safety), compressed transaction data from each L2 batch is posted as calldata to the Ethereum L1. This ensures that even if the L2's operators were to disappear or become malicious, the full state of Jubilee is fully recoverable from Ethereum, allowing users to exit their funds directly to L1 if necessary. This mechanism is fundamental to the security model of all ZK-Rollups.

**Asset Custody**: The canonical bridges for assets like ETH and various ERC-20 tokens are controlled by immutable smart contracts on Ethereum. The L1 contracts act as the secure escrow, locking assets on Ethereum before they are represented on Jubilee. This ensures that every bridged asset on Jubilee is fully backed 1:1 by its corresponding asset on Ethereum, maintaining the peg and providing trustless asset transfer between the layers.

### 2.2. L2: The Execution & Programmability Layer (Jubilee)

This is the active, high-performance environment where all user interactions, application logic, and the core financial primitives of the Jubilee Protocol reside. It is designed to provide a seamless and efficient user experience, leveraging the scalability benefits of ZK-Rollups.

**EVM Compatibility**: Built using the open-source ZK Stack, Jubilee is designed to be fully EVM-compatible at the opcode level. This allows developers to migrate existing Solidity smart contracts, deploy new dApps, and use familiar development tools (e.g., Hardhat, Foundry, Truffle) without modification. This frictionless development experience significantly lowers the barrier to entry for developers and fosters rapid innovation within the Jubilee ecosystem.

**High Throughput and Low Cost**: By processing transactions off-chain and only posting proofs and compressed data to Ethereum, Jubilee dramatically increases transaction throughput and reduces transaction costs compared to direct L1 interactions. This makes complex DeFi strategies and frequent trading economically viable for a broader range of users.

**Native Gas Token**: The native token for paying transaction fees (gas) on the L2 is jETH, a canonically bridged representation of Ethereum's ETH. This design choice creates a direct and continuous utility for ETH within the Jubilee ecosystem, aligning incentives between the L1 and L2 and ensuring that the economic activity on Jubilee contributes to the overall health of the Ethereum network.

### 2.3. L3: The Data Finality & Archival Layer (Bitcoin)

Bitcoin's role in the Jubilee architecture is specific, supplementary, and strictly for data permanence and immutable archival. It does not participate in the security or validation of the L2 state, which remains solely anchored to Ethereum. Instead, Bitcoin serves as an unparalleled append-only ledger for critical data.

**Mechanism**: An off-chain service, known as the L3 Settlement Service, periodically bundles cryptographic hashes (specifically, Merkle roots) of selected L2 state data, transaction batches, or other critical application-specific information. These Merkle roots are then embedded into a standard Bitcoin transaction via the OP_RETURN opcode. The OP_RETURN opcode allows for the inclusion of up to 80 bytes of arbitrary data in a Bitcoin transaction output, which is then pruned from the UTXO set, ensuring it does not bloat the active state of the Bitcoin network while remaining permanently recorded on its blockchain.

**Function**: This process creates a permanent, immutable, and globally verifiable timestamp and proof of existence for the embedded data. It leverages Bitcoin's immense proof-of-work security to provide an unparalleled level of data finality. By anchoring these hashes to the Bitcoin blockchain, Jubilee can prove, with the full force of Bitcoin's computational security, that a specific piece of data existed at a specific point in time (the Bitcoin block height). This functions as a "digital notary" service for applications requiring an exceptional level of data permanence, supplementing the primary security provided by Ethereum. This L3 layer is particularly valuable for auditing, regulatory compliance, and long-term data archival, where the absolute immutability of Bitcoin's ledger provides an additional layer of trust and verifiable history. 

For example, imagine a decentralized insurance protocol built on Jubilee that underwrites real-world climate risk. To pay out a claim, the protocol must prove that a specific event (e.g., a hurricane making landfall) occurred before a policy's expiration date. While Ethereum's history is robust, it is theoretically subject to deep reorganizations or future consensus changes. By anchoring the claim data hash to the Bitcoin blockchain, the protocol gains an indisputable, non-repudiable timestamp secured by the largest proof-of-work network in history. This level of finality is critical for high-value contracts and for building trust with off-chain institutions.

---

## 3. Core Technical Components

Jubilee Protocol is built upon a foundation of robust and battle-tested cryptographic and blockchain technologies. This section details the key technical components that enable the protocol's functionality, from its L2 execution environment to its multi-chain bridging mechanisms.

### 3.1. L2 ZK-Rollup Implementation

Jubilee leverages the ZK Stack, an open-source framework for building ZK-Rollups, to construct its L2 environment. This framework provides the necessary components for transaction processing, proof generation, and interaction with the Ethereum L1. The core of the ZK-Rollup involves two primary actors: the Sequencer and the Prover.

#### 3.1.1. The Sequencer: From Centralized to Decentralized

The Sequencer is a critical component responsible for collecting user transactions, ordering them into a sequence, constructing L2 blocks, and ultimately submitting batches of these transactions to the Ethereum L1.

**Initial Phase (Centralized)**: At launch, Jubilee Protocol will utilize a centralized Sequencer operated by the Hundredfold Foundation. This approach provides high throughput, predictable transaction ordering, and simplified maintenance during the early stages.

**Decentralization Path (Proof-of-Stake)**: The long-term vision includes a progressive transition to a decentralized Proof-of-Stake (PoS) sequencer set. Validators will be required to stake a significant amount of $JUBL tokens to participate. A leader selection algorithm will ensure fair rotation, and on-chain slashing conditions will penalize malicious behavior, ensuring honest operation.

#### 3.1.2. The Prover: Ensuring Computational Integrity

The Prover is responsible for generating the cryptographic validity proofs (ZK-SNARKs or ZK-STARKs) for each batch of L2 transactions, allowing the Ethereum L1 verifier contract to confirm the integrity of the L2 state without re-executing every transaction.

**Initial Phase (Permissioned)**: An initial permissioned Prover network will be operated by the Hundredfold Foundation to ensure timely proof generation and a smooth user experience.

**Decentralization Path (Permissionless & Competitive)**: The long-term goal is to transition to a permissionless, competitive prover market. In this model, any participant with sufficient computational resources can act as a Prover, incentivized by fees. This is expected to drive down proving costs and further decentralize the protocol.

### 3.2. The Interoperability Fabric: Bridge Architecture & Security

Interoperability is fundamental to Jubilee's mission. Secure and efficient bridging mechanisms are essential for the seamless transfer of assets between Ethereum, Jubilee, and Bitcoin.

#### 3.2.1. The jETH Bridge: Relayer Security

The jETH bridge facilitates the trust-minimized transfer of ETH and ERC-20 tokens between Ethereum L1 and Jubilee L2. It operates on a standard lock-and-mint mechanism, where assets are locked on the L1 and an equivalent amount is minted on the L2.

**Initial Phase (Centralized Relayer)**: At launch, the relayer service will be operated by the Hundredfold Foundation to ensure high availability and rapid response.

**Decentralization Path (PoS Validator Relayers)**: The relayer role will be progressively decentralized and integrated into the L2's Proof-of-Stake validator set. A validator chosen to propose a block will also be responsible for relaying pending bridge events.

#### 3.2.2. The jBTC Bridge: Trust-Minimized Bitcoin Bridging

To mitigate the risks associated with traditional wrapped Bitcoin, the jBTC bridge employs a sophisticated Threshold Signature Scheme (TSS) / Multi-Party Computation (MPC) model. This approach distributes trust across a network of independent participants, ensuring that no single entity can unilaterally control the underlying BTC.

**Decentralized Custody**: Through a Distributed Key Generation (DKG) ceremony, a Bitcoin private key is generated, but no single node ever possesses the full key. Instead, each node holds only a share. A transaction can only be signed if a predefined threshold (t) of n nodes collectively agree.

**Deposit & Mint**: A user sends native BTC to a TSS-controlled address. After sufficient confirmations, a supermajority of TSS nodes sign an attestation, which is submitted to a Jubilee L2 smart contract to mint the corresponding amount of jBTC.

**Network Composition**: The initial TSS Network will consist of a permissioned set of reputable, geographically distributed node operators and strategic partners vetted for reliability and technical competence.

**Economic Security**: The security of the jBTC bridge is economically enforced. Each TSS node operator will be required to stake a significant amount of $JUBL tokens. This stake acts as a security bond. If a supermajority of nodes collude to steal the underlying BTC or censor withdrawals, their staked $JUBL will be slashed. The value of the staked $JUBL will be programmatically maintained to be greater than the value of the BTC in the bridge, making collusion economically irrational and providing a strong financial disincentive against malicious behavior. 

To enforce this, the protocol incorporates several automated safeguards. A 'Collateralization Health Ratio' is constantly monitored on-chain. If this ratio of staked $JUBL value to bridged BTC value falls below a critical threshold (e.g., 150%), the bridge will automatically enter a 'deposits-only' mode, halting new jBTC mints until the ratio is restored. Furthermore, in the event of a sudden, severe price drop in the $JUBL token, an on-chain circuit breaker will temporarily pause all bridge operations (both minting and burning) to prevent opportunistic attacks and allow for governance intervention. This ensures the solvency and security of the bridge during extreme market volatility.

**Incentives**: TSS nodes are compensated for their services through a combination of fees generated by the jBTC bridge and a share of the protocol's overall revenue.

### 3.3. The L3 Settlement Service

The L3 Settlement Service is an off-chain component responsible for creating the permanent data anchor on the Bitcoin blockchain. Its primary function is to provide an additional, immutable layer of data provenance for critical L2 information.

**Data Aggregation & Merkle Tree Construction**: The service periodically collects and aggregates cryptographic hashes of designated L2 data, constructing a Merkle tree to create a single, compact hash (the Merkle root) that cryptographically summarizes all the included data.

**Bitcoin OP_RETURN Embedding**: The Merkle root is then embedded into a standard Bitcoin transaction using the OP_RETURN opcode, which allows for up to 80 bytes of arbitrary data.

**Immutable Timestamping**: By embedding the Merkle root into a Bitcoin transaction, the L3 Settlement Service creates an immutable, globally verifiable timestamp, proving with the full force of Bitcoin's proof-of-work that the specific L2 data existed at that exact time.

**Operational Model**: The L3 Settlement Service is designed as a decentralized and automated 'cron job' for the protocol. Initially, this service may be triggered by a permissioned set of keeper bots operated by the Hundredfold Foundation to ensure reliability. However, the long-term architecture is for this role to be integrated into the L2's Proof-of-Stake validator set. The validator responsible for proposing a new L2 block will also be tasked with constructing the Merkle root of designated L3 data and broadcasting the corresponding Bitcoin OP_RETURN transaction. Their successful inclusion of this L3 anchor can be verified on-chain, and they are rewarded with a portion of protocol fees for performing this duty. Failure to do so would result in a minor penalty, ensuring the task is consistently executed and fully decentralized.

---

## 4. Core Products: The Jubilee Asset Suite

Jubilee Protocol is not merely an infrastructure layer; it is a platform designed to host and optimize a suite of innovative, yield-generating financial products. These products are engineered to unlock new forms of capital efficiency, provide diversified exposure to core crypto assets, and generate sustainable yield through automated strategies. The core products are built as ERC-4626 compliant tokenized vaults, ensuring composability and ease of integration within the broader DeFi ecosystem.

### 4.1. Product Philosophy: Automated, Yield-Bearing Primitives

Our product philosophy centers on creating automated, yield-bearing primitives that abstract away complexity for the end-user while maximizing capital efficiency. By encapsulating sophisticated strategies within standardized ERC-4626 vaults, we enable composability, allowing other DeFi protocols to easily integrate and build upon Jubilee's offerings. This approach aims to make advanced yield generation accessible to a wider audience, from retail investors to institutional players.

### 4.2. jBTCi: The Jubilee Bitcoin Index

jBTCi (Jubilee Bitcoin Index) is a decentralized, yield-generating index fund designed to systematically capture and distribute value from the fragmented Bitcoin liquidity across the Ethereum ecosystem. It represents a diversified basket of leading Bitcoin representations on Ethereum, actively managed to exploit price inefficiencies and generate alpha for its holders.

**Thesis and Value Proposition**: The fundamental thesis behind jBTCi is that while all wrapped/bridged Bitcoin tokens on Ethereum are theoretically pegged 1:1 to native BTC, small but persistent price deviations exist. jBTCi is engineered to systematically identify and exploit these "peg-delta" opportunities, generating consistent arbitrage profits that accrue to jBTCi holders. It offers automated alpha generation, diversified Bitcoin exposure, and transforms a non-yield-bearing asset into a productive one.

**Portfolio Composition and Governance**: The jBTCi vault holds a dynamic basket of leading Bitcoin representations, governed by the Jubilee Council. The Council establishes a clear framework for including new assets based on criteria like bridge security, decentralization, liquidity, and audit history. The initial proposed basket includes wBTC, tBTC, rBTC, cbBTC, and the native jBTC, with target weights set and adjusted by Council governance.

### 4.3. jETHs: The Jubilee Ethereum Staked Index

jETHs (Jubilee Ethereum Staked Index) is a diversified index of yield-bearing, liquid-staked Ethereum (LST) tokens. It is designed to provide broad exposure to the Ethereum staking ecosystem while simultaneously generating additional alpha through systematic arbitrage strategies.

**Thesis and Dual Yield Source**: The value of jETHs grows from two sources: 1) the base staking yield from the underlying LSTs as they accrue consensus rewards, and 2) arbitrage alpha generated by the Rebalancing Engine from trading between LSTs when their prices deviate. This offers diversified staking exposure, automated yield optimization, and compounding returns.

**Portfolio Composition and Governance**: Similar to jBTCi, the jETHs composition is dynamic and managed by the Jubilee Council. The Council defines rigorous security and liquidity standards for including new LSTs. The initial proposed basket includes established LSTs like stETH, rETH, and cbETH, with target weights governed by the Council.

### 4.4. jUSDi: The Jubilee Stablecoin Index

jUSDi (Jubilee USD Index) is a yield-optimized stablecoin index designed to maintain stable value while generating returns through systematic rebalancing between leading USD-pegged stablecoins. It represents a diversified basket of established stablecoins, actively managed to exploit small price inefficiencies and provide superior capital stability.

**Thesis and Value Proposition**: While stablecoins are designed to maintain a 1:1 peg to the US Dollar, market dynamics create temporary deviations from this peg. jUSDi systematically captures value from these micro-arbitrage opportunities while maintaining the stability characteristics users expect from dollar-denominated assets. The product offers stable value preservation, automated yield generation from peg arbitrage, diversified stablecoin exposure reducing single-issuer risk, and a composable primitive for DeFi applications requiring stable collateral.

**Portfolio Composition and Governance**: The jUSDi vault holds a dynamic basket of leading stablecoins, governed by the Jubilee Council. The Council establishes strict criteria for inclusion based on regulatory compliance, reserve transparency, redemption reliability, market liquidity, and issuer reputation. The initial proposed basket includes USDC and DAI, with target weights set and adjusted by Council governance. Additional stablecoins may be added as they meet the Council's rigorous standards.

**Multi-Chain Strategy**: jUSDi, along with jBTCi and jETHs, is designed as a multi-chain product suite. While the core protocol infrastructure operates on the Jubilee L2 (built on zkSync), these index strategies will be deployed across multiple blockchain ecosystems to maximize accessibility and capture arbitrage opportunities where they exist. Initial deployments are planned for:
- **Jubilee L2 (zkSync Era)**: The native home for all index products with full protocol integration
- **Base**: Leveraging Coinbase's ecosystem and deep stablecoin liquidity
- **Additional EVM chains**: To be determined by the Council based on liquidity depth and strategic fit

Each deployment operates independently with its own liquidity pools and rebalancing mechanisms optimized for the specific chain's characteristics. Future protocol developments may enable carefully designed cross-chain bridging of index tokens, allowing users to move their positions between chains. However, such bridging functionality will only be implemented with extensive security review, as cross-chain bridges represent significant attack vectors. The Council will approach any bridging implementation with extreme caution, prioritizing security over convenience.

### 4.5. The Rebalancing Engine & Oracle Security Model

The Rebalancing Engine is the core intelligence behind the jBTCi and jETHs index products. It is a sophisticated, automated system designed to identify and execute profitable arbitrage opportunities within the specified asset baskets.

**Off-Chain Analysis & On-Chain Execution**: An off-chain component continuously monitors markets to identify arbitrage opportunities. Once found, it initiates an on-chain transaction. To prevent front-running and ensure profitability, the engine employs MEV protection strategies like private mempool submission and includes an atomic on-chain check that reverts the transaction if it is not profitable after all costs.

**Oracle Security Model**: The integrity of the index products depends on secure price data. The engine incorporates a multi-layered oracle security model using Chainlink Price Feeds as the primary source, supplemented by built-in circuit breakers that pause activity if price data exceeds a predefined "sanity bound" (e.g., >10% deviation in a single block). For large trades, it also cross-references the spot price with an on-chain Time-Weighted Average Price (TWAP) to prevent spot price manipulation.

#### 4.5.1. Long-Term Strategy: Beyond Arbitrage

While the Rebalancing Engine is designed to capture arbitrage profits from peg deviations, the protocol recognizes that these opportunities may diminish as markets become more efficient. Therefore, the engine's primary long-term value proposition is not just profit generation, but sophisticated index health and risk management.

Its core function will evolve into a liquidity balancing tool. By systematically selling the over-weighted asset and buying the under-weighted one, the engine actively helps maintain the peg of all constituent assets within the index. This creates a healthier, more stable ecosystem for all wrapped/staked tokens on Jubilee. In this mature state, its value is twofold:

1. **Risk Mitigation**: It acts as an automated portfolio manager, reducing the index's exposure to any single asset that may be de-pegging or experiencing issues.
2. **Public Good**: It provides a constant source of stabilizing liquidity, benefiting the entire Jubilee ecosystem.

Arbitrage profits will then be seen as a valuable secondary benefit derived from the primary function of maintaining index health, ensuring the sustainability of the products even in highly efficient markets.

### 4.6. Mathematical Framework & Fee Structure

**Mathematical Framework for Index Products**: The Net Asset Value per share (NAV) of an index token reflects the total value of the underlying assets plus accumulated arbitrage profits, divided by the total supply of the index token. As the Rebalancing Engine generates profits, they are compounded back into the vault, increasing the NAV.

**Fee Structure**: Jubilee is designed as a sustainable, revenue-generating ecosystem. All fees are controlled by Council governance. The structure includes a small annual Management Fee on AUM, a Performance Fee on gross arbitrage profits, trading fees on the protocol's DEX, and small fees for bridging operations.

### 4.7. Minting and Redemption Mechanics

As ERC-4626 compliant vaults, the minting and redemption processes for jBTCi, jETHs, and jUSDi are standardized and intuitive. Users can mint new index tokens by depositing an approved underlying asset into the respective vault. The vault contract calculates the current NAV and mints a proportional amount of the index token. Conversely, users can redeem their index tokens for a proportional amount of the underlying assets held in the vault. Small fees may be applied to minting and redemption to prevent oracle front-running and contribute to the protocol treasury.

---

## 5. The Economic Engine: Value Accrual and Distribution

The Jubilee Protocol is designed with a robust economic engine that ensures sustainable value accrual for the protocol and its participants. This engine is powered by a capital-efficient decentralized exchange, a well-defined revenue model, and a novel tokenomics structure that aligns incentives and distributes value back to the community.

### 5.1. The Jubilee Exchange: AMM Design & Liquidity Strategy

The Jubilee Exchange (or Jubilee Ex for short), fully named the Jubilee Exchange for Swaps and Unified Settlement, is the central liquidity hub of the Jubilee Protocol. It is an automated market maker (AMM) designed for capital efficiency, low slippage, and deep liquidity across a wide range of assets, particularly those central to the Jubilee ecosystem (e.g., jETH, jBTC, jBTCi, jETHs, and $JUBL).

**Hybrid Liquidity Model**: The Jubilee Exchange employs a hybrid liquidity model, combining the strengths of different AMM designs:

- **Concentrated Liquidity Pools**: For volatile asset pairs (e.g., jETH/$JUBL), the exchange utilizes a concentrated liquidity model, similar to Uniswap V3. This allows liquidity providers (LPs) to allocate their capital within specific price ranges, significantly increasing capital efficiency and enabling deeper liquidity around the current market price.

- **Stable Pools**: For like-kind asset pairs (e.g., jBTC and other wrapped BTC variants; or jETH and various LSTs), the exchange employs a stable swap invariant, similar to Curve Finance. This design is optimized for very low slippage on trades between assets that are expected to maintain a close peg, making it ideal for the arbitrage operations of the Rebalancing Engine.

**Liquidity Strategy**: Bootstrapping and maintaining deep liquidity on the Jubilee Exchange is critical for the protocol's success. A significant portion of the "Community & Ecosystem" token allocation will be dedicated to this.

1. **Liquidity Mining**: In the initial phases, liquidity providers for key pairs will be rewarded with $JUBL emissions to attract early LPs and establish robust liquidity pools.

2. **Protocol-Owned Liquidity (POL)**: The Jubilee Council will strategically use funds from the protocol treasury to create its own liquidity positions on the Jubilee Exchange. This Protocol-Owned Liquidity ensures a permanent base level of liquidity for critical pairs, reducing reliance on external LPs and allowing the protocol to directly earn trading fees.

### 5.2. The $JUBL Token: Governance and Utility

The $JUBL token is the native utility and governance asset of the Jubilee Protocol. It is designed to be integral to the protocol's security, decentralization, and economic sustainability.

- **Governance**: $JUBL holders are granted voting rights within the Jubilee Council (when held by verified member organizations), allowing them to participate in critical decisions.

- **Staking**: $JUBL can be staked to participate in the protocol's security mechanisms, such as securing the decentralized sequencer set and the TSS Network for the jBTC bridge. Stakers are rewarded with a share of protocol revenue and $JUBL emissions.

- **Fee Discounts**: $JUBL may be used to pay for protocol fees (e.g., trading fees on the Jubilee Exchange, bridge fees) at a discounted rate.

- **Access to Features**: Future protocol features or premium services may require holding or staking $JUBL.

### 5.3. $JUBL Staking and "Choice Yield": The Economic Flywheel

Jubilee introduces "Choice Yield," a novel staking mechanism designed to provide $JUBL stakers with tangible, high-quality yield directly from protocol revenue. This mechanism creates a powerful economic flywheel that aligns the interests of $JUBL holders with the overall success and revenue generation of the Jubilee Protocol.

**Revenue Collection**: All protocol revenue streams (Jubilee Exchange trading fees, Index Fund management/performance fees, and Bridge fees) are collected in their native asset forms (primarily jETH and jBTC) and directed to a dedicated FeeCollector.sol smart contract.

---

## 6. Governance: The Jubilee Council

The Jubilee Protocol is governed by the Jubilee Council, an innovative governance body that operates similarly to a decentralized autonomous organization (DAO) but with a mission-aligned membership structure. Like traditional DAOs, the Council makes decisions through on-chain voting, maintains transparent proposal processes, and manages protocol parameters autonomously. However, rather than token-weighted voting by anonymous holders, the Council is composed of verified organizations with long-term stewardship commitments.

### 6.1. Principles of Stewardship

The Jubilee Council is founded on the principle of long-term stewardship over the protocol as a vital public good for a specific community, with a multi-generational vision. Governance prioritizes the sustained health, security, and ethical development of the protocol in alignment with Christian principles of service, integrity, and community welfare. The governance culture will emphasize:

- **Transparency**: All proposals, discussions, and voting records will be publicly accessible on-chain and through dedicated forums.

- **Accountability**: Governors are accountable to the community for their decisions.

- **Mission-Alignment**: The long-term goal is to foster participation from a diverse set of organizations that are aligned with the protocol's core mission.

- **Resilience**: Governance mechanisms are designed to be robust against various attack vectors, including economic and social exploits.

### 6.2. Council Composition: A United Group

The Jubilee Council, the primary governing body for key protocol parameters and upgrades, is composed of verified, Bible-believing Christian churches and mission-aligned non-profit organizations.

**Rationale**: This model is chosen to create a stable, values-driven governance layer. These institutions possess long-term operational horizons, established community trust, and an inherent alignment with the protocol's mission that transcends market cycles. Their participation is intended as an act of stewardship, not speculation, creating a bulwark against hostile takeovers or short-sighted, profit-driven decisions that could harm the protocol's long-term health.

**Verification Process**: The Hundredfold Foundation will manage a robust 'Know Your Organization' (KYO) process to verify the legal identity, non-profit status, doctrinal alignment, and operational history of each applicant. This process is critical to ensuring the integrity of the Council and its adherence to the protocol's foundational mission.

**Staking Requirement & Security**: Each verified organization will be required to stake a significant amount of $JUBL tokens to activate and maintain its voting power. This staking requirement serves multiple purposes:

- **Economic Alignment**: It creates a direct financial commitment to the protocol.

- **Attack Deterrent**: An attack on the governance system would require an actor to not only corrupt a supermajority of disparate, real-world organizations but also to acquire and stake a massive amount of $JUBL tokens, making such an attack prohibitively expensive and logistically improbable as Jubilee Protocol grows.

- **Reputational Stake**: For established organizations, the reputational damage associated with participating in a malicious governance action provides a strong non-financial disincentive against collusion.

### 6.3. The Hundredfold Grant Program: Empowering the Ecosystem

While the Jubilee Council holds formal governance power over core protocol functions, the broader community of $JUBL token holders plays a vital and distinct role in directing the protocol's real-world impact through grant-making.

**Proposal & Nomination**: On a quarterly basis starting 1 year after mainnet, any $JUBL holder can nominate organizations or projects that they believe align with Christian morals and values for consideration in the Hundredfold Grant Program. These nominations are discussed and voted on by the community of token holders in a public forum.

**Final Approval & Funding**: The top-voted nominees from the community vote are then presented to the Hundredfold Foundation (and, in the future, the Jubilee Council) for a final review and approval. This final check ensures alignment with the core mission. Winners receive grants funded by a designated portion of the protocol's treasury revenue, creating a direct link between the protocol's economic success and its ability to support mission-aligned work in the real world.

### 6.4. Scope of Governance & Legal Wrapper

The Jubilee Council will have comprehensive authority over all key aspects of the protocol, ensuring that its evolution is guided by its governors.

- **Protocol Parameters**: The Council will control critical protocol parameters, including fees, risk parameters, and reward rates.

- **Treasury Management**: The Council will manage the protocol treasury, allocating funds for grants, core development, security audits, and Protocol-Owned Liquidity (POL).

- **Smart Contract Upgrades**: All major smart contract upgrades will require Council approval, executed via a timelock contract to provide a grace period for users to react to changes.

- **Index Management**: The Council will be responsible for the strategic direction of the jBTCi, jETHs, and jUSDi index products, including setting target weights and approving new assets for inclusion.

**Legal Wrapper**: To facilitate interactions with the traditional legal and financial systems, the Jubilee Council will be wrapped in a legal entity based in the US. The Hundredfold Foundation will serve as the offshore entity, holding intellectual property and managing global operations, ensuring a robust and compliant multi-jurisdictional legal structure. Lastly, Hundredfold will have an additional entity based in the US for launching, growing, and scaling Jubilee Protocol before transitioning all technology into the hands of the Jubilee Council. The Hundredfold entity based in the US will manage all technology aspects of the Jubilee Protocol for the Jubilee Council for the foreseeable future.

---

## 7. Security and Risk Factors

Security is paramount for any decentralized protocol, especially one dealing with significant financial value and bridging across multiple blockchains. The Jubilee Protocol employs a multi-layered security approach, combining cryptographic assurances, economic incentives, and robust operational practices. However, like all complex systems, it is not without inherent risks. This section outlines the security measures in place and discusses potential risk factors.

### 7.1. A Multi-Layered Security Model

Jubilee Protocol's security is derived from a defense-in-depth strategy, leveraging the strengths of its underlying layers and implementing additional safeguards at the application level.

- **L1 Security (Ethereum)**: The ultimate security and finality of the Jubilee L2 are inherited directly from Ethereum. All L2 state transitions are cryptographically proven via ZK-SNARKs/STARKs and verified by smart contracts on Ethereum L1. Furthermore, all L2 transaction data is posted to Ethereum L1 as calldata, ensuring data availability and allowing users to force withdrawals directly to L1.

- **L3 Permanence (Bitcoin)**: While not directly contributing to the L2's real-time security, the L3 Bitcoin layer provides an unparalleled level of data permanence. By anchoring cryptographic hashes of critical L2 state data to the Bitcoin blockchain, Jubilee creates an immutable, censorship-resistant audit trail for dispute resolution and regulatory compliance.

- **Economic Security (Staking & Slashing)**: The decentralization of the Sequencer and the jBTC bridge's TSS Network is economically secured by $JUBL staking. Validators and TSS node operators are required to lock up significant amounts of $JUBL as collateral, which is subject to slashing if they engage in malicious behavior. The economic value of the staked $JUBL is designed to always exceed the potential gain from an attack, making such actions economically irrational.

- **Smart Contract Security**: All smart contracts will undergo rigorous security assessments, including:
  - Internal Code Reviews: Continuous review by the core development team.
  - External Audits: Engagement with multiple, independent, top-tier blockchain security firms.
  - Formal Verification: For the most critical components, Jubilee will implement formal verification to mathematically prove the correctness of the code.
  - Bug Bounties: A continuous and well-funded bug bounty program will be launched to incentivize hackers and security researchers to identify and responsibly disclose vulnerabilities.

- **Oracle Security**: As detailed in Section 4.4, the protocol incorporates a multi-layered oracle security model, relying on Chainlink Price Feeds with built-in circuit breakers and TWAP checks to mitigate risks associated with data manipulation or oracle failure.

### 7.2. Key Risk Considerations

Despite robust security measures, all blockchain protocols carry inherent risks. Participants should be aware of the following:

- **Smart Contract Risk**: While audited and formally verified, smart contracts are complex and can contain unforeseen bugs or vulnerabilities. An exploit in a critical contract could lead to loss of funds. Users should understand that interacting with smart contracts always carries a degree of risk.

- **Technology Risk**: The underlying technologies (ZK-Rollups, TSS/MPC, blockchain interoperability) are cutting-edge and evolving. Unforeseen technical issues or undiscovered flaws in these foundational technologies could impact the protocol's stability or security.

- **Market Risk**: The value of assets held within the Jubilee Protocol, including jBTCi, jETHs, and $JUBL, is subject to significant market volatility. The performance of index products is dependent on the existence of arbitrage opportunities, which may diminish over time.

- **Centralization Risk (Early Phase)**: In its initial phases, Jubilee Protocol will operate with a centralized sequencer, permissioned provers, centralized relayers, and a permissioned L3 Settlement Service operator. While necessary for bootstrapping, this introduces temporary centralization risks. A failure to successfully execute the decentralization roadmap could expose the protocol to censorship, single points of failure, or reduced resilience.

- **Bridge Risk**: While designed for trust-minimization, bridges are complex and remain a common target for exploits. Risks include vulnerabilities in bridge contracts, collusion among TSS operators (though economically disincentivized), or operational failures.

- **Regulatory Risk**: The legal and regulatory landscape for digital assets and decentralized finance is uncertain and varies significantly across jurisdictions. New regulations could adversely impact the Jubilee Protocol's operations, its token, or the ability of users to participate.

- **Governance Risk**: The protocol's unconventional governance model, while mission-aligned, is experimental and carries unique risks. It may face challenges in scaling the verification process globally, ensuring the Council has access to adequate technical expertise to make informed decisions, and defending against social attacks or attempts to co-opt member organizations. The protocol's long-term success is tied to the successful implementation and integrity of this novel stewardship model.

- **Liquidity Risk**: Insufficient liquidity on the Jubilee Exchange or for the $JUBL token could lead to high slippage for traders or difficulty for holders to exit positions.

---

## 8. Roadmap and Tokenomics

### 8.1. The Jubilee Rollout: A Phased Deployment

The development and deployment of the Jubilee Protocol will follow a phased approach, metaphorically structured around the four phases: Yoke, Harvest, Wisdom, Heritage. This phased rollout allows for iterative development, rigorous testing, and progressive decentralization, ensuring stability and security at each stage. The timeline is intentionally framed over a two-year window to prioritize moving correctly over moving fast, providing ample flexibility for research, development, and security audits.

#### Phase 1: "Yoke" — Foundation & Community Cultivation (H2 2025 - H1 2026)

**Objective**: Establish the core technical infrastructure and cultivate the foundational community.

**Key Deliverables**:
- Completion of core L2 ZK-Rollup smart contracts (Sequencer, Prover interfaces, Bridge contracts).
- Internal audit of core smart contracts.
- Launch of private testnet for internal testing and early partner integration.
- Development of initial documentation and developer tooling.
- Establishment of core community channels and initial community building efforts.
- Formalization of the Hundredfold Foundation and US-based Hundredfold legal entities.

#### Phase 2: "Harvest" — Mainnet Launch & Token Generation (H2 2026)

**Objective**: Launch the Jubilee L2 Mainnet and introduce the $JUBL token to bootstrap network effects and liquidity.

**Key Deliverables**:
- Deployment of Jubilee L2 Mainnet.
- Token Generation Event (TGE) for the $JUBL token.
- Listing of $JUBL on initial decentralized exchanges (DEXs) to establish liquidity.
- Launch of $JUBL staking mechanism.
- Initial liquidity mining programs on the Jubilee Exchange for core pairs.
- Completion of initial external security audit of core L2 contracts and jETH bridge.

#### Phase 3: "Wisdom" — The Asset Suite & Real Yield Activation (H1 2027)

**Objective**: Deploy the core yield-generating index products and activate the "Choice Yield" mechanism.

**Key Deliverables**:
- Deployment of jBTCi (Jubilee Bitcoin Index), jETHs (Jubilee Ethereum Staked Index), and jUSDi (Jubilee USD Index) ERC-4626 vaults.
- Activation of the Rebalancing Engine for all index products.
- Multi-chain deployment of index strategies on Base and other compatible chains.
- Full activation of the "Choice Yield" mechanism for $JUBL stakers, distributing protocol revenue in jBTC and jETH.
- Integration of Chainlink Oracles for index products.
- Second external security audit focusing on index products and Rebalancing Engine.

#### Phase 4: "Heritage" — Permanent Provenance & Decentralization (H2 2027+)

**Objective**: Activate the L3 Bitcoin settlement layer and transition to full community ownership and decentralized operation.

**Key Deliverables**:
- Activation of the L3 Settlement Service, periodically anchoring L2 data hashes to the Bitcoin blockchain via OP_RETURN.
- Progressive decentralization of the Sequencer to a PoS validator set.
- Progressive decentralization of the Prover network to a permissionless, competitive market.
- Transition of the jBTC bridge TSS Network to a fully decentralized, economically secured set of operators.
- Launch of the Jubilee Council governance framework, enabling on-chain voting by verified organizations.
- Establishment of the Ecosystem Grants Program, inviting developers to build on Jubilee.
- Ongoing research and development into advanced ZK technologies and cross-chain interoperability.

### 8.2. $JUBL Tokenomics and Emissions

The $JUBL token is designed to be the economic backbone of the Jubilee Protocol, aligning incentives across all participants and ensuring the long-term sustainability and decentralization of the network. The total supply is capped, and emissions are carefully managed to bootstrap network effects while transitioning to a model primarily driven by protocol revenue.

**Total Supply (Max)**: 1,000,000,000 $JUBL

**Emission Schedule**: The 25% of supply allocated to staking rewards will be distributed on a logarithmic decay schedule. The emission rate per block will halve each year for the first 4-5 years. This schedule is designed to:
- **Bootstrap Security**: Provide strong incentives for early stakers to secure the network when protocol revenue is still nascent.
- **Transition to Real Yield**: Gradually reduce reliance on inflationary emissions as protocol revenue from fees grows, ensuring that $JUBL staking yield primarily derives from real economic activity in the long term.
- **Predictability**: Offer a predictable emission schedule, allowing participants to forecast future supply and rewards.

#### Token Allocation

| Category | Percentage | Tokens | Vesting Schedule | Rationale |
|----------|-----------|--------|------------------|-----------|
| Community & Ecosystem | 40% | 400,000,000 | 4-5 years (linear unlock, often tied to liquidity mining and grants) | Designed to bootstrap liquidity, incentivize early adopters, fund ecosystem grants, and support community initiatives for network growth. |
| Staking Rewards | 25% | 250,000,000 | 5+ years (logarithmic decay, as described above) | Incentivizes $JUBL staking for network security (sequencers, TSS nodes) and governance participation. |
| Foundation & Core Team | 20% | 200,000,000 | 1-year cliff, 3-year linear unlock | Compensates the founding team and core contributors for their long-term commitment. The vesting aligns their incentives with the protocol. |
| Investors (Private) | 10% | 100,000,000 | 1-year cliff, 2-year linear unlock | Provides capital for initial development and audits. Vesting ensures investors are aligned with long-term value creation. |
| Public Sale / Liquidity | 5% | 50,000,000 | 100% Unlocked at TGE | Facilitates initial public distribution and provides immediate liquidity for the $JUBL token on exchanges. |

---

## 9. Conclusion

The Jubilee Protocol represents a fundamental step forward in the evolution of decentralized infrastructure. By refusing to accept the inherent trade-offs of a fragmented Web3 landscape, we have designed a system that is both highly performant and permanently secure. The integration of an Ethereum-based ZK-Rollup (L2) with a Bitcoin-based Provenance Layer (L3) creates a novel architectural primitive, unlocking unprecedented levels of scalability, data immutability, and cross-chain interoperability.

Through its core products—the jBTCi, jETHs, and jUSDi automated, yield-generating index funds—Jubilee unlocks new forms of capital efficiency for Bitcoin, Ethereum, and stablecoin assets. The introduction of "Choice Yield" establishes a powerful economic flywheel, aligning incentives and distributing real protocol revenue to $JUBL stakers. The multi-layered security model, progressive decentralization roadmap, and robust governance framework underscore our commitment to building a resilient and sustainable ecosystem.

Jubilee is more than just a protocol; it is a vision for a unified, secure, and capital-efficient decentralized future. We invite developers, users, and stakeholders to join us in building this symbiotic superstructure, bridging the great divide, and ushering in a new era of blockchain innovation.

---

## 10. Disclaimer

This whitepaper is for informational purposes only and does not constitute an offer to sell or a solicitation of an offer to buy any securities or tokens. It is not intended to provide legal, financial, or investment advice. The information contained herein may not be exhaustive and does not imply any elements of a contractual relationship. Please consult with a qualified professional before making any investment decisions.

The Jubilee Protocol is under development, and its features, design, and implementation are subject to change without notice. There are inherent risks associated with blockchain technology, cryptocurrencies, and decentralized finance, including but not limited to loss of funds, smart contract vulnerabilities, market volatility, and regulatory uncertainty. Participants should conduct their own due diligence and understand these risks before engaging with the protocol.

---

## 11. Definitions

- **AMM (Automated Market Maker)**: A type of decentralized exchange protocol that relies on mathematical formulas to price assets.

- **Arbitrage**: The simultaneous buying and selling of an asset in different markets to profit from price differences.

- **calldata**: A special read-only, non-modifiable area in Ethereum transactions used to pass arguments to a contract function.

- **DAO (Decentralized Autonomous Organization)**: An organization represented by rules encoded as a computer program, transparent, controlled by the organization's members, and not influenced by a central government.

- **DeFi (Decentralized Finance)**: An umbrella term for financial applications enabled by blockchain technology, typically without intermediaries.

- **DKG (Distributed Key Generation)**: A cryptographic process where multiple parties jointly compute a shared secret key, but no single party ever knows the entire key.

- **ERC-20**: A technical standard used for all smart contracts on the Ethereum blockchain for fungible tokens.

- **ERC-4626**: A tokenized vault standard designed to optimize and standardize the yields of interest-bearing tokens.

- **EVM (Ethereum Virtual Machine)**: The runtime environment for smart contracts in Ethereum.

- **jBTC**: Bridged Bitcoin on the Jubilee L2.

- **jBTCi**: The Jubilee Bitcoin Index, a yield-generating index fund.

- **jETH**: Bridged Ethereum on the Jubilee L2, also used as the native gas token.

- **jETHs**: The Jubilee Ethereum Staked Index, a diversified index of liquid-staked Ethereum tokens.

- **jUSDi**: The Jubilee USD Index, a yield-optimized stablecoin index.

- **L1 (Layer 1)**: The base blockchain (e.g., Ethereum, Bitcoin).

- **L2 (Layer 2)**: A scaling solution built on top of an L1 blockchain (e.g., ZK-Rollups).

- **L3 (Layer 3)**: An additional layer built on top of an L2, often for specific functionalities like data provenance.

- **LST (Liquid Staking Token)**: A token representing staked ETH, allowing users to retain liquidity while earning staking rewards.

- **MEV (Maximal Extractable Value)**: The maximum value that can be extracted from block production in excess of the standard block reward and gas fees by including, excluding, or reordering transactions within a block.

- **Merkle Root**: The top hash in a Merkle tree, which summarizes all the transactions or data in the tree.

- **MPC (Multi-Party Computation)**: A cryptographic protocol that allows multiple parties to jointly compute a function over their inputs while keeping those inputs private.

- **NFT (Non-Fungible Token)**: A unique and non-interchangeable unit of data stored on a digital ledger.

- **OP_RETURN**: A Bitcoin script opcode that allows for the inclusion of up to 80 bytes of arbitrary data in a transaction output.

- **PoS (Proof-of-Stake)**: A consensus mechanism where validators are chosen to create new blocks based on the amount of cryptocurrency they hold and are willing to "stake" as collateral.

- **PoW (Proof-of-Work)**: A consensus mechanism where participants (miners) solve complex computational puzzles to validate transactions and create new blocks.

- **Sequencer**: A component in a ZK-Rollup responsible for ordering transactions and submitting them to the L1.

- **TGE (Token Generation Event)**: The initial distribution of a new cryptocurrency token.

- **TSS (Threshold Signature Scheme)**: A cryptographic scheme where a signature can only be generated if a threshold number of participants cooperate.

- **TWAP (Time-Weighted Average Price)**: The average price of an asset over a specified time period.

- **UTXO (Unspent Transaction Output)**: The amount of cryptocurrency remaining after a transaction, which can be used as input for new transactions.

- **ZK-Rollup**: A Layer 2 scaling solution that bundles (rolls up) hundreds of transactions off-chain and generates a cryptographic proof (ZK-SNARK/STARK) of their validity, which is then posted to the L1.

- **ZK-SNARK (Zero-Knowledge Succinct Non-Interactive Argument of Knowledge)**: A type of zero-knowledge proof that allows one party to prove possession of certain information to another party without revealing the information itself.

- **ZK-STARK (Zero-Knowledge Scalable Transparent Argument of Knowledge)**: A type of zero-knowledge proof similar to ZK-SNARKs but designed for greater scalability and transparency.

---

## 12. References

1. Nakamoto, S. (2008). *Bitcoin: A Peer-to-Peer Electronic Cash System*. Available at: https://bitcoin.org/bitcoin.pdf

2. Buterin, V. (2013). *Ethereum Whitepaper: A Next-Generation Smart Contract and Decentralized Application Platform*. https://ethereum.org/en/whitepaper/

3. zkSync. (2023). *ZK Stack*. A framework for building custom ZK-Rollups. https://zksync.io/stack

4. *OpenTimestamps*. Leveraging the Bitcoin Blockchain for Timestamping. A project demonstrating the use of Bitcoin's OP_RETURN for data anchoring. https://opentimestamps.org/

5. *Chainlink*. Chainlink 2.0: Next Steps in the Evolution of Decentralized Oracle Networks. A whitepaper detailing the architecture of decentralized oracle networks for hybrid smart contracts. https://chain.link/whitepaper

6. *EIP-4626: Tokenized Vaults*. An Ethereum Improvement Proposal standardizing yield-bearing vaults. https://eips.ethereum.org/EIPS/eip-4626

7. Adams, H., Zinsmeister, N., Salem, M., Keefer, R., & Robinson, D. (2021). *Uniswap v3 Core*. A whitepaper detailing the concepts of concentrated liquidity. https://uniswap.org/whitepaper-v3.pdf

8. Egorov, M. (2019). *StableSwap - Efficiently Swapping Stablecoins