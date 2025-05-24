---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Fees

Hyperliquid's fee system is designed to reward active users, builders, and the broader community. By leveraging volume-based discounts, staking incentives, and referral programs, the platform ensures that participation benefits users while funding the ecosystem's development.

### Fee Structure Overview

| Category               | Method                                                                        | Benefit                        | Details                                                                                 |
| ---------------------- | ----------------------------------------------------------------------------- | ------------------------------ | --------------------------------------------------------------------------------------- |
| **User Fee Reduction** | [VIP Tiers](fees.md#fee-schedule-vip--staking-tiers) (Volume-Based)           | Up to 47% discount             | Based on rolling 14-day weighted volume                                                 |
|                        | Staking Tiers                                                                 | Up to 40% discount             | Based on HYPE tokens staked                                                             |
|                        | Referral Discount                                                             | 4% discount                    | For first $25M volume when using referral code                                          |
| **User Fee Rewards**   | Referral Rewards                                                              | 10% of referred users' fees    | For first $1B volume of referred users                                                  |
|                        | [Staking Referral Program](fees.md#staking-referral-program)                  | 40% to 100% of fees difference | _Coming soon_ - Enhanced rewards for staking referrers (depends on referred user's VIP) |
|                        | Staking Referral Sharing                                                      | Up to 50% revenue sharing      | _Coming soon_ - Can share staking referral revenue with referred users                  |
|                        | Builder Codes                                                                 | 100% custom fee + 40% to 100%  | Builder fee + staking referral rewards if staking HYPE                                  |
|                        | Maker Rebates                                                                 | Up to -0.003% rebate           | Continuous rebates for market makers                                                    |
| **Community Benefits** | [HLP Vault](../../vault.md#id-1.-protocol-vaults-hyperliquidity-provider-hlp) | Liquidity incentives           | Fees fund liquidity provision rewards                                                   |
|                        | Assurance Fund                                                                | fees reinvested                | Ecosystem protection and HYPE buybacks                                                  |

**Please note:**

* **Volume Calculation:** Fees based on rolling 14-day weighted volume: `(14d perps volume) + 2 × (14d spot volume)`
* **Sub-Accounts:** Volume from sub-accounts counts toward master account's fee tier; all sub-accounts share the same tier
* **Vault Volume:** Vault transactions treated separately from master account
* **Referral Limits:**
  * Referral discounts apply for first $25M in volume
  * Referral rewards apply for first $1B in volume
  * Discounts don't apply to vaults or sub-accounts
* **Builder Codes:** Staking referral program also applies to builder codes (more info on this [page](../../../../guide/builder-guide/hypercore/)). Builders receive builder fee + up to 40% of HL fees and can share up to 50% of these fees with users
* **Fee Assessment:** Calculated at end of each day in UTC

***

### **Fee Distribution & Sources**

On Hyperliquid, **fees are entirely directed to the community** through HLP, the Assistance Fund, and spot/perp deployers rather than being extracted by the protocol team.

**Current Fee Allocation:**

* **7% of fees** → HLP vault
* **93% of fees** → Assistance Fund
* **Fee Tracking:** Direct fee visibility is limited - estimates based on trading volume. Analytics: [HyperDash](https://hyperdash.info/statistics) | [HypurrScan](https://hypurrscan.io/dashboard)

**Fee Sources:**

* **Perpetual trading:**
  * **Hyperliquid Labs perps:** All fees go to protocol
  * **HIP-3 perps:** Up to 50% of fees go to deployer, remainder to protocol
* **Spot trading:**
  * **USDC side (bid):** Fees go to protocol
  * **Token side (ask):** Deployer controls what percentage of fees they collect (0-100%)
    * If 100% → All fees go to deployer's address
    * If 0% → All fees are burned
    * Deployers can only decrease their share permanently
    * Tokens deployed before January 2025 have all fees burned (including [HYPE](https://data.asxn.xyz/dashboard/hype-burn))
    * To check a token's fee share: Call API `spotMetaAndAssetCtxs` → `deployerTradingFeeShare`
* **Spot deployment:** [Auction fees](../../hips/spot-deployments-hip-1-hip-2.md#what-is-hip-1) paid by deployers to purchase tickers
* **Future:** HyperEVM fees may be distributed to HYPE stakers

***

### Fee Tiers&#x20;

You can view your current fee tier on your [portfolio page](https://app.hyperliquid.xyz/portfolio) which includes an integrated fee schedule calculator.

#### Staking Tiers

| Tier     | HYPE Staked | Trading Fee Discount |
| -------- | ----------- | -------------------- |
| Wood     | >10         | 5%                   |
| Bronze   | >100        | 10%                  |
| Silver   | >1,000      | 15%                  |
| Gold     | >10,000     | 20%                  |
| Platinum | >100,000    | 30%                  |
| Diamond  | >500,000    | 40%                  |

#### Fee Schedule (VIP + **Staking Tiers)**

| Perp  | VIP                     | Base Rate       | Diamond           | Platinum          | Gold              | Silver            | Bronze            | Wood              |
| ----- | ----------------------- | --------------- | ----------------- | ----------------- | ----------------- | ----------------- | ----------------- | ----------------- |
| Tier  | 14d Weighted Volume ($) | Taker/Maker     | Taker/Maker       | Taker/Maker       | Taker/Maker       | Taker/Maker       | Taker/Maker       | Taker/Maker       |
| **0** |                         | 0.045% / 0.015% | 0.0270% / 0.0090% | 0.0315% / 0.0105% | 0.0360% / 0.0120% | 0.0383% / 0.0128% | 0.0405% / 0.0135% | 0.0428% / 0.0143% |
| **1** | >5M                     | 0.040% / 0.012% | 0.0240% / 0.0072% | 0.0280% / 0.0084% | 0.0320% / 0.0096% | 0.0340% / 0.0102% | 0.0360% / 0.0108% | 0.0380% / 0.0114% |
| **2** | >25M                    | 0.035% / 0.008% | 0.0210% / 0.0048% | 0.0245% / 0.0056% | 0.0280% / 0.0064% | 0.0298% / 0.0068% | 0.0315% / 0.0072% | 0.0333% / 0.0076% |
| **3** | >100M                   | 0.030% / 0.004% | 0.0180% / 0.0024% | 0.0210% / 0.0028% | 0.0240% / 0.0032% | 0.0255% / 0.0034% | 0.0270% / 0.0036% | 0.0285% / 0.0038% |
| **4** | >500M                   | 0.028% / 0.000% | 0.0168% / 0.0000% | 0.0196% / 0.0000% | 0.0224% / 0.0000% | 0.0238% / 0.0000% | 0.0252% / 0.0000% | 0.0266% / 0.0000% |
| **5** | >2B                     | 0.026% / 0.000% | 0.0156% / 0.0000% | 0.0182% / 0.0000% | 0.0208% / 0.0000% | 0.0221% / 0.0000% | 0.0234% / 0.0000% | 0.0247% / 0.0000% |
| **6** | >7B                     | 0.024% / 0.000% | 0.0144% / 0.0000% | 0.0168% / 0.0000% | 0.0192% / 0.0000% | 0.0204% / 0.0000% | 0.0216% / 0.0000% | 0.0228% / 0.0000% |

| Spot  | VIP                     | Base Rate       | Diamond           | Platinum          | Gold              | Silver            | Bronze            | Wood              |
| ----- | ----------------------- | --------------- | ----------------- | ----------------- | ----------------- | ----------------- | ----------------- | ----------------- |
| Tier  | 14d Weighted Volume ($) | Taker/Maker     | Taker/Maker       | Taker/Maker       | Taker/Maker       | Taker/Maker       | Taker/Maker       | Taker/Maker       |
| **0** |                         | 0.070% / 0.040% | 0.0420% / 0.0240% | 0.0490% / 0.0280% | 0.0560% / 0.0320% | 0.0595% / 0.0340% | 0.0630% / 0.0360% | 0.0665% / 0.0380% |
| **1** | >5M                     | 0.060% / 0.030% | 0.0360% / 0.0180% | 0.0420% / 0.0210% | 0.0480% / 0.0240% | 0.0510% / 0.0255% | 0.0540% / 0.0270% | 0.0570% / 0.0285% |
| **2** | >25M                    | 0.050% / 0.020% | 0.0300% / 0.0120% | 0.0350% / 0.0140% | 0.0400% / 0.0160% | 0.0425% / 0.0170% | 0.0450% / 0.0180% | 0.0475% / 0.0190% |
| **3** | >100M                   | 0.040% / 0.010% | 0.0240% / 0.0060% | 0.0280% / 0.0070% | 0.0320% / 0.0080% | 0.0340% / 0.0085% | 0.0360% / 0.0090% | 0.0380% / 0.0095% |
| **4** | >500M                   | 0.035% / 0.000% | 0.0210% / 0.0000% | 0.0245% / 0.0000% | 0.0280% / 0.0000% | 0.0298% / 0.0000% | 0.0315% / 0.0000% | 0.0333% / 0.0000% |
| **5** | >2B                     | 0.030% / 0.000% | 0.0180% / 0.0000% | 0.0210% / 0.0000% | 0.0240% / 0.0000% | 0.0255% / 0.0000% | 0.0270% / 0.0000% | 0.0285% / 0.0000% |
| **6** | >7B                     | 0.025% / 0.000% | 0.0150% / 0.0000% | 0.0175% / 0.0000% | 0.0200% / 0.0000% | 0.0213% / 0.0000% | 0.0225% / 0.0000% | 0.0238% / 0.0000% |

#### Market Maker Tiers

Market makers benefit from lower fees through a dedicated tier system that rewards high liquidity providers. Hyperliquid offers no special programs or rebates, **anyone can participate**. Tools and support: [Python SDK](https://github.com/hyperliquid-dex/hyperliquid-python-sdk) | [#api-traders Discord](https://discord.gg/hyperliquid).

| Tier | 14d Weighted Maker Volume | Maker Fee Rebate |
| ---- | ------------------------- | ---------------- |
| 1    | >0.5%                     | -0.001%          |
| 2    | >1.5%                     | -0.002%          |
| 3    | >3.0%                     | -0.003%          |

***

### Referral Program

#### Standard Referral Program

**How to Refer:**

* Complete $10,000 in trading volume to create your referral code at [Hyperliquid Referrals](https://app.hyperliquid.xyz/referrals)
* Share your unique link: `https://app.hyperliquid.xyz/join/YOURCODE`

**Benefits:**

* **Referrers Earn:** 10% of referred users' fees (for first $1B volume)
* **Referred Users Get:** 4% fee discount (for first $25M volume)

#### Staking Referral Program

_Coming soon_ - The staking referral program allows builders and referrers who stake HYPE to earn enhanced rewards based on the **difference between their staking tier discount and their referred user's discount**.

**Key Mechanism:**

* If a referrer has a higher staking tier than their referred user, they can keep a percentage of the staking discount difference
* The percentage kept decreases as the referred user's VIP tier increases (higher VIP = lower earnings for referrer)

| VIP Tier | 14d Weighted Volume ($) | Amount Kept by Referrer |
| -------- | ----------------------- | ----------------------- |
| **0**    |                         | 100%                    |
| **1**    | >5M                     | 90%                     |
| **2**    | >25M                    | 80%                     |
| **3**    | >100M                   | 70%                     |
| **4**    | >500M                   | 60%                     |
| **5**    | >2B                     | 50%                     |
| **6**    | >7B                     | 40%                     |

**Example:** Alice stakes 100K HYPE (Diamond tier = 30% discount) and refers Bob who stakes 100 HYPE (Bronze tier = 10% discount). Bob is VIP 1 (90% rate).

* **Staking discount difference:** 30% - 10% = 20%
* **Alice keeps:** 20% × 90% = 18% of Bob's fees
* **Alice can share back:** Up to 50% of her 18% = 9% discount for Bob
* **Result:** Bob gets up to 9% additional discount using Alice's referral code

***

### Resources

* Official documentation on [Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees) and [Referrals](https://hyperliquid.gitbook.io/hyperliquid-docs/referrals).
* [Fee Calculator](https://app.hyperbeat.org/dapp/calculator): You can determine the number of fees you pay in different situations. [@0xHyperBeat](https://x.com/0xHyperBeat/status/1902396341520675060)
