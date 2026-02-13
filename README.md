# The Jubilee Protocol Whitepaper (v3)

**A Hybrid Application/Settlement Architecture for Institutional Asset Management and Permanent Provenance**

**Author**: Jubilee Labs | February 11, 2026

---

## Abstract

The Jubilee Protocol is a hybrid application/settlement architecture designed to unify Ethereum’s programmability with Bitcoin’s permanence. It operates as an institutional-grade application layer on secure, EVM-compatible Layer 2s (e.g., Base, zkSync), enabling a high-performance environment for a suite of sophisticated, yield-generating financial products. Its defining feature is a novel Settlement Layer that periodically anchors cryptographic hashes of application state to the Bitcoin blockchain via `OP_RETURN`, creating an immutable, permanent audit trail for critical data.

The protocol’s core products—jBTCi (Bitcoin Index), jETHs (Staked Ethereum Index), jSOLi (Solana Staking Index), and jUSDi (Stablecoin Index)—are automated, ERC-4626 compliant vaults that capture sustainable yield. By deploying on established L2s, Jubilee unlocks new forms of capital efficiency and provides a dual-security proposition previously unseen in the blockchain ecosystem.

The $JUBL token serves as the economic backbone, providing financial power through lending credits, revenue sharing via the Choice Yield mechanism, and governance rights within the mission-aligned Jubilee Council. This paper outlines the protocol’s architecture, products, and economic model, which are designed to provide the tools for responsible stewardship in the digital age.

---

## Table of Contents

1. **Introduction**

1. **Protocol Architecture**

1. **Core Technical Components**

1. **Core Products: The Jubilee Asset Suite**

1. **The Economic Engine: $JUBL Token**

1. **Governance: The Jubilee Council**

1. **Security and Risk Factors**

1. **Roadmap**

1. **Conclusion**

1. **Disclaimer**

1. **References**

---

## 1. Introduction

### 1.1. The Great Divide: A Foundational Opportunity

The digital asset landscape presents a significant challenge for fiduciaries and institutional stewards. The market is bifurcated into two dominant paradigms:

- **Bitcoin**: The ultimate settlement layer, offering unparalleled security, decentralization, and immutability. It is the bedrock of digital truth, but its native programmability is limited, rendering it a passive, non-yielding asset.

- **Ethereum**: The global execution layer, a vibrant ecosystem of smart contracts, decentralized finance (DeFi), and complex financial products. It offers boundless utility and yield opportunities but introduces its own set of security considerations and a fragmented, ever-evolving scaling landscape.

This division forces a **Foundational Compromise** upon institutions, particularly faith-based and non-profit organizations. They require the long-term security and permanence of Bitcoin for their endowments but need the yield and utility of Ethereum to fulfill their missions. Existing solutions, such as standalone L2s, are often fragmented, require users to adopt new security models, and lack the native privacy and compliance tools essential for managing donor-funded treasuries.

### 1.2. The Jubilee Solution: A Symbiotic Superstructure

Jubilee Protocol resolves this compromise by introducing the **Hybrid Application/Settlement Model**. Instead of building a new blockchain, Jubilee deploys its institutional-grade products as an application layer on top of battle-tested, secure L2s. This approach creates a symbiotic architecture that harmonizes the strengths of both Bitcoin and Ethereum.

> **Assets live on high-speed L2s for DeFi composability (Lending, Yield), but critical audit data is anchored to the Bitcoin L1 via ****`OP_RETURN`**** for 100-year permanence.**

This model allows Jubilee to offer the best of both worlds: the low-cost, high-speed transaction environment of L2s for active strategy management, combined with the unimpeachable audit trail of the Bitcoin blockchain for ultimate security and provenance. Our philosophy is one of **Stewardship over Speculation**, building a resilient financial ecosystem that prioritizes capital preservation, sustainable yield, and long-term value creation.

---

## 2. Protocol Architecture: A Two-Layer Stack

Jubilee’s core innovation is its hybrid, two-layered architecture that ensures scalability, security, and permanence through a clear separation of concerns. This design leverages the strengths of each underlying blockchain, creating a robust and resilient system.

### 2.1. L2: The Execution & Programmability Layer (Base, zkSync, etc.)

This is the active, high-performance environment where all user interactions, application logic, and the core financial primitives of the Jubilee Protocol reside. By deploying on established L2s, Jubilee inherits their security and liquidity, allowing the protocol to focus on product innovation.

- **EVM Compatibility**: By deploying on EVM-compatible L2s, Jubilee ensures that its smart contracts are easily auditable and composable with the broader DeFi ecosystem. Users can interact with Jubilee using familiar wallets and tools.

- **High Throughput and Low Cost**: Jubilee leverages the scalability of L2s to make complex DeFi strategies and frequent rebalancing economically viable for a broader range of users.

- **Gas Abstraction**: The protocol is designed to allow users to pay for transaction fees using the $JUBL token, abstracting away the need to hold the L2’s native gas token (e.g., ETH) for application-level interactions.

### 2.2. Multi-Chain Deployment Strategy: Independent Instances

Jubilee Protocol adopts a strategic multi-chain presence, deploying its application suite on select Layer 2s to serve distinct market segments without introducing cross-chain bridge risk. Our initial deployment targets a dual-chain architecture:

- **Base**: Serving as the primary **consumer and retail layer**. Its integration with the Coinbase ecosystem provides a low-friction onboarding experience for individual users and smaller organizations.

- **zkSync**: Serving as the primary **institutional layer**. Its native support for account abstraction and advanced privacy features makes it an ideal environment for large treasuries and organizations with complex compliance needs.

**Crucially, each deployment of a Jubilee vault (e.g., jBTCi on Base, jBTCi on zkSync) is an entirely independent and sovereign smart contract instance.** This design is a deliberate security choice.

| Aspect | Jubilee's Approach | Rationale |
| --- | --- | --- |
| **Vault Liquidity** | Fragmented by chain | **Security over Capital Efficiency**. This model completely eliminates the risk of a native bridge exploit, which has historically been a major vector for catastrophic losses in DeFi. |
| **Asset Bridging** | User-managed via third-party bridges | The protocol does not endorse or manage any specific bridge. Users are responsible for moving their assets between chains using established, battle-tested bridges of their choice. |
| **$JUBL Token** | Unified via Omnichain Fungible Token (OFT) standard | While asset vaults are independent, the $JUBL token will be seamlessly transferable across all supported chains, ensuring unified governance and utility. |

This architecture allows Jubilee to offer tailored experiences for different user bases while upholding the highest security standards by avoiding the systemic risks associated with cross-chain liquidity protocols.

### 2.3. L1: The Data Provenance & Anchor Layer (Bitcoin)

While Layer 2 handles execution and immediate throughput, the Bitcoin Layer 1 in the Jubilee architecture is strictly defined as a **Sovereign Data Anchor**, not a recursive execution environment. It uses Bitcoin's blockchain solely for data permanence and immutable archival.

- **Mechanism**: An off-chain service, the **Bitcoin L1 Anchor Service**, periodically bundles cryptographic hashes (Merkle roots) of selected L2 application state data. These Merkle roots are then embedded into a standard Bitcoin transaction via the `OP_RETURN` opcode.

- **Function**: This process creates a "Digital Notary" service. By anchoring Jubilee’s state to Bitcoin, we provide an indisputable, proof-of-work secured timestamp of the protocol’s history. This protects against data integrity issues and provides a permanent audit trail for regulatory compliance, ensuring that the historical state of assets remains verifiable via Bitcoin.

---

## 3. Core Technical Components

Jubilee Protocol is built upon a foundation of robust and battle-tested smart contract standards and security practices.

### 3.1. ERC-4626 Tokenized Vault Standard

All of Jubilee’s core products are built as ERC-4626 compliant tokenized vaults. This standard, pioneered by Yearn Finance, provides a unified API for yield-bearing vaults, ensuring composability, security, and ease of integration across the DeFi ecosystem. By adhering to this standard, Jubilee vaults can be easily integrated into other protocols, aggregators, and institutional dashboards.

### 3.2. Oracle Security: A Dual-Oracle System

To ensure accurate and manipulation-resistant pricing for lending and rebalancing operations, Jubilee employs a dual-oracle system:

1. **Primary Oracle**: Chainlink’s industry-leading, decentralized price feeds provide real-time asset prices.

1. **Validation Oracle**: A Time-Weighted Average Price (TWAP) oracle, calculated from high-liquidity DEXs on the respective L2, is used to validate Chainlink’s prices. If the deviation between the two oracles exceeds a predefined threshold (e.g., 2%), the system can pause operations to prevent exploits.

### 3.3. ZK-Account Abstraction

To enhance usability for non-technical institutional users, Jubilee integrates ZK-Account Abstraction. This allows users to interact with the protocol using modern authentication methods like FaceID and Passkeys instead of managing complex seed phrases. This significantly lowers the barrier to entry and improves security for organizations.

### 3.4. The Rebalancing Engine

The Rebalancing Engine is the core intelligence behind the jBTCi, jETHs, and jUSDi index products. It is a sophisticated, automated system designed to identify and execute profitable arbitrage opportunities within the specified asset baskets, transforming passive indexes into actively managed, yield-generating vaults.

- **Off-Chain Analysis & On-Chain Execution**: An off-chain component continuously monitors markets on high-liquidity DEXs (e.g., Uniswap v3, Curve) to identify arbitrage opportunities. Once an opportunity is found, it initiates an on-chain transaction. To prevent front-running, the engine employs MEV protection strategies and includes an atomic on-chain check that reverts the transaction if it is not profitable after all costs.

- **External DEX Execution**: The Rebalancing Engine executes trades on external decentralized exchanges where deep liquidity exists. This is critical because arbitrage opportunities are a function of market depth and volume.

- **Long-Term Strategy: Beyond Arbitrage**: While the engine is designed to capture arbitrage profits, its primary long-term value is **sophisticated index health and risk management**. As markets become more efficient, its function will evolve into a liquidity balancing tool. By systematically selling the over-weighted asset and buying the under-weighted one, the engine actively helps maintain the peg of all constituent assets, providing a stabilizing public good to the ecosystem.

### 3.5. Multi-Signature Governance & Timelocks

All administrative functions and protocol upgrades are controlled by a multi-signature wallet, initially managed by the Jubilee Council. Any proposed change requires a majority of signers to approve and is subject to a **24-hour timelock** before it can be executed. This provides transparency and gives the community time to review and react to any proposed changes.

---

## 4. Core Products: The Jubilee Asset Suite

Jubilee’s core products are a suite of automated, yield-generating index vaults designed to meet the specific needs of institutional and faith-based treasuries.

### 4.1. jBTCi: The Bitcoin Yield Index

- **Status**: Live on Base Mainnet

- **Thesis**: Systematically captures arbitrage profits from the price deviations between different wrapped Bitcoin assets (e.g., WBTC, cbBTC) on L2s.

- **Value Proposition**: Transforms passive Bitcoin holdings into a productive, yield-generating asset while maintaining diversified exposure to the Bitcoin ecosystem.

### 4.2. jETHs: The Liquid Staking Index

- **Status**: Live on Ethereum Testnet

- **Thesis**: Optimizes yield by diversifying across a basket of top-tier Ethereum Liquid Staking Tokens (LSTs) like wstETH, cbETH, and rETH.

- **Value Proposition**: Provides broad, decentralized exposure to Ethereum staking rewards while generating additional alpha through automated rebalancing and arbitrage.

### 4.3. jSOLi: The Solana Staking Index

- **Status**: Live on Solana Devnet

- **Thesis**: Aggregates and optimizes yield from Solana's leading LST protocols, including Jito, Marinade, and BlazeStake.

- **Value Proposition**: Offers a simple, one-click solution to access the high-yield opportunities within the Solana staking ecosystem, including MEV rewards.

### 4.4. jUSDi: The Stablecoin Yield Index

- **Status**: Multi-chain deployment (Live on Base)

- **Thesis**: Functions as the "risk-free rate" for on-chain treasuries by generating sustainable yield from a diversified basket of the most secure and liquid USD-pegged stablecoins.

- **Value Proposition**: Provides a stable, reliable source of yield for institutional cash management, minimizing single-issuer risk and capturing micro-arbitrage from peg deviations.

### 4.5. Jubilee Lending (Roadmap)

- **Status**: In Development

- **Thesis**: A non-custodial, over-collateralized lending protocol that allows users to borrow jUSDi against their yield-bearing index tokens (jBTCi, jETHs, jSOLi).

- **Value Proposition**: Unlocks liquidity for institutional treasuries, allowing them to access working capital without selling their strategic positions. The protocol is designed for capital efficiency, with LTV ratios directly influenced by $JUBL staking.

#### 4.5.1. Lending Mechanics: Yield-Backed Borrowing

Jubilee Lending introduces a novel, self-repaying loan model. Instead of borrowers paying interest, the yield generated by their deposited collateral (e.g., the arbitrage profits from jBTCi) is automatically used to pay down the loan principal.

- **Collateral Assets**: jBTCi, jETHs, jSOLi

- **Borrow Asset**: jUSDi

- **Interest Model**: 0% interest. The only cost to the borrower is the opportunity cost of the yield from their collateral, which is used for repayment.

**Example**: A church deposits $1,000,000 in jBTCi (generating 6% net APY) and borrows $500,000 in jUSDi for a building expansion. The jBTCi generates $60,000 in yield per year, which is automatically applied to the loan principal. The loan is fully repaid in approximately 8.3 years from the collateral's yield alone, and the church retains its full exposure to Bitcoin.

#### 4.5.2. The Role of $JUBL: LTV Boosts

The primary utility of the $JUBL token within the lending protocol is to serve as a **capital efficiency tool**, allowing borrowers to increase their Loan-to-Value (LTV) ratio.

- **Base LTV**: 50% for all collateral types.

- **Boost Mechanism**: For every $1 worth of $JUBL staked in the lending contract, the user's borrowing capacity increases by $1.

- **Maximum Boost**: Users can increase their LTV by up to +20% (to a maximum of 70% LTV).

**Formula**: `Effective LTV = Base LTV + (Value of Staked $JUBL / Value of Collateral)`

**Example**:

- **Without $JUBL**: Deposit $1M of jBTCi → Borrow up to $500,000 of jUSDi (50% LTV).

- **With $JUBL**: Deposit $1M of jBTCi + Stake $200,000 worth of $JUBL → Borrow up to $700,000 of jUSDi (70% LTV).

This creates a powerful incentive for institutions to acquire and stake $JUBL, as it directly unlocks additional liquidity and improves their capital efficiency.

#### 4.5.3. Risk Parameters & Liquidations

To protect the protocol from insolvency, a clear set of risk parameters is enforced.

| Parameter | Value | Description |
| --- | --- | --- |
| **Base LTV** | 50% | The initial borrowing power a user has against their collateral. |
| **Max LTV (with Boost)** | 70% | The maximum borrowing power achievable by staking $JUBL. |
| **Liquidation Threshold** | 80% | If the value of the debt rises to 80% of the collateral's value, the position is eligible for liquidation. |
| **Liquidation Penalty** | 5% | A 5% fee is applied to the liquidated collateral, which is used to reward liquidators and the protocol treasury. |

If a user's Health Factor (the ratio of collateral value to debt value) falls below the liquidation threshold, a portion of their collateral is sold on the open market to repay the debt and restore the position to health.

---

## 5. The Economic Engine: $JUBL Token

The $JUBL token is the economic engine of the Jubilee Protocol, designed to align incentives and empower stakeholders. Its utility model is focused on providing **Financial Power and Governance Rights**.

- **Total Supply**: 1,000,000,000 $JUBL (Fixed)

### 5.2. Token Allocation

The allocation of the $JUBL token is designed to foster long-term, sustainable growth and align the incentives of all stakeholders, from the community to the core team.

| Category | Percentage | Tokens | Vesting Schedule | Rationale |
| --- | --- | --- | --- | --- |
| **Community & Ecosystem** | 40% | 400,000,000 | 4-5 years (linear) | To bootstrap liquidity, incentivize early adopters through yield farming, fund ecosystem grants via the Hundredfold Grant Program, and support community initiatives. |
| **Staking Rewards** | 25% | 250,000,000 | 5+ years (logarithmic) | To incentivize participation in governance via the Jubilee Council and to reward users who stake $JUBL to enhance their capital efficiency in Jubilee Lending. |
| **Foundation & Core Team** | 20% | 200,000,000 | 1-year cliff, 3-year linear | To compensate the founding team and core contributors at Jubilee Labs for their long-term commitment to building and maintaining the protocol. |
| **Private Investors** | 10% | 100,000,000 | 1-year cliff, 2-year linear | To provide the necessary capital for initial development, security audits, legal structuring, and go-to-market operations. |
| **Public Liquidity** | 5% | 50,000,000 | 100% Unlocked at TGE | To facilitate the initial public distribution of the token and provide immediate, deep liquidity on decentralized exchanges upon launch. |

- **Emission Schedule**: Staking rewards (25% of supply) are distributed on a logarithmic decay schedule, with emissions halving each year for the first 4-5 years to reward early participants most heavily.

### 5.1. Revenue Model & Value Accrual

The Jubilee Protocol is designed with a sustainable economic engine that captures value from its financial products and distributes it to $JUBL token holders. The revenue model is based on standard institutional asset management fees.

#### Fee Structure

| Fee Type | Rate | Description |
| --- | --- | --- |
| **Index Management Fee** | 0.5% - 1.0% | An annual fee charged on the Assets Under Management (AUM) in the index vaults (jBTCi, jETHs, etc.). |
| **Index Performance Fee** | 10% - 20% | A fee charged on the gross arbitrage profits generated by the Rebalancing Engine. This aligns protocol incentives with depositor success. |
| **Lending Origination Fee** | 0.5% | A one-time fee charged on the borrowed amount when a new loan is initiated in Jubilee Lending. |
| **Lending Liquidation Fee** | 2.0% | A portion of the 5% liquidation penalty that is directed to the protocol treasury. |

#### Value Accrual to $JUBL

The flow of value begins with the **First Fruits Tithe**, a foundational principle of the protocol's economic model.

#### The First Fruits Tithe

Before any revenue is distributed to token holders or the treasury, **10% of all gross protocol revenue** is automatically tithed to the **First Fruits Fund**. This fund is a dedicated, on-chain treasury governed by the Jubilee Council, with the sole purpose of supporting whitelisted charitable organizations and faith-based initiatives.

This mechanism ensures that the protocol's growth is intrinsically linked to real-world impact, embedding missional alignment at the core of the economic engine.

The remaining 90% of protocol revenue then flows to the **Jubilee Treasury**, which is governed by the Jubilee Council. This revenue is then distributed to $JUBL stakers via the **Choice Yield** mechanism. This system allows $JUBL stakers to not only receive a share of the protocol's revenue but also to direct a portion of the yield to whitelisted charitable organizations, creating a powerful alignment of financial incentives and missional impact.

### 5.3. Choice Yield: Technical Implementation

The Choice Yield mechanism is the system through which protocol revenue is distributed to $JUBL stakers. It is designed for transparency, efficiency, and user choice.

- **Revenue Collection**: All protocol revenue (the 90% remaining after the First Fruits Tithe) flows to a single `FeeCollector.sol` smart contract. All fees collected in jUSDi are automatically swapped to jBTCi and jETHs at market rates, ensuring stakers receive rewards in the protocol's primary productive assets.

- **Distribution Mechanism**: A `ChoiceYieldDistributor.sol` contract calculates each staker's pro-rata share of the revenue based on the amount of $JUBL they have staked. The distribution formula is as follows:

   > `User's Pending Rewards = (Total Distributable Revenue × User's Staked $JUBL) / Total Staked $JUBL`

- **Claiming Options**: Users can call a `claimRewards()` function to receive their share. They have the flexibility to claim their rewards in jBTCi, jETHs, or a proportional mix of both.

- **Gas Optimization**: To minimize gas costs for small holders, rewards accrue passively without requiring any user action, and claims are processed based on periodic snapshots of staked balances.

##### 5.4. Core Utilities

The $JUBL token is designed with a multi-faceted utility model that integrates it deeply into the protocol's operations, creating a sustainable economic flywheel.

| Utility               | Description                                                                                                                                                                                                                                                        |
| :-------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Lending Credits**   | **(Primary Financial Utility)** Staking $JUBL directly increases a user's borrowing capacity (LTV) in Jubilee Lending, transforming the token into a capital efficiency tool. This is the core driver of institutional demand.                               |
| **Governance Rights** | **(Primary Control Utility)** A significant stake of $JUBL is required to join the Jubilee Council, granting verified organizations a vote in protocol governance. This ensures that those who control the protocol are economically aligned with its success. | 
| **Revenue Share**     | **(Primary Economic Utility)** Staked $JUBL tokens receive a pro-rata share of the protocol's revenue (90% of gross revenue after the First Fruits tithe) through the Choice Yield mechanism, making it a productive, yield-bearing asset.                |
| **Gas Abstraction**   | **(Secondary UX Utility)** $JUBL can be used to pay for gas fees on the application layer, abstracting away the need for users to hold the L2's native gas token (e.g., ETH) for routine interactions with Jubilee's smart contracts.                               |s.

---

## 6. Governance: The Jubilee Council

Governance of the Jubilee Protocol is stewarded by the **Jubilee Council**, a mission-aligned body composed of high-tier stakers, including verified faith-based organizations, non-profits, and core contributors. The Council is responsible for the strategic direction and risk management of the protocol.

The Council is founded on principles of long-term stewardship, transparency, and mission-alignment, ensuring the protocol serves its community with integrity.

### 6.1. Council Composition

The Jubilee Council is composed of verified, Bible-believing Christian churches and mission-aligned non-profit organizations. This model creates a stable, values-driven governance layer.

- **Verification Process**: The Hundredfold Foundation manages a robust 'Know Your Organization' (KYO) process to verify the legal identity, non-profit status, and operational history of each applicant.

- **Staking Requirement**: Each verified organization is required to stake a significant amount of $JUBL tokens to activate and maintain its voting power. This creates economic alignment and attack resistance.

- **Voting Power**: Critically, each verified organization receives **one equal vote** regardless of the amount of $JUBL staked above the minimum requirement. This prevents plutocracy and ensures that governance is driven by a council of peers.

### 6.2. Responsibilities

- **Product Governance**: The Council oversees the composition of the index vaults (jBTCi, jETHs, jSOLi), setting risk parameters and approving the inclusion of new assets.

- **Risk Management**: Manages protocol-wide risk parameters, including collateralization ratios for Jubilee Lending and the configuration of security modules.

- **Treasury Management**: Governs the protocol treasury and the allocation of the "First Fruits" tithe, a portion of protocol revenue directed to whitelisted charitable organizations.

- **Upgrades**: Approves all major smart contract upgrades and protocol enhancements through a time-locked, on-chain voting process.

---

## 7. Security and Risk Factors

Security is the cornerstone of the Jubilee Protocol. Our approach is multi-layered, combining battle-tested code, rigorous auditing, and economic incentives to protect user funds.

- **Audits**: All core contracts have achieved a **92/100 audit score** and have undergone comprehensive testing, including stress tests and fuzz testing. We are committed to continuous audits for all new products and major upgrades.

- **Inherited Security**: By deploying on established L2s like Base and zkSync, Jubilee inherits the security of their underlying infrastructure, which has been battle-tested with billions of dollars in value.

- **Elimination of Bridge Risk**: By design, the protocol does not operate its own cross-chain asset bridge. Vaults on different chains are independent instances, which completely removes the risk of a native bridge exploit, a common and catastrophic failure point in DeFi.

- **ERC-4626 Standard**: By building on a widely adopted standard, we reduce smart contract risk and benefit from the extensive auditing and community review of the standard itself.

- **Circuit Breakers**: Automated safety mechanisms are built into each vault to pause operations in the event of extreme market volatility or detected exploits.

- **FASB Compliance**: Our user-facing dashboards provide the necessary reporting tools for institutions to comply with **FASB ASU 2023-08**, including fair value calculations and CSV exports.

---

## 8. Roadmap

Jubilee Protocol is being developed and deployed in a phased approach, prioritizing security and user feedback.

### Live Now

- **jBTCi**: Live on Base Mainnet

- **jETHs**: Live on Ethereum Sepolia Testnet

- **jSOLi**: Live on Solana Devnet

- **jUSDi**: Live on Base Mainnet

- **Institutional Dashboard**: FASB-compliant reporting and Safe multi-sig integration.

### In Development (2026-2027)

- **Jubilee Lending**: Over-collateralized lending protocol.

- **$JUBL Token**: TGE and integration of staking utilities.

- **Bitcoin L1 Anchor**: Activation of the Settlement Service for permanent data provenance.

- **Choice Yield**: Implementation of the gauge voting system for yield direction.

- **ZK-Account Abstraction**: Rollout of passkey and FaceID authentication.

---

## 9. Conclusion

Jubilee Protocol represents a paradigm shift in decentralized finance, moving beyond pure speculation to build a sustainable ecosystem for long-term stewardship. By harmonizing the security of Bitcoin with the utility of Ethereum, we provide institutions with the tools they need to navigate the digital economy responsibly. Our Hybrid Application/Settlement Model, institutional-grade security, and faith-aligned governance create a resilient foundation for the future of finance—a future where capital is not only efficient but also purposeful.

---

## 10. Disclaimer

This whitepaper is for informational purposes only and does not constitute an offer to sell or a solicitation of an offer to buy any securities or tokens. The Jubilee Protocol is under continuous development, and its features are subject to change. Participating in DeFi carries inherent risks, including but not limited to smart contract vulnerabilities and market volatility. Please conduct your own due diligence.

---

## 11. References

1. Financial Accounting Standards Board (FASB). (2023). *Accounting Standards Update 2023-08: Accounting for and Disclosure of Crypto Assets*. [https://www.fasb.org/page/Document?pdf=ASU%202023-08.pdf](https://www.fasb.org/page/Document?pdf=ASU%202023-08.pdf) 

1. Ethereum Improvement Proposals. (2022). *EIP-4626: Tokenized Vaults*. [https://eips.ethereum.org/EIPS/eip-4626](https://eips.ethereum.org/EIPS/eip-4626) 

1. Nakamoto, S. (2008). *Bitcoin: A Peer-to-Peer Electronic Cash System*. [https://bitcoin.org/bitcoin.pdf](https://bitcoin.org/bitcoin.pdf) 
