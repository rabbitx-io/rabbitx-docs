# Get Started

### **Connect your wallet**

* Visit [https://app.rabbitx.io](https://testnet.rabbitx.io)
* Enter the access code (you can get the access code from our Discord https://discord.com/invite/rabbitx)
* Click the "Connect Wallet" button in upper-right corner:

![](<.gitbook/assets/image (8).png>)

* Connect your Metamask wallet > switch to "Ethereum network" > Sign and verify to ownership of your wallet
* If you don't have a web3 wallet, you can download Metamask here [https://metamask.io/download/](https://metamask.io/download/)

### **Trading**

* Deposit USDT via the 'deposit' button
* The order panel is in the right hand side. There you can input your order type, limit price (if applicable), and the size of your trade.

<img src=".gitbook/assets/image (16).png" alt="" data-size="original">

### **Review your positions, trades and orders**

* At the bottom of the page you will see your completed and open orders under the Orders option
* Clicking the Positions tab will show your current positions on RabbitX
* Clicking the Account tab shows your account balances, margin requirement, PnL, leverage, and volume figures

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## **FAQs**

**Q:** How do I deposit collateral to start trading?

**A:** You must deposit USDT-ERC20 to start trading

**Q:** Do I need to pay gas to trade?

**A:** You do not need to pay gas for trading. However you will need to pay gas for depositing and withdrawals.

**Q:** Why am I interacting on an Ethereum if you’re on Starknet?

**A:** Deposits and withdrawals on RabbitX are done on Ethereum layer 1. RabbitX then uses Starknet for settlement service to handle your deposits and withdrawals. Using our L1-to-L2 Link, we conveniently take care of all the backend processes for you. This is why you can use an EVM wallet with us and don’t have to use a cairo-specific wallet.&#x20;

**Q:** Why do withdrawals take so long?

Withdrawals may take up to 12 hours, the length of time for a new batch of transactions to be confirmed from Starknet to Ethereum. Please note the process for withdrawals, in order of occurrence:

* Your wallet balance on RabbitX will be immediately deducted by the withdrawn amount
* You will see the withdrawn amount display initially as “Pending” in your Transfers tab
* Once the withdrawal is accepted by Starknet, the status will change to “Transferring”
* In “Transferring” status, your withdrawal is now being processed by Starknet. Depending on Starknet’s block time this process currently takes up to 12 hours, with an estimated time of 6-10 hours.
* Once completed, the transfer status will change to “Success” in your Transfers tab
* You will be able to claim your requested withdrawal amount back to your wallet

**Q:** Why do my market orders sometimes not immediately fill?

**A:** To protect traders from adverse price movements when executing a market order, if the execution price of a market order deviates beyond 5%, the exchange will automatically place the remaining unfilled portion of the order at 5% away from the fair price
