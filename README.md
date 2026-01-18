# The Jubilee Protocol Whitepaper (v2)

## A Hybrid L2/L3 Architecture for Decentralized Asset Management and Permanent Provenance

---

### Abstract
The Jubilee Protocol is a hybrid Layer 2/Layer 3 architecture designed to unify Ethereum's programmability with Bitcoin's permanence. It operates as an EVM-compatible ZK-Rollup (L2) on Ethereum, enabling a high-performance environment for a suite of sophisticated, yield-generating financial products and decentralized applications. Its defining feature is a novel Layer 3 (L3) data provenance layer that periodically anchors cryptographic hashes of L2 state to the Bitcoin blockchain via OP_RETURN. This creates an immutable, permanent audit trail for critical data.

The protocol's core products—jBTCi (Bitcoin Index), jETHs (Staked Ethereum Index), and jUSDi (Stablecoin Index)—are automated, yield-generating vaults that capture arbitrage opportunities from market inefficiencies. By bridging native assets like ETH (jETH) and BTC (jBTC), Jubilee unlocks new forms of capital efficiency and provides a dual-security proposition previously unseen in the blockchain ecosystem.

The protocol's index strategies deploy across multiple blockchain environments including the native Jubilee L2 (built on zkSync Era), Base, and other compatible EVM chains, maximizing accessibility and capital efficiency while maintaining security through careful cross-chain design considerations. The $JUBL governance token serves as the economic backbone, providing lending credits for Jubilee Lending (launching Good Friday 2026), revenue sharing through the Choice Yield mechanism, and governance rights within the mission-aligned Jubilee Council.

### Table of Contents
1. Introduction
2. Protocol Architecture
3. Core Technical Components
4. Core Products
5. The Economic Engine
6. Governance
7. Security and Risk Factors
8. Roadmap and Tokenomics
9. Conclusion
10. Disclaimer
11. Definitions
12. References

### 1. Introduction

#### 1.1. The Great Divide: A Foundational Compromise
The decentralized web has evolved along two parallel, powerful, yet largely separate, tracks. Ethereum emerged as the undisputed leader for smart contract execution, fostering a vibrant ecosystem of decentralized applications (dApps), DeFi, and NFTs. Its strength lies in its Turing-complete EVM, enabling boundless innovation and complex financial primitives. Developers and users are drawn to its rich ecosystem, extensive tooling, and the promise of a globally accessible, programmable financial layer.

In contrast, Bitcoin has solidified its position as the world's most secure, decentralized, and immutable ledger. Its proof-of-work consensus, simple UTXO model, and robust design make it the ultimate store of value and the final arbiter of digital truth. Bitcoin's unparalleled security and censorship resistance are derived from its massive energy consumption and distributed mining network, making it incredibly difficult to alter its historical record.

This bifurcation has created inherent limitations and a foundational compromise. Developers and users are often forced into a trade-off: build on a highly programmable but singular security model (Ethereum), or anchor to an immutable but non-programmable one (Bitcoin). This results in siloed liquidity, where assets are difficult to deploy across ecosystems, and a fragmented security posture, where no single application can easily leverage the strengths of both networks. The capital efficiency of the broader crypto market is hampered by this separation, as significant value remains locked in one ecosystem, unable to participate fully in the other.

#### 1.2. The Jubilee Solution: A Symbiotic Superstructure
The Jubilee Protocol is designed to bridge this divide, not by replacing either network, but by creating a symbiotic superstructure that harmonizes them. It offers a "best-of-both-worlds" solution by operating as a high-speed, low-cost, and programmable ZK-Rollup on Ethereum (L2) while simultaneously leveraging Bitcoin as its final settlement and data provenance layer (L3). This unique architecture allows Jubilee to provide the fast, low-cost, and programmable environment necessary for modern DeFi, while anchoring critical data to the most secure and immutable ledger ever created.
Jubilee's approach is to extend the capabilities of both Ethereum and Bitcoin, creating a unified financial ecosystem where assets can flow freely and security is maximized through a multi-layered approach. This symbiotic relationship aims to unlock new forms of capital efficiency, enhance overall system resilience, and provide a truly decentralized platform for the next generation of financial applications.

The development of the Jubilee Protocol is stewarded by the Hundredfold Foundation, a non-profit organization dedicated to building resilient, open, and equitable financial infrastructure. Our commitment is to the long-term success and progressive decentralization of the protocol, ensuring it remains a public good that serves its community.

### 2. Protocol Architecture: A Three-Layer Stack
Jubilee's core innovation is its hybrid, multi-layered architecture that ensures scalability, security, and permanence through a clear separation of concerns. This design leverages the strengths of each underlying blockchain, creating a robust and resilient system.

#### 2.1. L1: The Security & Settlement Layer (Ethereum)
Ethereum serves as the foundational layer and the ultimate source of truth for the Jubilee Protocol. Its role is absolute and encompasses several critical functions, providing the bedrock of security and finality for the entire system. Jubilee inherits Ethereum's robust security guarantees, including its decentralized validator set, censorship resistance, and battle-tested smart contract environment.

* **State Verification:** As a ZK-Rollup, Jubilee's state transitions are only considered valid after a cryptographic proof (a Zero-Knowledge Succinct Non-Interactive Argument of Knowledge, or ZK-SNARK; or a Zero-Knowledge Scalable Transparent Argument of Knowledge, or ZK-STARK) is submitted to and verified by a verifier smart contract deployed on Ethereum L1. This mathematical verification ensures the integrity and correctness of every transaction that occurs on the L2 without requiring L1 nodes to re-execute them. This off-chain computation and on-chain verification significantly reduce the computational load on Ethereum, enabling higher throughput on Jubilee.
* **Data Availability:** To guarantee that the L2 state can always be reconstructed independently (a crucial property for censorship resistance and user fund safety), compressed transaction data from each L2 batch is posted as calldata to the Ethereum L1. This ensures that even if the L2's operators were to disappear or become malicious, the full state of Jubilee is fully recoverable from Ethereum, allowing users to exit their funds directly to L1 if necessary. This mechanism is fundamental to the security model of all ZK-Rollups.
* **Asset Custody:** The canonical bridges for assets like ETH and various ERC-20 tokens are controlled by immutable smart contracts on Ethereum. The L1 contracts act as the secure escrow, locking assets on Ethereum before they are represented on Jubilee. This ensures that every bridged asset on Jubilee is fully backed 1:1 by its corresponding asset on Ethereum, maintaining the peg and providing trustless asset transfer between the layers.

#### 2.2. L2: The Execution & Programmability Layer (Jubilee)
This is the active, high-performance environment where all user interactions, application logic, and the core financial primitives of the Jubilee Protocol reside. It is designed to provide a seamless and efficient user experience, leveraging the scalability benefits of ZK-Rollups.

* **EVM Compatibility:** Built using the open-source ZK Stack, Jubilee is designed to be fully EVM-compatible at the opcode level. This allows developers to migrate existing Solidity smart contracts, deploy new dApps, and use familiar development tools (e.g., Hardhat, Foundry, Truffle) without modification. This frictionless development experience significantly lowers the barrier to entry for developers and fosters rapid innovation within the Jubilee ecosystem.
* **High Throughput and Low Cost:** By processing transactions off-chain and only posting proofs and compressed data to Ethereum, Jubilee dramatically increases transaction throughput and reduces transaction costs compared to direct L1 interactions. This makes complex DeFi strategies and frequent trading economically viable for a broader range of users.
* **Native Gas Token:** The native token for paying transaction fees (gas) on the L2 is $JUBL, the protocol's governance and utility token. This design choice creates direct and continuous utility for $JUBL within the Jubilee ecosystem, ensuring that every transaction on the protocol drives demand for the token. Users can acquire $JUBL through the embedded exchange or external DEXs to pay for gas fees, creating a closed-loop economy where protocol activity directly benefits $JUBL holders. This differs from traditional L2 designs that use bridged ETH for gas, as it allows users to preserve their bridged jETH and jBTC holdings exclusively for productive uses (lending collateral, index deposits) rather than consuming them for operational overhead.

#### 2.3. L3: The Data Provenance & Anchor Layer (Bitcoin)
While Layer 2 handles execution and immediate throughput, Layer 3 in the Jubilee architecture is strictly defined as a **Sovereign Data Anchor**, not a recursive execution environment. It uses Bitcoin's blockchain solely for data permanence and immutable archival.

* **Mechanism:** An off-chain service, the **L3 Settlement Service**, periodically bundles cryptographic hashes (Merkle roots) of selected L2 state data, transaction batches, or other critical application-specific information. These Merkle roots are then embedded into a standard Bitcoin transaction via the `OP_RETURN` opcode, which allows for up to 80 bytes of arbitrary data in a Bitcoin transaction output. This data is permanently recorded on the blockchain without bloating the UTXO set.
* **Function:** This process creates a "Digital Notary" service. By anchoring Jubilee's state to Bitcoin, we provide an indisputable, proof-of-work secured timestamp of the protocol’s history. This protects against long-range attacks on the PoS layer and provides a permanent audit trail for regulatory compliance, ensuring that even if the L2 were to suffer a catastrophic failure, the historical state of assets remains verifiable via Bitcoin.
For example, imagine a decentralized insurance protocol built on Jubilee that underwrites real-world climate risk. To pay out a claim, the protocol must prove that a specific event occurred before a policy's expiration date. By anchoring the claim data hash to the Bitcoin blockchain, the protocol gains an indisputable, non-repudiable timestamp secured by the largest proof-of-work network in history.

### 3. Core Technical Components
Jubilee Protocol is built upon a foundation of robust and battle-tested cryptographic and blockchain technologies. This section details the key technical components that enable the protocol's functionality, from its L2 execution environment to its multi-chain bridging mechanisms.

#### 3.1. L2 ZK-Rollup Implementation
Jubilee leverages the ZK Stack, an open-source framework for building ZK-Rollups, to construct its L2 environment. This framework provides the necessary components for transaction processing, proof generation, and interaction with the Ethereum L1. The core of the ZK-Rollup involves two primary actors: the Sequencer and the Prover.

#### 3.1.1. The Sequencer: From Centralized to Decentralized
The Sequencer is a critical component responsible for collecting user transactions, ordering them into a sequence, constructing L2 blocks, and ultimately submitting batches of these transactions to the Ethereum L1.
* **Initial Phase (Centralized):** At launch, Jubilee Protocol will utilize a centralized Sequencer operated by the Hundredfold Foundation. This approach provides high throughput, predictable transaction ordering, and simplified maintenance during the early stages.
* **Decentralization Path (Proof-of-Stake):** The long-term vision includes a progressive transition to a decentralized Proof-of-Stake (PoS) sequencer set. Validators will be required to stake a significant amount of $JUBL tokens to participate. A leader selection algorithm will ensure fair rotation, and on-chain slashing conditions will penalize malicious behavior, ensuring honest operation.

#### 3.1.2. The Prover: Ensuring Computational Integrity
The Prover is responsible for generating the cryptographic validity proofs (ZK-SNARKs or ZK-STARKs) for each batch of L2 transactions, allowing the Ethereum L1 verifier contract to confirm the integrity of the L2 state without re-executing every transaction.
* **Initial Phase (Permissioned):** An initial permissioned Prover network will be operated by the Hundredfold Foundation to ensure timely proof generation and a smooth user experience.
* **Decentralization Path (Permissionless & Competitive):** The long-term goal is to transition to a permissionless, competitive prover market. In this model, any participant with sufficient computational resources can act as a Prover, incentivized by fees. This is expected to drive down proving costs and further decentralize the protocol.

#### 3.2. The Interoperability Fabric: Bridge Architecture & Security
Interoperability is fundamental to Jubilee's mission. Secure and efficient bridging mechanisms are essential for the seamless transfer of assets between Ethereum, Jubilee, and Bitcoin.

#### 3.2.1. The jETH Bridge: Relayer Security
The jETH bridge facilitates the trust-minimized transfer of ETH and ERC-20 tokens between Ethereum L1 and Jubilee L2. It operates on a standard lock-and-mint mechanism, where assets are locked on the L1 and an equivalent amount is minted on the L2.
* **Initial Phase (Centralized Relayer):** At launch, the relayer service will be operated by the Hundredfold Foundation to ensure high availability and rapid response.
* **Decentralization Path (PoS Validator Relayers):** The relayer role will be progressively decentralized and integrated into the L2's Proof-of-Stake validator set. A validator chosen to propose a block will also be responsible for relaying pending bridge events.

#### 3.2.2. The jBTC Bridge: Guardians & Insurance
To mitigate the risks of wrapping Bitcoin, the jBTC bridge employs a defense-in-depth model combining cryptography, economic incentives, and an automated insurance backstop.

* **The Guardian Network (TSS):** Custody is managed by a Threshold Signature Scheme (TSS) network. A Bitcoin private key is generated via a Distributed Key Generation (DKG) ceremony, split into shares among *n* nodes. A transaction requires *t* of *n* signatures to execute.
    * **Decentralized Custody:** No single node ever possesses the full key.
    * **Network Composition:** The initial "Federated Guardian Set" consists of 15 verified, geographically distributed entities (including reputable infrastructure providers and Council members).
    * **Economic Security:** Guardians must stake $JUBL tokens equal to a minimum collateralization ratio (e.g., 150%) of the BTC value they secure. Slashing is automated: if a Guardian signs a malicious transaction, their stake is burned.
* **The Jubilee Insurance Fund:** A portion of all protocol revenue (5% of index performance fees and lending origination fees) is automatically diverted to an on-chain **Insurance Fund**. This fund holds diversified assets (USDC, BTC, ETH) and serves as the "Lender of Last Resort." In the unlikely event of a bridge exploit or slashing failure, the Insurance Fund is programmatically authorized to reimburse jBTC holders, providing an institutional-grade safety net for church treasuries.

#### 3.3. The L3 Settlement Service
The L3 Settlement Service is an off-chain component responsible for creating the permanent data anchor on the Bitcoin blockchain. Its primary function is to provide an additional, immutable layer of data provenance for critical L2 information.
* **Data Aggregation & Merkle Tree Construction:** The service periodically collects and aggregates cryptographic hashes of designated L2 data, constructing a Merkle tree to create a single, compact hash (the Merkle root) that cryptographically summarizes all the included data.
* **Bitcoin OP_RETURN Embedding:** The Merkle root is then embedded into a standard Bitcoin transaction using the OP_RETURN opcode, which allows for up to 80 bytes of arbitrary data.
* **Immutable Timestamping:** By embedding the Merkle root into a Bitcoin transaction, the L3 Settlement Service creates an immutable, globally verifiable timestamp, proving with the full force of Bitcoin's proof-of-work that the specific L2 data existed at that exact time.
* **Operational Model:** The L3 Settlement Service is designed as a decentralized and automated 'cron job' for the protocol. Initially, this service may be triggered by a permissioned set of keeper bots operated by the Hundredfold Foundation to ensure reliability. However, the long-term architecture is for this role to be integrated into the L2's Proof-of-Stake validator set.

### 4. Core Products: The Jubilee Asset Suite
Jubilee Protocol is not merely an infrastructure layer; it is a platform designed to host and optimize a suite of innovative, yield-generating financial products. These products are engineered to unlock new forms of capital efficiency, provide diversified exposure to core crypto assets, and generate sustainable yield through automated strategies. The core products are built as ERC-4626 compliant tokenized vaults, ensuring composability and ease of integration within the broader DeFi ecosystem.

#### 4.1. Product Philosophy: Automated, Yield-Bearing Primitives
Our product philosophy centers on creating automated, yield-bearing primitives that abstract away complexity for the end-user while maximizing capital efficiency. By encapsulating sophisticated strategies within standardized ERC-4626 vaults, we enable composability, allowing other DeFi protocols to easily integrate and build upon Jubilee's offerings. This approach aims to make advanced yield generation accessible to a wider audience, from retail investors to institutional players.

#### 4.2. jBTCi: The Jubilee Bitcoin Index
jBTCi (Jubilee Bitcoin Index) is a decentralized, yield-generating index fund designed to systematically capture and distribute value from the fragmented Bitcoin liquidity across the Ethereum ecosystem. It represents a diversified basket of leading Bitcoin representations on Ethereum, actively managed to exploit price inefficiencies and generate alpha for its holders.
* **Thesis and Value Proposition:** The fundamental thesis behind jBTCi is that while all wrapped/bridged Bitcoin tokens on Ethereum are theoretically pegged 1:1 to native BTC, small but persistent price deviations exist. jBTCi is engineered to systematically identify and exploit these "peg-delta" opportunities, generating consistent arbitrage profits that accrue to jBTCi holders. It offers automated alpha generation, diversified Bitcoin exposure, and transforms a non-yield-bearing asset into a productive one.
* **Portfolio Composition and Governance:** The jBTCi vault holds a dynamic basket of leading Bitcoin representations, governed by the Jubilee Council. The Council establishes a clear framework for including new assets based on criteria like bridge security, decentralization, liquidity, and audit history. The initial proposed basket includes wBTC, tBTC, rBTC, cbBTC, and the native jBTC, with target weights set and adjusted by Council governance.

#### 4.3. jETHs: The Jubilee Ethereum Staked Index
jETHs (Jubilee Ethereum Staked Index) is a diversified index of yield-bearing, liquid-staked Ethereum (LST) tokens. It is designed to provide broad exposure to the Ethereum staking ecosystem while simultaneously generating additional alpha through systematic arbitrage strategies.
* **Thesis and Dual Yield Source:** The value of jETHs grows from two sources: 1) the base staking yield from the underlying LSTs as they accrue consensus rewards, and 2) arbitrage alpha generated by the Rebalancing Engine from trading between LSTs when their prices deviate. This offers diversified staking exposure, automated yield optimization, and compounding returns.
* **Portfolio Composition and Governance:** Similar to jBTCi, the jETHs composition is dynamic and managed by the Jubilee Council. The Council defines rigorous security and liquidity standards for including new LSTs. The initial proposed basket includes established LSTs like stETH, rETH, and cbETH, with target weights governed by the Council.

#### 4.4. jUSDi: The Jubilee Stablecoin Index
jUSDi (Jubilee USD Index) is a yield-optimized stablecoin index designed to maintain stable value while generating returns through systematic rebalancing between leading USD-pegged stablecoins. It represents a diversified basket of established stablecoins, actively managed to exploit small price inefficiencies and provide superior capital stability.
* **Thesis and Value Proposition:** While stablecoins are designed to maintain a 1:1 peg to the US Dollar, market dynamics create temporary deviations from this peg. jUSDi systematically captures value from these micro-arbitrage opportunities while maintaining the stability characteristics users expect from dollar-denominated assets. The product offers stable value preservation, automated yield generation from peg arbitrage, diversified stablecoin exposure reducing single-issuer risk, and a composable primitive for DeFi applications requiring stable collateral.
* **Portfolio Composition and Governance:** The jUSDi vault holds a dynamic basket of leading stablecoins, governed by the Jubilee Council. The Council establishes strict criteria for inclusion based on regulatory compliance, reserve transparency, redemption reliability, market liquidity, and issuer reputation. The initial proposed basket includes USDC and DAI, with target weights set and adjusted by Council governance.
* **Multi-Chain Strategy:** jUSDi, along with jBTCi and jETHs, is designed as a multi-chain product suite. While the core protocol infrastructure operates on the Jubilee L2 (built on zkSync Era), these index strategies will be deployed across multiple blockchain ecosystems to maximize accessibility and capture arbitrage opportunities where they exist. Initial deployments are planned for Jubilee L2, Base, and other EVM chains.

#### 4.5. The Rebalancing Engine & Oracle Security Model
The Rebalancing Engine is the core intelligence behind the jBTCi, jETHs, and jUSDi index products. It is a sophisticated, automated system designed to identify and execute profitable arbitrage opportunities within the specified asset baskets.
* **Off-Chain Analysis & On-Chain Execution:** An off-chain component continuously monitors markets to identify arbitrage opportunities. Once found, it initiates an on-chain transaction. To prevent front-running and ensure profitability, the engine employs MEV protection strategies like private mempool submission and includes an atomic on-chain check that reverts the transaction if it is not profitable after all costs.
* **External DEX Execution:** The Rebalancing Engine executes arbitrage trades on external decentralized exchanges with deep liquidity, including Uniswap V3, Curve Finance, SyncSwap, and others. This external execution strategy is critical because arbitrage opportunities exist where deep liquidity lives.
* **Oracle Security Model:** The integrity of the index products depends on secure price data. The engine incorporates a multi-layered oracle security model using Chainlink Price Feeds as the primary source, supplemented by built-in circuit breakers that pause activity if price data exceeds a predefined "sanity bound" (e.g., >10% deviation in a single block).

#### 4.5.1. Long-Term Strategy: Beyond Arbitrage
While the Rebalancing Engine is designed to capture arbitrage profits from peg deviations, the protocol recognizes that these opportunities may diminish as markets become more efficient. Therefore, the engine's primary long-term value proposition is not just profit generation, but sophisticated index health and risk management.
Its core function will evolve into a liquidity balancing tool. By systematically selling the over-weighted asset and buying the under-weighted one, the engine actively helps maintain the peg of all constituent assets within the index. This creates a healthier, more stable ecosystem for all wrapped/staked tokens on Jubilee. In this mature state, its value is twofold:
1. Risk Mitigation: It acts as an automated portfolio manager, reducing the index's exposure to any single asset that may be de-pegging or experiencing issues.
2. Public Good: It provides a constant source of stabilizing liquidity, benefiting the entire Jubilee ecosystem.

#### 4.5.2. Index Product Revenue Model
While the index products (jBTCi, jETHs, jUSDi) generate yield for depositors through automated arbitrage, the protocol also captures fees from managing these strategies. This fee structure provides sustainable revenue to support protocol operations and distribute value to $JUBL token holders.

**Fee Structure:**
* **Management Fee:** 0.5-1% of Assets Under Management (AUM) annually.
* **Performance Fee:** 10-20% of gross arbitrage profits. This aligns protocol incentives with depositor success—the protocol only earns when it successfully generates yield.

**Fee Collection Mechanism:**
Fees are continuously collected as yield is generated and deposited into the `FeeCollector.sol` smart contract (detailed in Section 5.3). All fees are then:
1. Converted to jBTC and jETH via external DEXs or the internal embedded exchange
2. Distributed to $JUBL holders via the Choice Yield mechanism
3. Claimable at any time by $JUBL holders in their preferred asset (jBTC, jETH, or both)

**Projected Index Revenue (Year 3):**

| Product | AUM | Management Fee (1%) | Arbitrage Yield | Performance Fee (15%) | Total Revenue |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **jBTCi** | $50M | $500K | $4M (8% APY) | $600K | $1.1M |
| **jETHs** | $30M | $300K | $2.1M (7% APY) | $315K | $615K |
| **jUSDi** | $20M | $100K | $800K (4% APY) | $120K | $220K |
| **Total** | **$100M** | **$900K** | **$6.9M** | **$1.035M** | **$1.935M** |

**After fees, depositors still earn:**
* **jBTCi:** 6.8% net APY (vs. 0% holding BTC elsewhere)
* **jETHs:** 5.95% net APY (vs. 3.5% staking ETH directly)
* **jUSDi:** 3.4% net APY (vs. 0% holding stablecoins in bank accounts)

This fee structure ensures the protocol is economically sustainable before Jubilee Lending even launches, providing immediate revenue to $JUBL holders from Day 1 of index product operations.

#### 4.6. Jubilee Lending: The Capital Efficiency Layer
Jubilee Lending is the protocol's flagship capital efficiency product, enabling users to unlock liquidity from their yield-bearing index tokens (jBTCi, jETHs) without selling their underlying Bitcoin or Ethereum exposure. Unlike traditional DeFi lending platforms that charge interest, Jubilee Lending uses a yield-backed repayment model where the collateral's automated arbitrage profits automatically pay down the loan over time.
* **Launch Timeline:** Jubilee Lending will launch on Good Friday 2026, approximately 3-6 months after the index products are live and generating consistent yield.

#### 4.6.1. Core Mechanism: Yield-Backed Borrowing
* **Collateral Assets:** Users deposit yield-generating index tokens:
    * jBTCi (generating arbitrage yield from BTC peg deviations)
    * jETHs (generating staking rewards + arbitrage yield)
* **Borrow Asset:** jUSDi (stablecoin index) for immediate liquidity
* **Automatic Repayment:** The yield generated by jBTCi/jETHs is automatically applied to reduce the loan principal. There are no interest charges—the only "cost" is the opportunity cost of the yield that would otherwise accrue to the depositor.
* **Example:** Church deposits $100,000 in jBTCi (generating 8% APY from arbitrage) and borrows $50,000 in jUSDi for building expansion. The jBTCi generates $8,000/year in yield, which is automatically applied to loan repayment. The loan is fully repaid in ~6.25 years from yield alone, and the Church retains Bitcoin exposure while accessing immediate capital.

#### 4.6.2. The $JUBL Token in Lending: Credits + Value Accrual
The $JUBL token serves three interconnected functions within Jubilee Lending:

**A. Lending Credits (Primary Utility)**
$JUBL unlocks additional borrowing capacity beyond the base loan-to-value ratio.
* **Base Lending (Without $JUBL):** Deposit $100,000 in jBTCi → Borrow up to $50,000 in jUSDi (50% LTV).
* **Enhanced Lending (With $JUBL):** Deposit $100,000 in jBTCi + 10,000 $JUBL tokens → Borrow up to $60,000 in jUSDi (60% effective LTV).
* **Conversion Ratio:** 1 $JUBL = $1 of additional borrowing capacity.
* **Maximum Boost:** Up to +20% LTV (requiring 20,000 $JUBL per $100K collateral for maximum enhancement).

**B. Deflationary Burn Mechanism**
$JUBL deposited for lending is locked within the lending contract for the loan's entire duration. Upon full repayment:
* 50% of deposited $JUBL is permanently burned (removed from circulating supply).
* 50% is returned to the borrower.
This creates continuous deflationary pressure as lending volume increases.

**Projected Burn Rate:**

| Annual Lending Volume | $JUBL Locked | Annual Burn (8yr avg) | % of Supply |
| :--- | :--- | :--- | :--- |
| $10M | 10M $JUBL | 625,000 | 0.06% |
| $50M | 50M $JUBL | 3,125,000 | 0.31% |
| $100M | 100M $JUBL | 6,250,000 | 0.63% |
| $500M | 500M $JUBL | 31,250,000 | 3.13% |

**C. Choice Yield Revenue Sharing**
Beyond lending utility, $JUBL holders participate in protocol revenue through the "Choice Yield" mechanism. All protocol revenue is collected in native assets (jBTC, jETH, jUSD) and distributed pro-rata to $JUBL holders based on their share of the total supply.

#### 4.6.3. The Embedded Exchange: Internal Liquidity Layer
While Jubilee Lending is the primary economic engine, it requires robust liquidity infrastructure to function efficiently. The Jubilee Exchange is not a standalone DEX competing with Uniswap or Curve, but rather an embedded liquidity layer purpose-built to support lending operations and index rebalancing.
* **Critical Distinction:** Index arbitrage happens on external DEXs (Uniswap, Curve). Jubilee Exchange handles internal protocol operations like swapping between Jubilee assets (jBTCi ↔ jETHs), liquidation flows, and fee conversions.
* **Liquidity Strategy:** Rather than competing for external liquidity providers, the Jubilee Exchange relies primarily on Protocol-Owned Liquidity (POL) and Treasury Allocation (20% of $JUBL supply).
* **Fees:** 100% of exchange trading fees flow to $JUBL holders.

#### 4.6.4. Loan Parameters and Repayment Flexibility
**Self-Repaying Mechanism:**
Loans are designed to be "set and forget." The yield from the collateral (jBTCi/jETHs) is harvested weekly and applied to the loan principal. There are no monthly payments required.

**Voluntary Repayment & Top-Ups (Crucial for Treasurers):**
We recognize that institutional treasuries require predictable amortization schedules. Therefore, Jubilee Lending includes **Voluntary Repayment** functionality:
* **Manual Pay-Down:** Borrowers can manually repay any portion of the loan principal in jUSDi at any time. This allows churches to accelerate debt retirement or close a loan early if they wish to unlock their collateral for other needs.
* **Collateral Top-Up:** If market yields compress (e.g., DeFi yields drop from 8% to 2%), extending the estimated repayment time, borrowers can deposit additional collateral or make one-time principal payments to keep their original repayment timeline on track. This ensures that a 5-year target payoff date doesn't drift into a 15-year term due to market conditions.

**Loan-to-Value & Liquidation Thresholds:**

| Collateral Type | Base LTV | With $JUBL Boost | Max LTV | Liquidation Threshold |
| :--- | :--- | :--- | :--- | :--- |
| **jBTCi** | 50% | +20% | 70% | 80% |
| **jETHs** | 50% | +20% | 70% | 80% |
| **jUSDi** | 80% | +10% | 90% | 95% |

**Health Factor Monitoring:**
Every loan has a continuously calculated Health Factor. If the Health Factor > 1.0, the loan is healthy. If it falls below 1.0, it is eligible for liquidation. Before a full liquidation occurs, the protocol allows for a "Self-Correction" period where the borrower is notified to top up collateral.

#### 4.6.5. Fee Structure and Revenue Model
Jubilee Lending operates on an interest-free model—borrowers pay no ongoing interest charges. Instead, the collateral's yield automatically repays the loan principal over time. This creates a fundamentally different fee structure from traditional DeFi lending protocols.

**One-Time Fees:**
1. **Origination Fee:** 0.5% of borrowed amount (one-time, paid in jUSDi).
2. **$JUBL Boost Fee:** 0.1% of $JUBL deposited (one-time, burned immediately).

**Event-Based Fees:**
3. **Liquidation Fee:** 2% of collateral value (charged to borrower if liquidated).
4. **Early Withdrawal Fee:** 1% of collateral (if withdrawn before loan 50% repaid).

**Projected Lending Revenue (Year 3):**

| Fee Type | Basis | Annual Volume | Revenue |
| :--- | :--- | :--- | :--- |
| Origination (0.5%) | $20M in new loans | $100,000 | |
| Liquidations (2%) | $2M liquidated | $40,000 | |
| Early Withdrawal (1%) | $1M early exits | $10,000 | |
| $JUBL Boost (0.1%) | 100K $JUBL deposited | @ $1/$JUBL | $100 (burned) |
| **Total** | | | **$150,000** |

**Comparison to Index Product Revenue (Year 3):**

| Source | Revenue | % of Total |
| :--- | :--- | :--- |
| Index Management Fees | $900,000 | 43% |
| Index Performance Fees | $1,035,000 | 49% |
| Lending Fees | $150,000 | 7% |
| Exchange Fees | $25,000 | 1% |
| **Total Protocol Revenue** | **$2,110,000** | **100%** |

Key Insight: Index products generate 93% of protocol revenue. Lending is a strategic feature, not the primary business model. The protocol makes money from managing yield-bearing assets (jBTCi/jETHs/jUSDi), not from charging interest on loans. All revenue flows to $JUBL holders via the Choice Yield mechanism.

#### 4.6.6. Multi-Chain Deployment Strategy
Like the index products (jBTCi, jETHs, jUSDi), Jubilee Lending will deploy across multiple chains to maximize accessibility and capital efficiency:
* **Primary Chain:** Jubilee L2 (zkSync-based).
* **Secondary Chain:** Base (Coinbase ecosystem).
* **Tertiary Chains:** Additional EVM chains as approved by Council.
**Cross-Chain Considerations:** Lending contracts on each chain are independent instances—there is no cross-chain borrowing. A user with collateral on Base cannot borrow against it on zkSync. This design choice prioritizes security over convenience, as cross-chain lending introduces significant attack vectors. However, $JUBL tokens will be bridged across all deployment chains using LayerZero OFT (Omnichain Fungible Token) standard.

#### 4.7. Mathematical Framework & Fee Structure Summary
* **Mathematical Framework:** The Net Asset Value per share (NAV) of an index token reflects the total value of the underlying assets plus accumulated arbitrage profits, divided by the total supply of the index token. As the Rebalancing Engine generates profits, they are compounded back into the vault, increasing the NAV.
* **Comprehensive Fee Structure:**
    * Index Management Fees: 0.5-1% of AUM annually
    * Index Performance Fees: 10-20% of arbitrage profits
    * Lending Origination Fees: 0.5% of borrowed amount
    * Lending Liquidation Fees: 2% of liquidated collateral
    * Exchange Trading Fees: 0.05-0.3% per swap (internal operations only)

#### 4.8. Minting and Redemption Mechanics
As ERC-4626 compliant vaults, the minting and redemption processes for jBTCi, jETHs, and jUSDi are standardized and intuitive. Users can mint new index tokens by depositing an approved underlying asset into the respective vault. The vault contract calculates the current NAV and mints a proportional amount of the index token. Conversely, users can redeem their index tokens for a proportional amount of the underlying assets held in the vault. Small fees may be applied to minting and redemption to prevent oracle front-running and contribute to the protocol treasury.

### 5. The Economic Engine: Value Accrual and Distribution
The Jubilee Protocol is designed with a robust economic engine that ensures sustainable value accrual for the protocol and its participants. This engine is powered by automated index products, yield-backed lending, an embedded liquidity layer, and a novel tokenomics structure that aligns incentives and distributes value back to the community.

#### 5.1. The Jubilee Exchange: Embedded Liquidity Infrastructure
The Jubilee Exchange is not a standalone product competing with established DEXs, but rather an embedded liquidity layer designed specifically to support Jubilee Lending operations and internal protocol swaps.
* **Purpose:** Provide efficient liquidity for loan collateral liquidations, internal conversions between Jubilee assets (jBTCi ↔ jETHs ↔ jUSDi), and fee revenue consolidation.
* **Architecture:** Hybrid AMM model combining Stable pools (0.05% fee) for pegged assets and Concentrated liquidity pools (0.3% fee) for cross-asset swaps.
* **Liquidity Strategy:** Protocol-Owned Liquidity (POL) funded by treasury (20% of $JUBL allocation) and Community LPs during bootstrap phase.
* **Critical Distinction:** The Jubilee Exchange is not where jBTCi, jETHs, and jUSDi generate their arbitrage profits. Index product yield is generated by the Rebalancing Engine executing trades on external DEXs (Uniswap, Curve, SyncSwap) where deep liquidity exists.

#### 5.2. The $JUBL Token: Lending Credits, Revenue Share, and Governance
The $JUBL token serves as the economic and governance backbone of Jubilee Protocol, with three interconnected utilities that create sustainable value accrual.

#### 5.2.1. Primary Utility: Lending Credits (Launching Good Friday 2026)
**A. Native Gas Token (Immediate Utility from Launch)**
$JUBL serves as the native gas token for the Jubilee L2, meaning every transaction on the protocol requires $JUBL to pay for gas fees. This creates immediate and continuous demand for the token. Unlike traditional L2 designs that use bridged ETH (jETH) for gas, Jubilee's use of $JUBL allows users to preserve their bridged jETH and jBTC holdings exclusively for productive uses.

**B. Lending Credits (Launching Good Friday 2026)**
When Jubilee Lending launches, $JUBL's utility expands to unlocking additional borrowing capacity beyond the base loan-to-value ratio (see Section 4.6.2 for details).
* **Deflationary Burn Mechanism:** As Jubilee Lending scales, $JUBL supply progressively contracts as 50% of the tokens used for boosts are burned upon loan repayment.
* **Why This Matters for Churches:** Many churches using the Zero21 Framework to build Bitcoin reserves will eventually need to access capital for building expansions, mission trips, or operational needs. Rather than selling their Bitcoin (losing long-term exposure) or taking traditional loans (paying interest), they can use jBTCi as collateral, unlock maximum borrowing capacity with $JUBL tokens, and let the yield repay the loan.

#### 5.2.2. Secondary Utility: Choice Yield Revenue Sharing
Pre-Lending Launch (2026-2027), $JUBL holders immediately begin receiving protocol revenue from index product operations. Post-Lending Launch (2027+), revenue sources expand to include lending fees.
* **Revenue Sources Flowing to $JUBL Holders:** Index management/performance fees, Lending origination/liquidation fees, Exchange trading fees, and $JUBL boost fees.
* **Distribution Mechanism:** All protocol revenue is collected in the `FeeCollector.sol` smart contract, converted to jBTC and jETH, and distributed pro-rata to $JUBL holders based on their share of total supply.
* **Claiming Options:** Holders can claim rewards in jBTC only, jETH only, or a proportional mix.

#### 5.2.3. Tertiary Utility: Governance Rights
$JUBL holders participate in protocol governance through two distinct channels:

**A. Jubilee Council (Verified Organizations)**
Verified churches and Christian nonprofits that complete the Know Your Organization (KYO) process can join the Jubilee Council by staking $JUBL:

| Organization Size | Required $JUBL Stake |
| :--- | :--- |
| Small (< 500 members) | 50,000 $JUBL |
| Medium (500-2,000 members) | 100,000 $JUBL |
| Large (2,000-10,000 members) | 250,000 $JUBL |
| Megachurch (10,000+ members) | 500,000 $JUBL |
| Denominational Networks | 1,000,000 $JUBL |

**Governance Scope:**
* Protocol fee adjustments (lending rates, index fees, liquidation thresholds)
* Collateral additions (which assets can be used in lending)
* Treasury allocations (grant distributions, Protocol-Owned Liquidity deployment)
* Smart contract upgrades (via timelock)
* Index composition (jBTCi/jETHs/jUSDi constituent asset weights)

**Critical Design Choice:** Each verified organization receives 1 equal vote regardless of $JUBL staked. The staking requirement creates economic alignment and attack resistance (corrupting governance requires both infiltrating real-world organizations AND acquiring massive amounts of $JUBL), but does not create plutocracy.

**B. Community Governance (All $JUBL Holders)**
$JUBL holders who are not Council members participate through the **Hundredfold Grant Program** (nominating and voting on grant recipients), **Signal Voting** (off-chain polls), and **Delegation**.

#### 5.2.4. $JUBL Value Accrual Summary
$JUBL captures value through multiple reinforcing mechanisms: Gas token utility (from Day 1), Income-Producing Asset (via Choice Yield), and Deflationary Mechanics (via lending burns). Unlike most DeFi tokens that rely solely on speculation, $JUBL has intrinsic value derived from mandatory gas demand, discounted cash flows of protocol revenue, and structural scarcity.

#### 5.3. Choice Yield: Technical Implementation

#### 5.3.1. Revenue Collection
All protocol revenue streams flow to a single `FeeCollector.sol` smart contract. All fees collected in jUSD are immediately swapped to jBTC and jETH via the Jubilee Exchange at market rates, ensuring $JUBL holders receive rewards in the protocol's primary productive assets.

#### 5.3.2. Distribution Mechanism
* **Smart Contract Architecture:** `FeeCollector.sol` aggregates all revenue; `ChoiceYieldDistributor.sol` calculates pro-rata shares and handles claims.
* **Distribution Formula:**
    ```
    User's Pending jBTC = (Total jBTC Revenue × User's $JUBL Balance) / Total $JUBL Supply
    User's Pending jETH = (Total jETH Revenue × User's $JUBL Balance) / Total $JUBL Supply
    ```
* **Claiming Options:** Users call `claimRewards(bool claimJBTC, bool claimJETH)` to receive their share. Unclaimed rewards auto-compound.

#### 5.3.3. Gas Optimization
To minimize gas costs for small holders:
* Rewards accrue passively without requiring user action
* Claims are batched (monthly snapshots of $JUBL holdings)
* Minimum claim threshold: $10 equivalent in jBTC/jETH (prevents uneconomical gas spending)

#### 5.3.4. Example Revenue Flow
**Scenario:** $500K in protocol revenue (one quarter) → 60% jBTC ($300K) / 40% jETH ($200K)
* **User A (Hold 0.5% of Supply):** Earns $1,500 in jBTC + $1,000 in jETH. Claims all as jBTC ($2,500 total).
* **User B (Hold 5% of Supply):** Earns $15,000 in jBTC + $10,000 in jETH. Claims 50/50 mix.
* **User C (Hold 0.01% of Supply):** Earns $30 in jBTC + $20 in jETH. Below minimum threshold, accumulates for future claim.

### 6. Governance: The Jubilee Council
The Jubilee Protocol is governed by the Jubilee Council, an innovative governance body that operates similarly to a decentralized autonomous organization (DAO) but with a mission-aligned membership structure. Like traditional DAOs, the Council makes decisions through on-chain voting, maintains transparent proposal processes, and manages protocol parameters autonomously. However, rather than token-weighted voting by anonymous holders, the Council is composed of verified organizations with long-term stewardship commitments.

#### 6.1. Principles of Stewardship
The Jubilee Council is founded on the principle of long-term stewardship over the protocol as a vital public good for a specific community, with a multi-generational vision. Governance prioritizes the sustained health, security, and ethical development of the protocol in alignment with Christian principles of service, integrity, and community welfare. The governance culture will emphasize Transparency, Accountability, Mission-Alignment, and Resilience.

#### 6.2. Council Composition: A United Group
The Jubilee Council, the primary governing body for key protocol parameters and upgrades, is composed of verified, Bible-believing Christian churches and mission-aligned non-profit organizations.
* **Rationale:** This model is chosen to create a stable, values-driven governance layer. These institutions possess long-term operational horizons and established community trust.
* **Verification Process:** The Hundredfold Foundation will manage a robust 'Know Your Organization' (KYO) process to verify the legal identity, non-profit status, doctrinal alignment, and operational history of each applicant.
* **Staking Requirement & Security:** Each verified organization will be required to stake a significant amount of $JUBL tokens to activate and maintain its voting power.

#### 6.3. The Hundredfold Grant Program: Empowering the Ecosystem
While the Jubilee Council holds formal governance power over core protocol functions, the broader community of $JUBL token holders plays a vital and distinct role in directing the protocol's real-world impact through grant-making.
* **Proposal & Nomination:** On a quarterly basis starting 1 year after mainnet, any $JUBL holder can nominate organizations or projects that they believe align with Christian morals and values for consideration.
* **Final Approval & Funding:** The top-voted nominees from the community vote are then presented to the Hundredfold Foundation (and, in the future, the Jubilee Council) for a final review and approval.

#### 6.4. Scope of Governance & Legal Wrapper
The Jubilee Council will have comprehensive authority over all key aspects of the protocol, ensuring that its evolution is guided by its governors.
* **Protocol Parameters:** Fees, risk parameters, and reward rates.
* **Treasury Management:** Allocating funds for grants, core development, and POL.
* **Smart Contract Upgrades:** Via a timelock contract.
* **Index Management:** Strategic direction of index products.
* **Legal Wrapper:** To facilitate interactions with the traditional legal and financial systems, the Jubilee Council will be wrapped in a legal entity based in the US. The Hundredfold Foundation will serve as governance for Jubilee Protocol, holding intellectual property and managing global operations.

### 7. Security and Risk Factors
Security is paramount for any decentralized protocol, especially one dealing with significant financial value and bridging across multiple blockchains. The Jubilee Protocol employs a multi-layered security approach, combining cryptographic assurances, economic incentives, and robust operational practices.

#### 7.1. A Multi-Layered Security Model
Jubilee Protocol's security is derived from a defense-in-depth strategy, leveraging the strengths of its underlying layers and implementing additional safeguards at the application level.
* **L1 Security (Ethereum):** The ultimate security and finality of the Jubilee L2 are inherited directly from Ethereum. All L2 state transitions are cryptographically proven via ZK-SNARKs/STARKs.
* **L3 Permanence (Bitcoin):** While not directly contributing to the L2's real-time security, the L3 Bitcoin layer provides an unparalleled level of data permanence by anchoring cryptographic hashes of critical L2 state data to the Bitcoin blockchain.
* **Economic Security (Staking & Slashing):** The decentralization of the Sequencer and the jBTC bridge's TSS Network is economically secured by $JUBL staking.
* **Insurance Fund:** An on-chain fund holding diverse assets serves as a backstop for the jBTC bridge, programmatically authorized to reimburse jBTC holders in the event of an exploit.
* **Smart Contract Security:** All smart contracts will undergo rigorous security assessments, including internal code reviews, external audits by top-tier firms, formal verification for critical components, and a continuous bug bounty program.
* **Oracle Security:** A multi-layered oracle security model using Chainlink Price Feeds with built-in circuit breakers and TWAP checks.

#### 7.2. Key Risk Considerations
Despite robust security measures, all blockchain protocols carry inherent risks. Participants should be aware of:
* **Smart Contract Risk:** Potential for unforeseen bugs or vulnerabilities.
* **Technology Risk:** Risks associated with cutting-edge ZK-Rollups and TSS/MPC technology.
* **Market Risk:** Value of assets held within the protocol is subject to volatility.
* **Centralization Risk (Early Phase):** Temporary risks associated with centralized components during bootstrapping.
* **Bridge Risk:** Potential vulnerabilities in bridge contracts or operational failures.
* **Regulatory Risk:** Uncertain legal landscape for digital assets.
* **Governance Risk:** Challenges in scaling the novel stewardship model.
* **Liquidity Risk:** Potential for high slippage or difficulty exiting positions.

### 8. Roadmap and Tokenomics
#### 8.1. The Jubilee Rollout: A Phased Deployment
The development and deployment of the Jubilee Protocol will follow a phased approach, metaphorically structured around the four phases: Yoke, Harvest, Wisdom, Heritage.

* **Phase 1: "Yoke" — Foundation & Community Cultivation (H2 2025 - H1 2026):** Establish core technical infrastructure (L2 smart contracts, testnet), internal audits, and cultivate the foundational community. Formalize Hundredfold Foundation.
* **Phase 2: "Harvest" — Mainnet Launch & Token Generation (H2 2026):** Deployment of Jubilee L2 Mainnet, Token Generation Event (TGE) for $JUBL, and initial liquidity mining.
* **Phase 3: "Wisdom" — The Asset Suite & Real Yield Activation (H1 2027):** Deployment of jBTCi, jETHs, jUSDi vaults. Activation of Rebalancing Engine and Choice Yield mechanism. Launch of Jubilee Lending (Good Friday 2026).
* **Phase 4: "Heritage" — Permanent Provenance & Decentralization (H2 2027+):** Activation of L3 Settlement Service. Progressive decentralization of Sequencer, Prover, and TSS Network. Full launch of Jubilee Council governance.

#### 8.2. $JUBL Tokenomics and Emissions
The $JUBL token is designed to be the economic backbone of the Jubilee Protocol, aligning incentives across all participants.

* **Total Supply (Max):** 1,000,000,000 $JUBL
* **Emission Schedule:** Staking rewards (25% of supply) distributed on a logarithmic decay schedule, halving each year for the first 4-5 years.

**Token Allocation:**

| Category | Percentage | Tokens | Vesting Schedule | Rationale |
| :--- | :--- | :--- | :--- | :--- |
| **Community & Ecosystem** | 40% | 400,000,000 | 4-5 years (linear) | Designed to bootstrap liquidity, incentivize early adopters, fund ecosystem grants, and support community initiatives. |
| **Staking Rewards** | 25% | 250,000,000 | 5+ years (logarithmic) | Incentivizes $JUBL staking for network security (sequencers, TSS nodes) and governance participation. |
| **Foundation & Core Team** | 20% | 200,000,000 | 1yr cliff, 3yr linear | Compensates the founding team and core contributors for their long-term commitment. |
| **Investors (Private)** | 10% | 100,000,000 | 1yr cliff, 2yr linear | Provides capital for initial development and audits. |
| **Public Sale / Liquidity** | 5% | 50,000,000 | 100% Unlocked | Facilitates initial public distribution and provides immediate liquidity. |

### 9. Conclusion
The Jubilee Protocol represents a fundamental step forward in the evolution of decentralized infrastructure. By refusing to accept the inherent trade-offs of a fragmented Web3 landscape, we have designed a system that is both highly performant and permanently secure. The integration of an Ethereum-based ZK-Rollup (L2) with a Bitcoin-based Provenance Layer (L3) creates a novel architectural primitive, unlocking unprecedented levels of scalability, data immutability, and cross-chain interoperability.

Through its core products—the jBTCi, jETHs, and jUSDi automated, yield-generating index funds, combined with the innovative Jubilee Lending protocol—Jubilee unlocks new forms of capital efficiency for Bitcoin, Ethereum, and stablecoin assets. The introduction of "Choice Yield" establishes a powerful economic flywheel, aligning incentives and distributing real protocol revenue to $JUBL stakers. The multi-layered security model, progressive decentralization roadmap, and robust governance framework underscore our commitment to building a resilient and sustainable ecosystem.

Jubilee is more than just a protocol; it is a vision for a unified, secure, and capital-efficient decentralized future. We invite developers, users, and stakeholders to join us in building this symbiotic superstructure, bridging the great divide, and ushering in a new era of blockchain innovation aligned with principles of stewardship, transparency, and long-term value creation.

### 10. Disclaimer
This whitepaper is for informational purposes only and does not constitute an offer to sell or a solicitation of an offer to buy any securities or tokens. It is not intended to provide legal, financial, or investment advice. The information contained herein may not be exhaustive and does not imply any elements of a contractual relationship. Please consult with a qualified professional before making any investment decisions.

The Jubilee Protocol is under development, and its features, design, and implementation are subject to change without notice. There are inherent risks associated with blockchain technology, cryptocurrencies, and decentralized finance, including but not limited to loss of funds, smart contract vulnerabilities, market volatility, and regulatory uncertainty. Participants should conduct their own due diligence and understand these risks before engaging with the protocol.

### 11. Definitions
* **AMM (Automated Market Maker):** A type of decentralized exchange protocol that relies on mathematical formulas to price assets.
* **Arbitrage:** The simultaneous buying and selling of an asset in different markets to profit from price differences.
* **calldata:** A special read-only, non-modifiable area in Ethereum transactions used to pass arguments to a contract function.
* **DAO (Decentralized Autonomous Organization):** An organization represented by rules encoded as a computer program, transparent, controlled by the organization's members, and not influenced by a central government.
* **DeFi (Decentralized Finance):** An umbrella term for financial applications enabled by blockchain technology, typically without intermediaries.
* **DKG (Distributed Key Generation):** A cryptographic process where multiple parties jointly compute a shared secret key, but no single party ever knows the entire key.
* **ERC-20:** A technical standard used for all smart contracts on the Ethereum blockchain for fungible tokens.
* **ERC-4626:** A tokenized vault standard designed to optimize and standardize the yields of interest-bearing tokens.
* **EVM (Ethereum Virtual Machine):** The runtime environment for smart contracts in Ethereum.
* **jBTC:** Bridged Bitcoin on the Jubilee L2.
* **jBTCi:** The Jubilee Bitcoin Index, a yield-generating index fund.
* **jETH:** Bridged Ethereum on the Jubilee L2, also used as the native gas token.
* **jETHs:** The Jubilee Ethereum Staked Index, a diversified index of liquid-staked Ethereum tokens.
* **jUSD:** Bridged USD stablecoins on the Jubilee L2.
* **jUSDi:** The Jubilee USD Index, a yield-optimized stablecoin index.
* **L1 (Layer 1):** The base blockchain (e.g., Ethereum, Bitcoin).
* **L2 (Layer 2):** A scaling solution built on top of an L1 blockchain (e.g., ZK-Rollups).
* **L3 (Layer 3):** An additional layer built on top of an L2 for data permanence.
* **LST (Liquid Staking Token):** A token representing staked ETH, allowing users to retain liquidity while earning staking rewards.
* **MEV (Maximal Extractable Value):** The maximum value that can be extracted from block production in excess of the standard block reward and gas fees by including, excluding, or reordering transactions within a block.
* **Merkle Root:** The top hash in a Merkle tree, which summarizes all the transactions or data in the tree.
* **MPC (Multi-Party Computation):** A cryptographic protocol that allows multiple parties to jointly compute a function over their inputs while keeping those inputs private.
* **NFT (Non-Fungible Token):** A unique and non-interchangeable unit of data stored on a digital ledger.
* **OP_RETURN:** A Bitcoin script opcode that allows for the inclusion of up to 80 bytes of arbitrary data in a transaction output.
* **PoS (Proof-of-Stake):** A consensus mechanism where validators are chosen to create new blocks based on the amount of cryptocurrency they hold and are willing to "stake" as collateral.
* **PoW (Proof-of-Work):** A consensus mechanism where participants (miners) solve complex computational puzzles to validate transactions and create new blocks.
* **Sequencer:** A component in a ZK-Rollup responsible for ordering transactions and submitting them to the L1.
* **TGE (Token Generation Event):** The initial distribution of a new cryptocurrency token.
* **TSS (Threshold Signature Scheme):** A cryptographic scheme where a signature can only be generated if a threshold number of participants cooperate.
* **TWAP (Time-Weighted Average Price):** The average price of an asset over a specified time period.
* **UTXO (Unspent Transaction Output):** The amount of cryptocurrency remaining after a transaction, which can be used as input for new transactions.
* **ZK-Rollup:** A Layer 2 scaling solution that bundles (rolls up) hundreds of transactions off-chain and generates a cryptographic proof (ZK-SNARK/STARK) of their validity, which is then posted to the L1.
* **ZK-SNARK (Zero-Knowledge Succinct Non-Interactive Argument of Knowledge):** A type of zero-knowledge proof that allows one party to prove possession of certain information to another party without revealing the information itself.
* **ZK-STARK (Zero-Knowledge Scalable Transparent Argument of Knowledge):** A type of zero-knowledge proof similar to ZK-SNARKs but designed for greater scalability and transparency.

### 12. References
1. Nakamoto, S. (2008). Bitcoin: A Peer-to-Peer Electronic Cash System. Available at: https://bitcoin.org/bitcoin.pdf
2. Buterin, V. (2013). Ethereum Whitepaper: A Next-Generation Smart Contract and Decentralized Application Platform. https://ethereum.org/en/whitepaper/
3. zkSync. (2023). ZK Stack. A framework for building custom ZK-Rollups. https://zksync.io/stack
4. OpenTimestamps. Leveraging the Bitcoin Blockchain for Timestamping. A project demonstrating the use of Bitcoin's OP_RETURN for data anchoring. https://opentimestamps.org/
5. Chainlink. Chainlink 2.0: Next Steps in the Evolution of Decentralized Oracle Networks. A whitepaper detailing the architecture of decentralized oracle networks for hybrid smart contracts. https://chain.link/whitepaper
6. EIP-4626: Tokenized Vaults. An Ethereum Improvement Proposal standardizing yield-bearing vaults. https://eips.ethereum.org/EIPS/eip-4626
7. Adams, H., Zinsmeister, N., Salem, M., Keefer, R., & Robinson, D. (2021). Uniswap v3 Core. A whitepaper detailing the concepts of concentrated liquidity. https://uniswap.org/whitepaper-v3.pdf
8. Egorov, M. (2019). StableSwap - Efficiently Swapping Stablecoins. Curve Finance whitepaper on optimized stablecoin trading. https://curve.fi/whitepaper
