---
icon: brake-warning
---

# Incident

Hyperliquid maintains transparency about platform incidents and their resolution. When technical issues or system irregularities occur that impact users, the platform has established protocols to address affected parties fairly.

The **Assurance Fund** (previously called Insurance Fund) serves as Hyperliquid's primary mechanism for compensating users affected by platform-related incidents. This governance-controlled fund reimburses users when issues stem from technical problems, system congestion, or other platform-specific challenges rather than normal market conditions.

While Hyperliquid carries [inherent risks](https://hyperliquid.gitbook.io/hyperliquid-docs/risks), the fund operates on the principle that users should not bear losses caused by platform malfunctions or design limitations during the protocol's development phase. For detailed information about how the fund operates, see the [Vault](../../../architecture/hypercore/vault.md#id-2.-protocol-vaults-assistance-fund-af) page and the [Risk Dashboard](https://data.asxn.xyz/dashboard/hl-risk-metrics) for real-time risk metrics.

***

### Incident History

[July 29, 2025](https://x.com/Sakrexer/status/1950552205305815398)

* **Description:** API servers experienced significant traffic spike causing order delays from 14:10-14:47 UTC during record-breaking trading activity. API returned error responses despite transactions being sent to mempool and included in blocks, confusing users who didn't realize their orders were executed
* **Response:** [Automated refund](https://x.com/pana067/status/1952295385713541318) methodology implemented for affected users: (1) Users with <$10k PnL during incident period received favorable mark price calculations from 30-minute window afterward, (2) Funding rate compensation for assets with >40x larger rates (kBONK, CFX, MKR, MOODENG, NXPC, RESOLV, VINE), (3) KYB/KYC process for users receiving ≥$10k refunds
* **Outcome:** No blockchain compromise - consensus and HyperEVM unaffected, blocks produced normally. API infrastructure improvements in development.

[March 26, 2025](https://x.com/HyperliquidX/status/1905319339991204263)

* **Description:** Attack on JELLY perps involving self-trading 4M USDC position at low price, then pumping spot price 400%+ to force HLP backstop liquidation of toxic short position, with potential coordination from major CEXs
* **Response:** JELLY long traders refunded by Foundation at advantageous settlement price (0.037555). HLP Liquidator vault capped to small percentage of total balance, refined OI caps based on market cap, onchain validator voting for delistings implemented
* **Outcome:** HLP significant losses contained, platform solvency maintained through enhanced risk management. [Full incident analysis](2025-26-03.md)

[March 12, 2025](https://x.com/threesigmaxyz/status/1899798137000145067)

* **Description:** Trader opened $271M ETH long position with 50x leverage using $6M collateral, then strategically withdrew funds to force liquidation while hedging short on external exchange, exploiting liquidation mechanics rather than technical vulnerabilities
* **Response:** Max leverage reduced to 40x (BTC) and 25x (ETH). Additional 20% margin ratio requirement [implemented](https://x.com/HyperliquidX/status/1900199063880171578) on margin transfers to directly address the withdrawal-based liquidation strategy
* **Outcome:** $4M HLP loss (approximately one month's profit), no Assurance Fund compensation as system operated as designed - mechanism exploit rather than platform malfunction

[June 21, 2024](https://discord.com/channels/1029781241702129716/1030197017655394447/1253396026753028138)

* **Description:** ZRO-USD hyperp settlement used erroneous mark price, causing incorrect negative P\&L for short position holders
* **Response:** Automatic refunds issued from Assurance Fund to all affected users, calculated as position value before erroneous update minus account value after update, plus 2% buffer to account for different valuation methodologies
* **Outcome:** Complete compensation for impacted traders with conservative buffer applied

[March 1, 2024](https://discord.com/channels/1029781241702129716/1030197017655394447/1212840955980550256)

* **Description:** Record $3B+ daily volume caused extreme network congestion during sharp price movement (17:26-17:32 UTC), preventing normal trading for users and HLP, leading to mark price volatility and unusual liquidations
* **Response:** Individual ticket review process initiated, affected users compensated from Assurance Fund according to fair policy framework
* **Outcome:** Platform scaling improvements implemented, consensus rewrite initiated, mark price formula enhanced for congestion resistance

[December 9, 2023](https://discord.com/channels/1029781241702129716/1030197017655394447/1182798702415462492)

* **Description:** User accidentally placed >$6M market order in wrong denomination (BTC instead of USD), experiencing high slippage
* **Response:** $15.4K refund from Assurance Fund, calculated by capping maximum slippage at 2%
* **Outcome:** Maximum notional value limits implemented for future orders based on asset liquidity

[November 14, 2023](https://discord.com/channels/1029781241702129716/1030197017655394447/1173693112913231902)

* **Description:** During YGG volatility period, profitable liquidation transfer from Liquidator vault to HLP caused uneven P\&L distribution (Liquidator -160K, HLP +200K), affecting early vault depositors
* **Response:** Platform operated as designed, but voluntary compensation provided for net losses through Assurance Fund to support unfamiliar users and early supporters
* **Outcome:** HLP integrated liquidation functionality, Liquidator vault retired, user protection enhanced

[August 22, 2023](https://x.com/HyperliquidX/status/1695102033437544783)

* **Description:** FRIEND-USD oracle vulnerability discovered by whitehats - TVL-based index was exploitable, allowing attackers to artificially inflate price by creating new subjects and buying shares atomically
* **Response:** Immediate oracle change to median price of 20 top subjects without advance notice to prevent exploit, maintenance margin refunds provided for liquidations during 01:48-14:00 UTC transition period
* **Outcome:** More secure oracle implementation, continued trading with isolated margin restrictions due to illiquid nature

[August 8, 2023](https://discord.com/channels/1029781241702129716/1030197017655394447/1138260805863874590)

* **Description:** YGG extreme volatility caused 50%+ divergence between oracle and mark prices, affecting liquidation fairness despite platform operating as designed with oracle-based liquidations
* **Response:** Compensation provided for YGG short maintenance margins liquidated during 12:00-16:00 UTC price divergence period, plus coverage for net Liquidator/HLP losses
* **Outcome:** Mark price liquidation system evaluation initiated, insurance fund formalized with fee allocation structure

***

### Platform Evolution

These incidents have driven continuous improvements to Hyperliquid's infrastructure, including enhanced network capacity, refined liquidation mechanisms, and stronger user protections. The Assurance Fund represents the platform's commitment to supporting users during the protocol's growth and development phases.

For current incident reports or compensation inquiries, users should open support tickets through official channels.
