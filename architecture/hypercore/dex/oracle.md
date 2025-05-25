---
icon: crystal-ball
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

# Oracle

The Hyperliquid Oracle System provides reliable price data for funding rates, margining, liquidations, and triggering Take Profit/Stop Loss orders through robust, manipulation-resistant mechanisms.

***

### **Spot Oracle Price** 📈

* **Validator-computed:** Published by validators **every 3 seconds** for high-frequency market updates
* **Weighted median** of major CEX prices: **Binance (3), OKX (2), Bybit (2), Kraken (1), Kucoin (1), Gate IO (1), MEXC (1), Hyperliquid (1)**
* **Final clearinghouse price:** Weighted median of validator-submitted prices (validators weighted by stake)
* **Usage:** Primary input for funding rate calculations and mark price component

**Special cases:**

* **Hyperliquid-native assets** (e.g., HYPE): External sources excluded until sufficient external liquidity
* **External primary liquidity** (e.g., BTC): Hyperliquid spot prices excluded from oracle

### **Mark Price** 📊

**Unbiased, robust estimate** of fair perpetual contract price using median of three components:

1. **Oracle price + 150-second EMA adjustment** • EMA of difference between Hyperliquid mid-price and oracle price • Smooths short-term fluctuations and integrates market deviations
2. **Hyperliquid order book median** • Median of best bid, best ask, and last trade price
3. **External perpetual median** • Median of mid-prices from **Binance (3), OKX (2), Bybit (2), Gate IO (1), MEXC (1)**

**Special handling:** If only 2 of 3 components exist, a **30-second EMA** of Hyperliquid bid/ask/last trade is added

**Update frequency:** \~3 seconds (synced with oracle updates)\
**Usage:** Liquidations, margin calculations, TP/SL triggers, unrealized PnL

#### Example

* **Spot Oracle Price:** Calculated as **$10,000**.
* **150-Second EMA:** Indicates Hyperliquid’s mid-price is on average **+$20** above the oracle price (i.e. **$10,020**).
* **Hyperliquid Median (Bid/Ask/Last Trade):**
  * Suppose the current best bid is **$10,005**, the best ask is **$10,015**, and the last trade occurred at **$10,010**.
  * The median of these three numbers would be **$10,010**.
* **External Perpetual Median:**&#x20;
  * Imagine the mid-prices from these exchanges are **$9,995**, **$10,000**, and **$10,010**.
  * The median of these values is **$10,000**.
* The mark price is computed by combining the spot oracle price with the above inputs.\
  In our example, the final mark price might then be in the vicinity of **$10,010 to $10,020** (the exact mathematical formula is not publicly disclosed), reflecting both the consensus market price and the slight premium observed on Hyperliquid.

#### Comparison Table: Spot Oracle Price vs. Mark Price ⚖️

| Feature                    | Spot Oracle Price                                | Mark Price                                                                                                           |
| -------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| **Source of Data**         | Aggregated CEX prices and Hyperliquid price      | Combination of oracle price, Hyperliquid order book data, and external perpetual markets                             |
| **Update Frequency**       | Every 3 seconds                                  | Every 3 seconds                                                                                                      |
| **Calculation Method**     | Weighted median (using set weights per exchange) | Composite calculation: spot oracle price + 150-second EMA adjustment + medians from Hyperliquid and external sources |
| **Primary Use**            | Funding rate calculations                        | Liquidations, margin calculations, TP/SL triggers, unrealized PnL computation                                        |
| **Additional Adjustments** | N/A                                              | Special inclusion of a 30-second EMA if one main input is missing                                                    |

***

### **Margining & Contract Types** 💵

**Standard contracts:**

* **USDC collateral, USDT-denominated prices** - maximizes liquidity and accessibility
* **Quanto structure:** No USDC/USDT conversion applied (USDT P\&L directly in USDC)

**USDC-denominated contracts:**

* **PURR-USD, HYPE-USD** - use USDC pricing due to primary Hyperliquid spot liquidity

**Uniswap Perpetuals:**

* **Isolated margin only** - no cross margining or manual margin removal
* **Uniswap V2/V3 AMM prices** converted to USDT using robust CEX oracle prices
* **Margin adjustment:** Only through position closure (partial/full)

***

### **Anti-Manipulation Features** 🛡️

* **Oracle independence:** Spot oracle completely separate from Hyperliquid market data
* **Weighted medians:** Resistant to single-source manipulation
* **Multi-component mark price:** Combines internal and external data sources
* **EMA smoothing:** Prevents short-term price manipulation from affecting critical calculations
* **Validator stake-weighting:** Ensures oracle integrity through economic incentives

This robust oracle architecture ensures fair, transparent, and manipulation-resistant price discovery for all Hyperliquid trading operations.

### Resources

* [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices)
* [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-l1/oracle)
* [Contract Addresses for Uniswap Pools](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/uniswap-perpetuals)
