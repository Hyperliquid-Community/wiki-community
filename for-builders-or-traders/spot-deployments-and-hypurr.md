---
icon: rocket
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

# Spot Deployments & Hypurr

This section is designed for **builders and traders**, providing a step-by-step guide on how to:

1. Deploy and trade assets on **Hyperliquid Spot**.
2. Leverage the **Hypurr Fun Bot** to explore and participate in new token launches.

For a detailed understanding of **HIP-1** and **HIP-2** (the foundation of Spot deployments), refer to the [community documentation here](https://community-hyperliquid.gitbook.io/community-docs/technical-overview-of-hyperliquid/hyperliquid-l1/hips/spot-deployments-hip-1-hip-2).

***

### **Using the Hypurr Fun Bot**

Hypurr Fun is a launch market and **social-fi bot** designed for the Hyperliquid L1. It simplifies token launches and provides a vibrant pre-market for discovering and trading new assets. Follow these steps to get started:

#### **Step 1: Set Up Your Wallet**

1. **Create an account on Telegram:** [Hypurr Fun Bot](https://t.me/HypurrFunBot).
2. **Fund your account:**
   * Transfer **at least 11 USDC** to your Hyperliquid wallet.
   * Bridge USDC from **Arbitrum** to Hyperliquid using [Debridge Finance](https://debridge.finance) or [Hybridge](https://hybridge.finance).
3. **Generate your wallet address:**
   * Type `/wallet` in the bot to receive your unique wallet address.
   * It’s highly recommended to **export your private key** and store it securely.
   * For more information on wallets, refer to the [Hypurr Fun Wallet Documentation](https://hypurr-fun.gitbook.io/hypurr-fun-docs/wallets/multi-wallets).

### Pre-Launches (On Hypurr)

#### **Step 2a: Explore New Pre-Launches**

Stay updated on the latest launches by exploring these resources:

* **HypurrPump Prelaunch Market:** [Telegram Group](http://t.me/+GRIwAPnAUBk4ODE0)
  * Focused exclusively on tokens **not yet launched** on the Hyperliquid L1.
* **Dashboard for Prelaunches:** [app.hypurr.fun/launches](https://app.hypurr.fun/launches)

On the **Hypurr Dashboard**, you can find:

* **Trust Factor Indicators:** 🟢 (High Trust), 🟡 (Moderate Trust), 🔴 (Low Trust), offering a quick assessment of a token's perceived reliability.
* **Creator Information:** See the deployer’s Telegram handle and check their reputation in the Hypurr Fun community.
* **Bonding Progress:** Track the progress of a launch towards bonding (e.g., TVL and auction price thresholds).

#### **Step 3a: Buy a Pre-Launch Token**

1. Select a token launch from HypurrPump (#Launch Alert)
2. Click "Trade" to access the community group for that token.
3. Execute purchases directly through the bot using commands like `/buy` and `/sell`.

### **Launches (On Hyperliquid L1)**

#### **Step 2b: Explore New Launches**

* **Hypurr Fun Community Group:** [Join Here](http://t.me/+SJRiO42rufBmODBk)
* **Explorer** : [Hypurrscan](https://hypurrscan.io/dashboard)

#### **Step 3b: Buy a Launch Token**

* **Trade Spot Tokens:** Just like on the **Hyperliquid DEX**, you can buy and sell spot tokens directly through the bot. \[[Read more about spot trading and TWAPs](https://hypurr-fun.gitbook.io/hypurr-fun-docs/trade/trade-spot-tokens)]
* **Sniping New Launches**
  * **Automatic Sniping:** Configure the bot to automatically **snipe new token launches** as soon as they go live.
  * **Manual Alerts:** Alternatively, wait for alerts in the **Hypurr Fun Telegram channel** to decide your entry manually. \[[Learn more about sniping setups](https://hypurr-fun.gitbook.io/hypurr-fun-docs/sniper/sniper)]
* **Dumping Tokens at Launch**
  * The bot also supports **automated token dumping**, allowing you to sell your airdropped tokens as soon as they’re launched on the Hyperliquid L1. This ensures you can capitalize on market opportunities early. \[[Find out more about dumping tokens](https://hypurr-fun.gitbook.io/hypurr-fun-docs/dumper/dump-your-airdrop)]

***

### **Understanding Hypurr’s Pre-Market Mechanism**

#### **Bonding Curve Overview**

The Hypurr pre-market operates on a **bonding curve model**, similar to Uniswap V2’s **Constant Product Market Maker (CPMM)**, using the formula: X⋅Y=K

Here’s how it works:

1. **X (USDC):** The amount of USDC inflow during token purchases.
2. **Y (Tokens):** The number of tokens available for sale.
3. **K:** A constant value that ensures the curve remains balanced.

#### **Threshold Formula for Bonding**

For a pre-launch token to bond and be listed on Hyperliquid, the following condition must be met: **X⋅0.65 > Auction Price**.

This ensures that sufficient USDC has been accumulated in the bonding curve to pay for the gas cost and seed initial liquidity in the buy-side order book.

**How It Works**

1. **Market Dynamics:**
   * As buyers purchase tokens, X (USDC) increases while Y (tokens) decreases.
   * For example:
     * Initial Parameters: X0=500; Y0=1,000,000; starting price = $0.0005
     * After $99,500 net inflow, **X=100,000**, price = $0.1.
2. **Bonding Trigger:**
   * Once X⋅0.65=65,000 (auction threshold), the token can bond.
   * The **deployer** must manually initiate bonding through the [Hyperliquid Deploy Spot Interface](https://app.hyperliquid.xyz/deploySpot). Some configurations may allow automatic bonding once the threshold is met.
3. **USDC Allocation:**
   * **65% (Auction Price):** Pays the gas cost for deploying the token.
   * **35% (Remaining USDC):** Automatically added to the HIP-2 liquidity pool, creating a reliable **buy-side market**.
4. **Airdrop to Buyers:**
   * Once bonded, early buyers receive a **proportional airdrop** of the actual token. This is sent directly to their **Hypurr Fun bot wallet**.

***

### **Technical Workflow of Hypurr Launches**

#### **Key Mechanics:**

* **Backend Operations**
  * When a token is launched, the **Hypurr backend interacts with the Hyperliquid API** to:
    * **Create a new wallet (address):** Each token is assigned a unique wallet, which acts as the central point for managing transactions related to that token.
    * **Link the wallet to the token ticker:** A database keeps track of this association, enabling the system to query and monitor blockchain transactions involving the token.
    * **Token Purchases:** When someone buys a token, the system simply **transfers the purchased amount to the wallet address linked to the ticker**. The system calculates how much the buyer needs to pay based on the CPMM.
  * The backend uses this data to display information such as token holdings, bonding progress, and market activity directly in the bot or [dashboard](https://app.hypurr.fun/).
* **Launch Protections:**
  * Creators must lock **$500** for 10 minutes to prevent immediate dumping.
  * Orders are capped at **$1,500** during the first **60 seconds** to ensure fair trading.
  * Trading starts **15 seconds** after launch to give everyone equal access.
  * Creators can preconfigure a **notional buy** to secure a portion of their token during the launch, competing with snipers.
* **Bonding Curve Process:**
  * **Virtual Balances:** The curve initializes with X0 (USDC) and Y0​ (tokens).
  * As users purchase tokens, the curve adjusts price levels and liquidity.

***

#### **Additional Resources**

For detailed guides on how to use the Hypurr Fun Bot and maximize its potential:

* [Step-by-step guide by @Jimihendrixgin](https://x.com/jimihendrixgin/status/1867770279847469437)
* [Tips and strategies from @DegennQuant](https://x.com/degennQuant/status/1865755024816852996)
* [Official Guide](https://hypurr-fun.gitbook.io/hypurr-fun-docs/launches/buying-a-token)
* [Strategies](https://l1ghtyear.notion.site/HL-Trenches-Ultimate-Guide-12f90df6c9b780b29adbdbd8717f86be)

**Official Hypurr Fun Docs:** [hypurr-fun.gitbook.io](https://hypurr-fun.gitbook.io/hypurr-fun-docs)

Before investing in or trading **listed tokens on Hyperliquid**, it’s essential to understand their history and potential risks. Some projects may be scams or poorly managed. The following resources provide detailed information on previously listed tokens:

* [General Overview on Notion (Pasteke)](https://0xpasteke.notion.site/68a1348a53c14e6fbd405036128037f5?v=26e777a949c34b6090b888ed20627295)
* [Spot Tokens Overview on Notion (ScroogeMcCoin)](https://scroogemccoin.notion.site/Hyperliquid-Spot-Tokens-df2f09de70f94fd2a761752a1ac71dc2)
* [Community-Compiled Spreadsheet of Tokens](https://docs.google.com/spreadsheets/d/1uDKdvamD6gOGPtzfyhjcY8eRsoXKm544v3uNu-f_H6o/edit?gid=0#gid=0)
