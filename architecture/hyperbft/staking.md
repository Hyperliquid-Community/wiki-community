---
icon: layer-group
---

# Staking

HYPE staking on Hyperliquid happens within HyperCore. Users can stake their HYPE tokens to validators to help secure the network and earn rewards.

#### How Staking Works

* **Account Management**
  * HYPE can be transferred between spot and staking accounts
  * Transfers from spot to staking account are **instant**
  * Transfers from staking to spot account have a **7-day unstaking queue**
  * You can [link](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees#staking-linking) a staking wallet to a trading wallet to benefit from fee reductions (permanent action)
* **Delegation Process**
  * Users can stake (delegate) HYPE to any number of validators
  * Each delegation has a **1-day lockup** period
  * After lockup, delegations can be partially or fully undelegated at any time
  * Undelegated balances **instantly** reflect in staking account balance
* **Validator Selection**
  * View the[ list of all validators](https://app.hyperliquid.xyz/staking) with their performance metrics
  * Active validator set consists of top N validators by total stake
  * Consider validator commission rates (cannot be increased above 1% once set)
  * Check validator uptime and reliability metrics, consult the [asxn dashboard](https://data.asxn.xyz/dashboard/hype-staking) for a detailed statistics.

#### Staking Rewards

* **APR and Reward Rate**
  * Reward rate is **inversely proportional** to the square root of total HYPE staked
  * At 400M total HYPE staked, yearly reward rate is approximately **2.37%**
  * Rewards come from future emissions reserve
  * Foundation's 250M staked HYPE does **NOT** earn rewards (tokens are unvested but can be staked)
* **Reward Distribution**
  * Rewards accrued every minute
  * Distributed to stakers daily
  * Automatically compounded (redelegated to the staked validator)
  * Validators may charge commission on rewards
* **Additional Benefits**
  * **Reduced trading fees** - staking HYPE reduces your trading fees
  * **Referral staking program** - earn from referrals
  * For more details on fee structure, see [Fees](../hypercore/dex/clearinghouse/fees-builder-codes.md) page

***

### HYPE Utility & Governance

#### Tokenomics

* **Total Supply:** 1,000,000,000 [HYPE tokens](https://app.hyperliquid.xyz/explorer/token/0x0d01dc56dcaaca66ad901c959b4011ec)
* **Current Circulating Supply:** \~333M HYPE
  * 310M: genesis distribution (only \~270m claimed)
  * 60M: Hyper Foundation budget
  * 3M: community grants
  * 120K: HIP-2
* **Team Allocation (Core Contributors):** 238M tokens with cliff ending November 28, 2025, followed by [2-4 year vesting](https://tokenomist.ai/hyperliquid). Track the core contributors' address on [Hypurrscan](https://hypurrscan.io/address/0x43e9abea1910387c4292bca4b94de81462f8a251).
* **Future Community Rewards:** \~430M tokens reserved for ongoing distributions and ecosystem growth
  * Distribution methods beyond the 2.2% staking rewards remain unannounced
* [HYPE Genesis medium](https://hyperfnd.medium.com/hype-genesis-1830a4dc2e3f) | [Current distribution](https://www.hypeburn.fun/)

#### Current Utilities

* **Gas token**: For HyperEVM transactions
* **Network security**: Through staking to validators
* **Fee reduction**: Staking reduces trading fees
* **Referral rewards**: Through the staking referral program
* **Governance**: Create and vote on proposals

#### Governance Features

* True community-driven governance (no VC allocation)
* Voting on:
  * Listings/de-listings (already possible via the **#listing-request** and **#governance** discord)
  * Platform fees
  * CEX weights for price oracle
  * Other protocol parameters
