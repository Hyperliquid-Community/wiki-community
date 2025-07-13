---
icon: bridge-circle-check
---

# Bridge

The **Hyperliquid Bridge** connects the **Hyperliquid L1** and the **EVM Arbitrum chain**, providing a secure and efficient mechanism for transferring assets between these two ecosystems.

***

### **Key Features** 🛡️

* **Validator-Secured Bridge:**
  * The bridge is secured by the same **validator set** as the Hyperliquid L1.
  * Deposits and withdrawals require signatures from **more than 2/3 of the staking power** to ensure security.
* **Deposit Process:**
  * Deposits to the bridge are **signed by validators** on the L1.
  * Once validated by **2/3 of the staking power**, the deposit is credited on the bridge.
* **Withdrawal Process:**
  1. **Escrow on the L1:** Withdrawals are immediately locked on the L1 upon request.
  2. **Validator Signatures:** Validators sign the withdrawal as separate L1 transactions.
  3. **EVM Bridge Interaction:** When 2/3 of the staking power signs the withdrawal, an EVM transaction can be sent to the bridge to complete the process.
* **Dispute Protection:**
  * After a withdrawal is requested, there is a **dispute period** to detect and block malicious withdrawals that do not match the L1 records.
  * If needed, the bridge can be locked using **cold wallet signatures** from **2/3 of stake-weighted validators**.
* **Finalization:**
  * After the dispute period, finalization transactions distribute the **USDC** to the appropriate destination addresses.

***

### **Additional Features**

* **Validator Management on the Bridge:**\
  The bridge maintains an active validator set with their corresponding stake, ensuring synchronization with the Hyperliquid L1.
* **No Arbitrum ETH Requirement for Withdrawals:**
  * Users do not need to provide Arbitrum ETH for gas fees.
  * Instead, a **withdrawal fee of 1 USDC** is paid on the L1 to cover validator costs.
* **Audited for Security:**\
  The bridge logic, in conjunction with L1 staking, has been **audited by Zellic**.
  * For more details, see the [Hyperliquid GitHub repository](https://github.com/hyperliquid-dex) and the audit reports.
