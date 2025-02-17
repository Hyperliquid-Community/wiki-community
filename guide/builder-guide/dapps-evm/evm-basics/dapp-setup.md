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

# dApp Setup

This guide covers how to configure and deploy a dApp on HyperEVM.

***

### **1. Setting Up Your Application**

Before deploying contracts, your dApp needs a proper setup with wallet integration and blockchain connectivity. HyperEVM supports standard Ethereum libraries, ensuring compatibility with tools like:

* **Wagmi / Viem & Ethers** – for seamless wallet connections.
* **Hyperliquid RPC endpoints** – to interact with the blockchain.

For a step-by-step guide on setting up a **Next.js application with Wagmi**, refer to the [**Builder Codes Guide**](../../api/builder-codes.md).

***

### 2. Deploying a Smart Contract on Hyperliquid EVM

Deploying a smart contract on Hyperliquid follows a similar workflow to Ethereum. You can use **Foundry** or **Hardhat**, two popular development frameworks.

* This guide focuses on **Foundry**, but you can find additional [**Hardhat resources here**](https://hardhat.org/tutorial).

#### **1️⃣ Deploying with Foundry**

_**Note:** This is an old data sheet, so some details may not be accurate for HyperEVM. I haven’t tested deployment on HyperEVM yet, but an update is coming soon. For now, consider this a summary rather than a full guide._

* **Resources:**
  * [Foundry documentation](https://book.getfoundry.sh/getting-started/installation)
  * [Tutorial](https://www.youtube.com/watch?v=GWLxIYAIMqQ\&list=PL2-Nvp2Kn0FPH2xU3IbKrrkae-VVXs1vk\&ab_channel=CyfrinAudits)
  * [OpenZeppelin](https://wizard.openzeppelin.com/)
*   **Install & Update Foundry**\
    First, ensure you have **Foundry** installed and updated:\
    ⚠️ Windows Users: Install [**WSL**](https://learn.microsoft.com/en-us/windows/wsl/install) or [**Git Bash**](https://gitforwindows.org/) to run these commands.

    ```bash
    curl -L https://foundry.paradigm.xyz | bash
    foundryup
    ```
*   **Create a New Project**

    ```bash
    forge init hello_foundry
    cd hello_foundry
    ```
*   (Optional) **Link to GitHub**:

    ```bash
    git remote add origin <REMOTE_URL>
    git remote -v
    echo "/lib/" >> .gitignore  # Ignore dependencies  
    git push -u origin main
    ```
*   **Install Dependencies**

    ```bash
    forge install openzeppelin/openzeppelin-contracts --no-commit
    ```

    *   **Configure remappings** in `foundry.toml`:

        ```bash
        remappings = ['@openzeppelin=lib/openzeppelin-contracts']
        ```
*   **Compile & Test**

    ```bash
    forge build
    forge test -vvv
    ```
*   **Deploy on a Local Devnet (Anvil)**\
    Start Anvil in a separate terminal:

    ```bash
    anvil
    ```
*   **Deploy the contract:**\
    Create a Script and run this command:

    ```bash
    forge script script/Token.s.sol --rpc-url http://127.0.0.1:8545 --broadcast --private-key <PRIVATE_KEY>
    ```
*   **Deploy on Testnet**\
    Add your testnet credentials to `.env`:

    ```bash
    SEPOLIA_RPC_URL=https://sepolia.infura.io/v3/YOUR_PROJECT_ID
    SEPOLIA_PRIVATE_KEY=YOUR_PRIVATE_KEY
    ```

    *   Deploy on **Sepolia**:

        ```bash
        source .env
        forge script script/Token.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $SEPOLIA_PRIVATE_KEY --broadcast
        ```
    *   **Verify the contract automatically**:

        ```bash
        ETHERSCAN_API_KEY=YOUR_KEY
        forge script script/Token.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $SEPOLIA_PRIVATE_KEY --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY
        ```
    * **Check deployment on Etherscan**:\
      Take the transaction hash from the deployment output and search for it on [**Etherscan**](https://sepolia.etherscan.io/) to view your contract.
    *   **Verify an already deployed contract**:

        ```
        forge verify-contract
        --chain-id 11155111
        --num-of-optimizations 1000000
        --watch
        --constructor-args $(cast abi-encode "constructor(string,string,uint256,uint256)" "ForgeUSD" "FUSD" 18 1000000000000000000000)
        --etherscan-api-key <your_etherscan_api_key>
        --compiler-version v0.8.10+commit.fc410830
        <the_contract_address>
        src/MyToken.sol:MyToken
        ```

#### 2️⃣ **Interacting with a Smart Contract**

You can use **Cast** for direct terminal interaction or leverage **Etherscan’s** UI to read contract data and interact with smart contracts.

* **Managing Wallets**
  *   Import a wallet:

      ```bash
      cast wallet import mywallet --private-key $PRIVATE_KEY
      ```
  *   List available wallets:

      ```bash
      cast wallet list
      ```
  *   Delete a wallet:

      ```bash
      rm -rf ~/.foundry/keystores/mywallet
      ```
* **Calling Smart Contract Functions:**
  *   Read function:

      ```bash
      cast call --rpc-url $RPC_URL <CA> "isUserAllowed(address)(bool)" <Public Key>
      ```
  *   Convert hex to decimal:

      ```bash
      cast --to-base 0x15b7d6 dec
      ```
* **Write function**
  *   Send a transaction:

      ```bash
      cast send --rpc-url $RPC_URL <CA> "addToAllowList(address)" "<Public Key>" --private-key $PRIVATE_KEY
      ```
  *   Send a transaction with multiple arguments:

      ```bash
      cast send --account mywallet --rpc-url $RPC <CA> "createMatrix(uint256,uint256)" 10 10
      ```
  *   Call a contract function and retrieve a stored value:

      ```bash
      cast call --rpc-url $RPC $DST "val()(uint256)"
      ```

#### **3️⃣ Understanding the Dual-Block Architecture**

Hyperliquid EVM uses a **dual-block system** for transaction processing. By default, transactions go to **small blocks**, but deploying contracts efficiently may require **big blocks**. To enable this, submit an **L1 action**.

💡 **For a deep dive into Dual-Block transactions**, visit **this** [**guide**](../hyperevm-specificities.md#id-2.-dual-block-architecture).

***

### **3. dApp <--> Blockchain**

To interact with a smart contract from your dApp’s frontend, you can use **Ethers.js**, **Viem**, or **Wagmi**. These tools allow you to read and write blockchain data, handle transactions, and manage wallet connections.

#### **1️⃣ Setting Up the Contract ABI & Address**

* **Extract the ABI from Foundry output**:\
  The ABI is located in `out/ContractName.sol/ContractName.json`.
*   **Store the contract address** as a constant:

    ```bash
    const CONTRACT_ADDRESS = "0xYourContractAddress";
    const contractABI = [{}]
    import contractABI, CONTRACT_ADDRESS from "@/lib/config/abi.ts";
    ```

***

#### **2️⃣ Using Ethers.js**

📌 **Documentation:** [Ethers.js Docs](https://docs.ethers.org/v6/getting-started/)

```bash
npm install ethers
```

**🔹 Read Data (Call a View Function)**

```jsx
import { ethers } from "ethers";

async function readContract() {
  const provider = new ethers.JsonRpcProvider("https://your-rpc-url.com");
  const contract = new ethers.Contract(CONTRACT_ADDRESS, contractABI, provider);
  const value = await contract.yourViewFunction();
  console.log("Contract Value:", value);
}
```

**🔹 Write Data (Send a Transaction)**

```jsx
async function writeContract(signer) {
  const contract = new ethers.Contract(CONTRACT_ADDRESS, contractABI, signer);
  const tx = await contract.yourWriteFunction("param1", "param2");
  await tx.wait();
  console.log("Transaction confirmed:", tx.hash);
}
```

***

#### **3️⃣ Using Viem**

📌 **Documentation:** [Viem Docs](https://viem.sh/docs/getting-started)

```bash
npm i viem
```

**🔹 Read Data (Call a View Function)**

```jsx
import { createPublicClient, http } from "viem";
import { mainnet } from "viem/chains";

const client = createPublicClient({
  chain: mainnet,
  transport: http(),
});

async function readContract() {
  const data = await client.readContract({
    address: CONTRACT_ADDRESS,
    abi: contractABI,
    functionName: "yourViewFunction",
  });
  console.log("Contract Value:", data);
}
```

**🔹 Write Data (Send a Transaction)**

```jsx
import { createWalletClient } from "viem";

async function writeContract(account) {
  const client = createWalletClient({
    account,
    chain: mainnet,
    transport: http(),
  });

  const txHash = await client.writeContract({
    address: CONTRACT_ADDRESS,
    abi: contractABI,
    functionName: "yourWriteFunction",
    args: ["param1", "param2"],
  });

  console.log("Transaction Hash:", txHash);
}
```

***

#### **4️⃣ Using Wagmi**

📌 **Documentation:** [Wagmi Docs](https://wagmi.sh/react/getting-started)

```bash
npm install wagmi viem@2.x @tanstack/react-query
```

**🔹 Setting Up Wagmi Config -** [**here**](dapp-setup.md#id-1.-setting-up-your-application)

**🔹 Read Data (Use Wagmi Hook)**

```jsx
import { useReadContract } from "wagmi";

const { data, isLoading } = useReadContract({
  address: CONTRACT_ADDRESS,
  abi: contractABI,
  functionName: "yourViewFunction",
});
```

**🔹 Write Data (Use Wagmi Hook)**

```jsx
import { useWriteContract } from "wagmi";

const { writeContract } = useWriteContract();

async function sendTx() {
  writeContract({
    address: CONTRACT_ADDRESS,
    abi: contractABI,
    functionName: "yourWriteFunction",
    args: ["param1", "param2"],
  });
}
```

You can use **Wagmi Core** instead of React hooks. Hooks must follow React rules (e.g., they cannot be called inside functions or conditionally).

🔗 **Learn more:** [Wagmi Core Documentation](https://wagmi.sh/core/getting-started)
