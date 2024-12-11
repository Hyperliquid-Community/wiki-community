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

# Funding

Funding rates are a critical mechanism in crypto perpetual contracts, ensuring that the perpetual contract price remains closely aligned with the underlying asset's spot price. On Hyperliquid, funding is designed to be **peer-to-peer**, transparent, and reflective of real market conditions.

***

### **Overview of Funding** 📈

* **Peer-to-Peer Payments:**\
  Funding involves direct payments between traders—**longs pay shorts** or vice versa. The platform does not collect any fees from these payments.
* **Hourly Settlements:**\
  Funding is accrued and paid **every hour**, providing consistent adjustments to the market.
* **Base Interest Rate + Premium:**\
  The funding rate is computed as the sum of:
  1. A **fixed interest** **rate** of **0.01% every 8 hours** applies, representing the cost difference between borrowing USD or cryptocurrencies. This corresponds to approximately **0.00125% per hour** and an **APR (Annual Percentage Rate) of \~11.6%**.
  2. A **premium/discount component**, which reflects the difference between the perpetual contract price and the **oracle-derived spot price** of the asset.

***

### **Funding Rate Calculation** 🧮

The funding rate formula is:

```lua
F = Average Premium Index (P) + clamp(Interest Rate - Premium Index (P), -0.0005, 0.0005)
```

* **Premium Index (P):** Reflects the difference between the **impact price** (calculated using order book depth) and the **oracle price**.
  * **Sampling:** The premium is sampled every **5 seconds** and averaged over the hour
* **Clamp:** Limits extreme differences between the interest rate and the premium index.

#### **Impact Price Calculation:**

```lua
impact_price = max(impact_bid_px - oracle_px, 0) - max(oracle_px - impact_ask_px, 0)
```

Where:

* **impact\_bid\_px / impact\_ask\_px** = Average execution prices to trade a specified notional amount on the bid and ask sides.
* **oracle\_px** = Weighted median of prices submitted by validators, ensuring accuracy and robustness.

***

### **Key Points** 💡

* **Oracle-Driven Calculations:**\
  The **spot oracle price**, derived from a weighted median of validator submissions, is fundamental in calculating the funding rate. Validators’ weights depend on their stake and the liquidity of the CEX they monitor.
*   **Funding Impact Notional:**\
    The impact notional used for funding calculations depends on the asset:

    * **20,000 USDC** for BTC and ETH.
    * **6,000 USDC** for all other assets.

    For example, a **50,000 USDC** BTC position pays funding only on the first **20,000 USDC**.
* **Caps on Funding Rates:**\
  Funding on Hyperliquid is capped at **4% per hour**, a much less aggressive cap than many centralized exchanges.
*   **Payments Formula:**\
    Funding payments are settled as:

    ```lua
    Payment = position_size × oracle_price × funding_rate
    ```

    The oracle price, not the mark price, is used to calculate the notional value for funding payments.

***

### **Example Calculation** 📝

1. **Scenario:**
   * Interest Rate = 0.01%
   * Impact Bid Price = $10,100
   * Spot Oracle Price = $10,000
   * Position Size = 10 contracts (each representing 1 BTC)
2.  **Step 1: Calculate Premium Index (P):**

    ```lua
    Premium = (Impact Bid Price - Spot Oracle Price) / Spot Oracle Price
    Premium = ($10,100 - $10,000) / $10,000
    Premium = 0.01 (1%)
    ```
3.  **Step 2: Clamp the Difference:**

    ```lua
    Clamped Difference = min(max(Interest Rate - Premium, -0.05%), 0.05%)
    Clamped Difference = min(max(0.01% - 1%, -0.05%), 0.05%)
    Clamped Difference = -0.05%
    ```
4.  **Step 3: Calculate Funding Rate (F):**

    ```lua
    Funding Rate = Premium + Clamped Difference
    Funding Rate = 1% + (-0.05%)
    Funding Rate = 0.95%
    ```
5.  **Step 4: Compute Payment:**

    ```lua
    Payment = Position Size × Oracle Price × Funding Rate
    Payment = 10 × $10,000 × 0.0095
    Payment = $950
    ```

***

### **Why Funding Matters** 🔗

Funding incentivizes traders to take positions that align the perpetual price with the spot price. This **price convergence mechanism** maintains a stable and fair trading environment for all participants. Hyperliquid's funding model closely mirrors centralized exchanges but adds decentralization and transparency, making it uniquely robust.
