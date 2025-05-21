---
icon: shield-cat
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

# Felix

Felix Protocol is the **second largest protocol** on Hyperliquid with over $150M TVL (as of May 21, 2025), trailing only behind Hyperlend. The [protocol's approach](https://x.com/emaverick90/status/1915013107753144542) aligns with Hyperliquid's philosophy, focusing on ecosystem growth and improvement while prioritizing **security, economic stability, and transparency**.

Led by founders [@0xBroze](https://x.com/0xBroze) and [@emaverick90](https://x.com/emaverick90), Felix maintains an educational approach through detailed articles and transparent communications about their development process.

### What is Felix Protocol?

Felix offers a **suite of on-chain borrowing and lending products** on Hyperliquid L1, designed to provide liquidity and yield opportunities with minimal friction.

The protocol consists of **two core primitives**:

<table><thead><tr><th width="203.6666259765625">Primitive</th><th>Purpose</th><th>Target Users</th></tr></thead><tbody><tr><td><strong>CDP Market (feUSD)</strong></td><td>Mint feUSD stablecoins against collateral</td><td>Traders seeking high LTV and cost-effective leverage</td></tr><tr><td><strong>Vanilla Markets</strong></td><td>Variable-rate lending pools for native assets</td><td>Users preferring direct asset exposure with dynamic rates</td></tr></tbody></table>

### Felix CDP Market: Core Mechanics

The CDP Market enables users to **deposit collateral** (like HYPE or UBTC) and **mint feUSD stablecoins** against it. This system brings together:

* **Borrowers/Minters** who deposit collateral and **set their own interest rates**
* **Stability Pool Depositors** who provide feUSD liquidity and earn interest, fees, and liquidation gains

#### Two Key Mechanisms Maintain the feUSD $1 Peg:

1. **Liquidations**
   * Occurs when a position's health falls below the threshold
   * Example: User deposits $10,000 in HYPE and borrows $5,000 feUSD. If HYPE value falls to $9,000, the LTV rises to \~55%, triggering liquidation
   * The system burns feUSD from the Stability Pool and transfers the borrower's collateral (plus a small penalty) to SP depositors
2. **Redemptions**
   * Activates when feUSD trades below $0.995
   * Prioritizes positions with the lowest interest rates first
   * Anyone can swap 1 feUSD for $1 of collateral from these positions
   * Unlike liquidations, redemptions can be partial rather than full
   * To avoid redemptions: ensure your interest rate is competitive compared to the median rate

**For borrowers:** Maintain adequate position health (1.25-1.50 recommended) and set competitive interest rates to avoid being first in line for redemptions.

**For lenders:** Earn from multiple revenue streams:

* Borrower interest (75% routed to Stability Pools)
* Protocol fees from position openings and rate changes
* Liquidation incentives (acquiring discounted collateral)

### Vanilla Markets

Felix's Vanilla Markets operate on Morpho's lending stack, providing a **traditional lending model** similar to Hyperlend:

* **Deposit collateral** (HYPE, UBTC, ETH) to borrow assets like HUSD or USDC
* **Supply idle assets** to earn yield through a floating APY determined by utilization
* **No redemption mechanics** - positions are immune to feUSD peg fluctuations

The primary risk is **liquidation** when a position's health factor falls below 1.0.

### HUSD: Recycling Value Back to Hyperliquid

HUSD is a **fiat-backed stablecoin** native to Hyperliquid, designed specifically to benefit the Hyperliquid ecosystem.

**Why HUSD matters:**

* Currently, $2.5B of bridged USDC on HyperCore generates \~$107.5M in annual interest revenue flowing to Circle
* As Hyperliquid grows 10x, 100x, or 1000x, this opportunity cost only increases

**How HUSD works:**

* A significant portion of interest revenue is used to **purchase HYPE** in the open market
* Similar to the Assistance Fund's automated HYPE buy-backs, but at the stablecoin layer
* Purchased HYPE is strategically redeployed to fuel ecosystem growth

**HUSD's impact on Builder Codes:**

* Helps bootstrap "Hyperliquid hybrids" by subsidizing builder code fees
* Allows interfaces to charge higher rates at no cost to users
* Example: If Interface XYZ receives 100 HUSD in rebate budget, it could process $100,000 worth of futures volume before users bear any cost
* Interface operators can reinvest builder code revenues into user acquisition and retention

**HUSD and feUSD synergy:**

* HUSD provides deep liquidity for feUSD pairs on Curve StableSwap, improving peg stability
* Serves as a lending asset on Felix's Vanilla Markets
* Potential future integration as collateral for minting feUSD (similar to USDC's role in DAI's PSM)
* Together, they form a complementary stablecoin pair rather than competing alternatives

HUSD created as a **public good initiative** by HyperActive and Felix in collaboration with the [@m0foundation](https://x.com/m0foundation).

### Resources

* **Getting Started**
  * [Felix Vanilla vs Felix CDP: Which is Right For You?](https://x.com/0xBroze/status/1922626240919257377) - Comparison to help choose the right product
  * [CDP Market Quickstart Guide](https://usefelix.gitbook.io/felix-docs/money-market-products/quickstart/quickstart#step-1-connect-wallet)
  * [Earning feUSD Yield Guide](https://usefelix.gitbook.io/felix-docs/money-market-products/quickstart/earning-feusd-yield#step-1-connect-wallet)
  * [Position Management Guide](https://usefelix.gitbook.io/felix-docs/money-market-products/quickstart/publish-your-docs)
* **Educational Content**
  * [Understanding Felix Stability Pools](https://x.com/0xBroze/status/1911762191897739707) - Explains yield mechanics, risk dynamics, and market impact
  * [Understanding Redemptions and Liquidations](https://x.com/0xBroze/status/1907395802449780931) - Guide to optimizing capital efficiency
  * [What does it mean to be a Hyperliquid-aligned fiat stable?](https://x.com/husd_fiat/status/1923017204045406416) - Explains HUSD's role in the ecosystem
  * [The Role of HUSD in the Felix Ecosystem](https://x.com/0xBroze/status/1917551086979932574) - How HUSD and feUSD work together
* **Official Documentation**
  * [Felix Protocol Documentation](https://usefelix.gitbook.io/felix-docs/)
