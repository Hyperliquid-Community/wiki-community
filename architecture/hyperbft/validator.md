---
icon: memo-circle-check
---

# Validator

#### Becoming a Validator

* **Overview**
  * Hyperliquid has a [permissionless validator](https://hyperfnd.medium.com/hyperliquids-permissionless-validator-network-secured-by-the-community-ad0057cfad71) set
  * Anyone can register as a validator
  * Active set consists of top N validators by total stake (currently N=21, increasing over time)
  * Validators outside the active set can still register but won't produce blocks until the set expands
* **Requirements**
  * **Minimum self-delegation**: 10,000 HYPE (locked for **1 year** even if not in active set)
  * **Technical infrastructure**: Must run reliable validator nodes
  * **Compliance**: Must meet regulatory requirements if applying for [Delegation Program](https://hyperliquid.gitbook.io/hyperliquid-docs/validators/delegation-program)

#### Delegation Program

* **What is it?**\
  The Delegation Program is Hyper Foundation's initiative to [delegate foundation HYPE](https://hypurrscan.io/address/0xd57ecca444a9acb7208d286be439de12dd09de5d) to high-quality validators. This helps bootstrap new validators who might not have enough stake to enter the active set on their own. Foundation delegations can significantly boost a validator's total stake.
* **Program Objectives**
  * Enhance network security by supporting reliable validators
  * Promote decentralization and validator diversity
  * Help committed validators enter the active set
  * Establish trusted validator network
* **Eligibility Requirements**
  * **Capital**: Must have 10k HYPE in one address before applying
  * **Infrastructure**: Must run at least two non-validator nodes with 95% uptime
  * **Compliance**:
    * Complete KYC/KYB processes
    * Comply with applicable laws and regulations
    * Not from restricted jurisdictions (Ontario, U.S., Cuba, Iran, Myanmar, North Korea, Syria, certain Russian-occupied regions of Ukraine)
  * **Technical**: Static IP addresses required (e.g., elastic IPs on AWS)
* **Application Process**
  * Fill out the application form
  * Undergo application review
  * Complete KYC/KYB if invited
  * Review and accept Program Terms if accepted
* **Important Notes**
  * Testnet performance considered for mainnet delegation
  * Ongoing monitoring of delegations
  * Foundation reserves right to cease delegation at any time
  * Foundation validators consider Delegation Program participation when trusting peer validators
  * Strongly recommended to apply before setting up mainnet validator

#### Technical Details

* **Getting Started**
  * For detailed technical instructions on setting up a validator node, see the [Builder Guide - Node Operators](../../guide/builder-guide/node-operators.md) section.
* **Validator Responsibilities**
  * Produce blocks proportional to total delegated stake
  * Maintain high uptime and performance
  * Respond adequately to consensus messages
  * Secure the network through honest participation
* **Jailing Mechanism**
  * Validators can vote to jail peers with inadequate latency/frequency
  * Jailed validators don't participate in consensus or produce rewards
  * Can unjail themselves after fixing issues (subject to rate limits)
  * Jailing ≠ slashing (reserved for provably malicious behavior)
* **Consensus Details**
  * HyperBFT consensus with quorum requirement (**>2/3 of total stake**)
  * Validator set evolves in epochs of 100,000 rounds (\~90 minutes)
  * Validators and stakes static within each epoch
