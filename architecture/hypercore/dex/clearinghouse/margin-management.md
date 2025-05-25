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

# Margin Management

Margin management in HyperCore ensures traders can efficiently use their capital while maintaining robust risk controls. The system balances capital efficiency with decentralized safety mechanisms, offering familiar margin modes while pioneering new approaches to protect against manipulation.

***

### **Margin Modes**

Traders can choose between two margin modes depending on their risk appetite and trading strategy:

**Cross Margin** 🌐

* **Shared collateral pool** - All positions share a single collateral pool, maximizing capital efficiency
* **Dynamic margin allocation** - Unrealized profits automatically become available margin for new positions
* **Portfolio-wide risk** - Losses on one position impact the entire portfolio since all positions draw from the same collateral

**Isolated Margin** 🔒

* **Dedicated collateral** - Each position has its own dedicated margin, isolating risk from other trades
* **Flexible adjustments** - Add or remove margin for individual positions after opening
* **Granular risk control** - Losses on one position don't affect others, providing better liquidation management

***

### **Initial Margin and Leverage**

**Leverage Selection**

* Choose leverage from 1x to maximum (varies by asset, typically 3x-50x)
* Higher leverage reduces initial margin requirements but increases liquidation risk
* Leverage is only checked when opening positions - monitor actively afterwards

**Initial Margin Calculation**

* **Formula**: `Initial Margin = (Position Size × Mark Price) ÷ Leverage`
* Cross margin locks initial margin (cannot be withdrawn)
* Isolated margin allows adjustments after position opening

**Understanding Margin Requirements** 💡

* **Initial Margin** = Collateral needed to **open** a position (depends on your chosen leverage)
* **Maintenance Margin** = Minimum collateral to **keep** position open (fixed % of position size)
* Example: $10,000 position on 20x max leverage asset:
  * With 10x leverage: Initial margin = $1,000, Maintenance margin = $250
  * With 20x leverage: Initial margin = $500, Maintenance margin = $250 (same!)
* Higher leverage means starting closer to liquidation threshold

**Managing Existing Positions**

* Partially or fully close positions
* Add margin (isolated positions only)
* Deposit USDC (affects cross positions)
* Increase leverage without closing (subject to margin requirements)

***

### Margin Tiers

Hyperliquid implements a tiered leverage system that adjusts maximum leverage based on position size, similar to major centralized exchanges but adapted for decentralized trading.

**How Tiers Work**

* **Maintenance margin** = Half of initial margin at max leverage (e.g., 20x leverage = 2.5%)
* **Maintenance deduction** = Adjustment that ensures smooth transitions between tiers
  * When position size crosses tier boundaries, prevents sudden jumps in margin requirements
  * Calculated to maintain continuous margin scaling across all position sizes
  * Example: Moving from $19M to $21M position smoothly transitions from 10x to 5x tier
* Larger positions automatically receive lower maximum leverage

**Current Mainnet Tiers**

**Large Cap Assets** (DOGE, kPEPE, SUI, WLD, TRUMP, LTC, ENA, POPCAT, WIF, AAVE, kBONK, LINK, CRV, AVAX, ADA, UNI, NEAR, TIA, APT, BCH)

* 0-20M USDC: **10x max leverage**
* > 20M USDC: **5x max leverage**

**Mid Cap Assets** (OP, ARB, LDO, TON, MKR, ONDO, JUP, INJ, kSHIB, SEI, TRX, BNB, DOT)

* 0-3M USDC: **10x max leverage**
* > 3M USDC: **5x max leverage**

***

### Unrealized PnL and Transfers

**Withdrawal Requirements**

* Unrealized PnL can be withdrawn from isolated positions or cross account, if remaining margin ≥ 10% of total position value
* Must also meet initial margin requirements
* **Transfer margin required** = max(initial margin, 10% × total position value)

**Anti-Manipulation Design**

* Liquidated positions must show either:
  * Loss relative to entry price, OR
  * 18.3% loss relative to last margin transfer (at 20x leverage)
* Prevents profitable manipulation through forced liquidations
* Maintains capital efficiency for legitimate traders
* As liquidity improves and market makers scale up, price manipulation becomes increasingly expensive, providing natural protection beyond technical safeguards

**Liquidation Triggers**

* **Cross Margin**: Account value (including unrealized PnL) < maintenance margin × total position notional
* **Isolated Margin**: Position-specific calculation using only that position's margin and notional

***

### Key Principles

Hyperliquid's margin system prioritizes:

* **True decentralization** - No centralized control or restrictions
* **Capital efficiency** - Familiar margin modes with unrealized PnL withdrawals
* **Robust safety** - First-principles approach to prevent manipulation
* **User experience** - Deterministic liquidation prices, clear risk parameters

The system continues to evolve as liquidity improves, making price manipulation increasingly expensive and attracting sophisticated market makers who provide additional market stability.

***

### Resources

* [Official Margining Documentation](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margining)
* [Official Margin Tiers Documentation](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers)
* [Jeff's Thread on Margin Design Philosophy](https://x.com/chameleon_jeff/status/1900218435562578130)
* [Jeff's Comments on DEX Margin Safety](https://x.com/chameleon_jeff/status/1726091053491470408)
