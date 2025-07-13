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
  * Rewards come from [future emissions reserve](../../guide/user-guide/airdrop.md#id-1.-why-farm-hl)
  * Foundation's 250M staked HYPE does **NOT** earn rewards (tokens are unvested but can be staked)
* **Reward Distribution**
  * Rewards accrued every minute
  * Distributed to stakers daily
  * Automatically compounded (redelegated to the staked validator)
  * Validators may charge commission on rewards
* **Additional Benefits**
  * **Reduced trading fees** - staking HYPE reduces your trading fees
  * **Referral staking program** - earn from referrals
  * For more details on fee structure, see [Fees](../hypercore/dex/clearinghouse/fees.md) page

***

### HYPE Utility & Governance

#### Current Utilities

* **Gas token**: For HyperEVM transactions
* **Network security**: Through staking to validators
* **Fee reduction**: Staking reduces trading fees
* **Referral rewards**: Through the staking program
* **Governance**: Create and vote on proposals

#### Potential Future Utilities

* Revenue sharing from:
  * Trading fees (Referral staking program)
  * Spot auction fees
  * HyperEVM gas fees
* Community-driven governance decisions (**#governance** discord)

#### Governance Features

* True community-driven governance (no VC allocation)
* Voting on:
  * Listings/de-listings (already possible via the **#listing-request** and **#governance** discord)
  * Platform fees
  * CEX weights for price oracle
  * Other protocol parameters

***

### Resources <a href="#resources" id="resources"></a>

* [HYPE Genesis medium](https://hyperfnd.medium.com/hype-genesis-1830a4dc2e3f)
