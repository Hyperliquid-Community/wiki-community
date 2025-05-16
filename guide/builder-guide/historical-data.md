---
icon: timeline-arrow
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

# Historical Data

This page provides access to Hyperliquid's historical data, available via S3 buckets and specific API endpoints. It covers market, node, and HyperEVM data.

**Downloading via S3**:

* Data is stored in S3 buckets and requires the AWS CLI.
* Setup: Install [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) and [LZ4](https://github.com/lz4/lz4) (or via package manager).
* Commands:
  * **List contents**: `aws s3 ls s3://<bucket-name>/ --request-payer requester`
  * **Download**: `aws s3 cp s3://<bucket-name>/<path> <local-path> --request-payer requester`
* Most files are compressed in LZ4 (decompress with `unlz4 --rm <file>.lz4`).

***

## HyperCore

HyperCore data is stored in two S3 buckets: `s3://hyperliquid-archive/` and `s3://hl-mainnet-node-data/`. Below is a detailed overview of the available data types, their structure, and key information.

### **L2Book Data**

* **Description**:\
  Contains **OrderBook snapshots** (Level2 Book data) for each asset, updated twice per second.
* **Bucket and Folder Structure**:
  * `s3://hyperliquid-archive/market_data/`
  * Path: `market_data/<date>/<hour>/l2Book/<ASSET_NAME>.lz4`
  * Example: `s3://hyperliquid-archive/market_data/20250311/9/l2Book/SOL.lz4`
  * Note: Each asset has its own file.
* **Data Availability**:
  * From 2023 (first day) to April 13, 2025 (as of April 15, 2025).
  * Updated monthly by the Hyperliquid team.
* **Data Format**:
  * Compressed in LZ4; decompressed to JSON.
  * Snapshot frequency: Twice per second.
*   **Data Example (CSV format)**:

    <table><thead><tr><th width="134">time</th><th width="106">ver_num</th><th>raw</th></tr></thead><tbody><tr><td>2025-03-11T09:00:03.296545473</td><td>1</td><td>{'channel': 'l2Book', 'data': {'coin': 'SOL', 'time': 1741683599768, 'levels': [[{'px': '124.04', 'sz': '341.81', 'n': 2}, ...], [{'px': '124.05', 'sz': '427.89', 'n': 5}, ...]]}}</td></tr></tbody></table>
* **Notations**:
  * `px`: Price
  * `sz`: Size
  * `n`: Number of orders in the level
* **Example File**:

{% file src="../../.gitbook/assets/SOL (2).csv" %}

### **Node Data**

Node data is stored in `s3://hl-mainnet-node-data/` and split into three types: `node_trades`, `explorer_blocks`, and `replica_cmds`.

#### **node\_trades**

* **Description**:\
  Contains **pure trade data** (executed trades).
* **Folder Structure**:
  * `node_trades/hourly/<date>/<hour>.lz4`
  * Example: `s3://hl-mainnet-node-data/node_trades/hourly/20250411/3.lz4`
  * Note: All assets are combined in a single hourly file.
* **Data Availability**:
  * From March 22, 2025, ongoing.
* **Data Validation**:
  * Matches trade data displayed on the Hyperliquid interface.
*   **Data Example (CSV format)**:

    <table><thead><tr><th width="74">coin</th><th width="62">side</th><th width="117">time</th><th width="66">px</th><th width="65">sz</th><th width="70">hash</th><th width="86">trade_dir_override</th><th>side_info</th></tr></thead><tbody><tr><td>SOL</td><td>A</td><td>2025-04-11T02:59:59.991721263</td><td>114.31</td><td>7.82</td><td>0xf8e8...</td><td>Na</td><td>[{'user': '0xecb6...', 'start_pos': '-30955.03', 'oid': 85737377300, ...}, ...]</td></tr></tbody></table>
* **Notations**:
  * `side`: B (Buy/Bid), A (Sell/Ask); indicates the aggressing side.
  * `oid`: Order ID
  * `cloid`: Client Order ID (optional 128-bit hex string).
* **Example File**:

{% file src="../../.gitbook/assets/node_data_node_trades_3_head.csv" %}

#### **explorer\_blocks**

* **Description**:\
  Contains **transaction data**, it is possible to obtain the **FOB (Full Order Book)**.
* **Folder Structure**:
  * `explorer_blocks/<general_block>/<second_level_block>/<third_level_block>.rmp.lz4`
  * Example: `s3://hl-mainnet-node-data/explorer_blocks/500000000/559100000/559148100.rmp.lz4`
* **Data Availability**:
  * From the first block to present; frequently updated.
* **Data Format**:
  * Compressed in LZ4; decompressed to JSON.
  * Each file covers \~0.1 to 2 seconds.
*   **Data Example (CSV format)**:

    <table><thead><tr><th width="270">timestamp</th><th>data</th></tr></thead><tbody><tr><td>2025-04-11T08:48:40.861715273</td><td>{'type': 'cancel', 'cancels': [{'a': 67, 'o': 85784624043}]}</td></tr><tr><td>2025-04-11T08:48:40.978603002</td><td>{'type': 'order', 'orders': [{'a': 122, 'b': False, 'p': '0.31648', 's': '2027', 'r': False, 't': {'limit': {'tif': 'Alo'}}}, ...], 'grouping': 'na'}</td></tr></tbody></table>
* **Order Notations** ([API Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint)):
  * `a`: Asset (number)
  * `b`: Is Buy (boolean)
  * `p`: Price (string)
  * `s`: Size (string)
  * `r`: Reduce Only (boolean)
  * `t`: Type
    * “limitˮ:{ "      tif": "Alo" | "Ioc" | "Gtc"}
      * TIF (time-in-force) sets the behavior of the order upon first hitting the book.
      * ALO (add liquidity only, i.e. "post only") will be canceled instead of immediately matching.
      * IOC (immediate or cancel) will have the unfilled part canceled instead of resting.
      * GTC (good til canceled) orders have no special behavior.
    * Or "trigger": {"      isMarket": Boolean, "triggerPx": String, "tpsl": "tp" | "slˮ}
  * `c`: Client Order ID (cloid)
  * `grouping`: Grouping type ("na", "normalTpsl", "positionTpsl")
  * `builder`: Builder Codes fees (Optional). `b` specifies the address that should receive the additional fee, and `f` indicates the fee amount. (e.g. if `f` is 10, 1bp of the order notional will be charged to the user    &#x20;and sent to the builder).
* **Example File**:&#x20;

{% file src="../../.gitbook/assets/559148100.zip" %}

* **Comment**:
  * Heavy data: Each LZ4 file is \~1-2 MB (7-10 MB decompressed).
  * Transaction types include: cancel, cancelByCloid, scheduleCancel, batchModify, order, etc.

#### **replica\_cmds**

* **Description**:\
  Contains **L1 transactions** related to Hyperliquid Vault.
* **Folder Structure**:
  * `replica_cmds/<timestamp>/<date>/<block_number>.lz4`
  * Example: `s3://hl-mainnet-node-data/replica_cmds/2025-04-06T14:33:08Z/20250411/559130000.lz4`
* **Data Availability**:
  * From the first block to present; frequently updated.
*   **Data Example**:

    ```json
    {
      "signature": {
        "r": "0xbabde70bde012bfd63c733ca8d3e01f798a06a5fbffe58ea795a20f14f00d4b0",
        "s": "0x126441aaa485fcf5f20f61a88a04c9a7dacdc9e88fc8980e18cb6fc1ce26ef41",
        "v": 27
      },
      "vaultAddress": "0x010461c14e146ac35fe42271bdc1134ee31c703a",
      "action": {
        "type": "cancel",
        "cancels": [{"a": 142, "o": 85780697537}, {"a": 142, "o": 85780679669}]
      },
      "nonce": 1744359815156
    }
    ```
* **Notations:**
  * `a` : Asset
  * `o` : Order ID (oid)
* **Comment:**
  * Data very voluminous.

### API

* [**Perp**](hypercore/endpoints/info/perpetuals.md):
  * `userFunding`: Funding history for a user.
  * `userNonFundingLedgerUpdates`: Deposits, withdrawals, transfers.
    * **vaultDeposit**; **vaultWithdraw**
    * **deposit** (on perp); **withdraw** (from perp)
    * **accountClassTransfer** (transfer between spot and perp)
    * **internalTransfer** (perp transfer between HL accounts)
    * **spotGenesis** (genesis airdrop)
    * **spotTransfer** (transfer on spot market, to HyperEVM if destination is 0x22)
  * `fundingHistory`: Funding rates and premium history per coin.
* [**General**](hypercore/endpoints/info/):
  * `historicalOrders`: User’s historical orders (max 2000).
  * `portfolio`: Account value and PnL history.
  * `delegatorHistory`: User staking history.
  * `delegatorRewards`: Staking rewards.

***

## HyperEVM

* **Raw Block Data**:
  * Mainnet bucket: `s3://hl-mainnet-evm-blocks/`
  * Testnet bucket: `s3://hl-testnet-evm-blocks/`
  * Format: MessagePack (RMP) files compressed in LZ4.
  * Example: `s3://hl-mainnet-evm-blocks/0/6000/6123.rmp.lz4`
  * Command: `aws s3 ls s3://hl-mainnet-evm-blocks/ --request-payer requester`
* **Unofficial Tools**:
  * Sprites Tools: [GitHub](https://github.com/sprites0/block-importer) for backfilling EVM blocks to hl-visor or hl-node (use `--serve-evm-rpc`).
  * Need to export your transaction history or just want to see what happened on the chain a few months ago: [X Post](https://x.com/helloSQD/status/1897248650742604242)

***

## Additional Information

#### **Asset Information**:

* **Perp vs Spot**:
  * Perp: Asset ID = index in metadata (e.g., BTC/USDC index 0 → 0).
  * Spot: Asset ID = 10000 + perp index (e.g., ETH/USDC index 1 → 10001).
* **Identifiers**:
  * Asset ID: Perp = direct index, Spot = 10000 + index.
  * Token ID (=token\_index): Unique ID per token (e.g., HYPE = 150).
  * Spot ID (=universe\_index): Unique ID per spot pair (e.g., HYPE/USDC = 107).
    * Names: Spot = `@<Spot ID>` (e.g., `@107`), Perp = direct name (e.g., `HYPE`).
    * Check this [diagram](hypercore/endpoints/info/spot.md) (Tesnet) to understand.
* **Mapping**:
  * **Spot**: Via [Spot API](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/spot#retrieve-spot-metadata):
    1. Get `token_index` from "token".
    2. Find `universe_index` in "universe" with `[token_index, 0]`.
    3. Name = `@<universe_index>`.
  * **Perp**: Via [Perp API](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/perpetuals#retrieve-perpetuals-metadata): ordered indices (BTC = 0, ETH = 1, etc.).

{% file src="../../.gitbook/assets/spot_mappings (2).json" %}

{% file src="../../.gitbook/assets/perp_index_mapping (1).json" %}

#### **Resources:**

* Official documentation: [Historical Data](https://hyperliquid.gitbook.io/hyperliquid-docs/historical-data); [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/raw-hyperevm-block-data); [Notation](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/notation); [AssetIDs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/asset-ids).
