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

The **Hyperliquid Oracle System** plays a critical role in maintaining the accuracy and robustness of trading operations. It provides reliable price data for **funding rate calculations**, **margining**, **liquidations**, and the triggering of **Take Profit (TP)** and **Stop Loss (SL)** orders.

***

### **Spot Oracle Price** 📈

#### Definition:

The **spot oracle price** is computed by validators and serves as a critical input to both **funding rates** and the **mark price**.

#### Key Features:

* **Published by Validators Every 3 Seconds:** Ensures high-frequency updates for dynamic markets.
* **Weighted Median of CEX Prices:**
  * Prices are aggregated from major centralized exchanges (CEXs), including Binance, OKX, Bybit, Kraken, Kucoin, Gate IO, MEXC, and Hyperliquid itself.
  * **Weights:** Binance (3), OKX (2), Bybit (2), Kraken (1), Kucoin (1), Gate IO (1), MEXC (1), Hyperliquid (1).
  * **Final Price for Clearinghouse:**\
    The clearinghouse uses the **weighted median of validator-submitted prices**, with validators weighted by their **stake**.

### **Mark Price** 📊

**Definition:**

The mark price is an unbiased, robust estimate of the **fair price** for perpetual contracts.

#### **Components:**

* **Spot Oracle Price:**
  * Acts as the baseline.
  * Plus a **150-second EMA Adjustment:**
    * An Exponential Moving Average (EMA) over 150 seconds of the **difference** between **Hyperliquid’s mid-price** and the **spot oracle price**.
    * This EMA smooths out short-term fluctuations and ensures that any short-lived deviations between Hyperliquid’s price and the broader market are gradually integrated into the mark price.
* **Hyperliquid Order Book Median:**
  * The median of the **best bid**, **best ask**, and the **last trade** price on Hyperliquid.
* **External Perpetual Market Median:**
  * The median of the **mid-prices** from Binance, OKX, and Bybit’s **perpetual contracts**.
  * Incorporating prices from these leading exchanges adds another layer of market depth and stability to the mark price calculation.
* **Special Case:**
  * **If only two of the three inputs exist,** a **30-second EMA** of the median of best bid, best ask, and last trade on Hyperliquid is included.

**Usage:**\
Used for liquidations, margin calculations, triggering TP/SL orders, and computing unrealized profit and loss (PnL) for active positions.

**Update Frequency:** Approximately every 3 seconds, in sync with oracle updates.

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

### **Uniswap Perpetuals** 🦄

Some perpetual contracts on Hyperliquid use **Uniswap V2 or V3 AMM prices** as their underlying spot asset.

* **Isolated-Only:**
  * These contracts do not allow cross margining or manual margin removal.
  * To adjust margin, positions must be partially or fully closed.
* **Conversion to USDT:**
  * Uniswap pool prices are converted to USDT using robust CEX oracle prices.

[Contract Addresses for Uniswap Pools](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/uniswap-perpetuals)

***

### **Margining and Oracle Usage** 💵

#### **USDC Margining with USDT Prices**

* **Primary Style:**
  * Oracle prices are denominated in **USDT**, while collateral is held in **USDC**.
  * This combination maximizes **liquidity** and **accessibility**.
* **Quanto Contracts:**
  * No conversion between USDC/USDT exchange rates occurs, meaning USDT P\&L is denominated directly in USDC.

#### **USDC-Denominated Contracts:**

* **Specific Assets:**
  * Only contracts with primary USDC liquidity (e.g., **PURR-USD** and **HYPE-USD**) have prices denominated in USDC.

***

#### Resources:

* [Robust price indices](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices)
* [Oracle](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-l1/oracle)

This robust oracle system ensures Hyperliquid remains fair, reliable, and transparent for all traders.
