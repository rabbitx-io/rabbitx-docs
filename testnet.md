# Get Started

### **Connect your wallet**

1. Visit [https://app.rabbitx.io](https://testnet.rabbitx.io)
2. Click the "Connect Wallet" button in upper-right corner

![](https://lh7-us.googleusercontent.com/IqZyJHRd2vuFjnamCDvjSHbZ7hCMOorvur9o8EfS4Qy5\_DlvmsEv2NgHS2qZFE7-t-7C6O0plHyx-DQTWQqexHnT\_5lKNWDWOFv3ZvYXNYEIBr9B43BvrR3JJJdXYp4ZcNoHnvjzi1hNMCFVd-5DUIs)

3. If you already have a metamask wallet, simply click “Metamask” at the connect page
4. If you don’t have a metamask wallet, you can register for a new wallet by clicking “Connect With Socials”

![](https://lh7-us.googleusercontent.com/50kk\_ftjea4OGch95yHq2z3DE2H9pjHbVDD4aOWOcwrUEVX0rqsLk1ywZ-V32LP-YVauKTLUwAZ3eUZroz6JV4sMuGG9gEm-6DXUKohscKmGJYHiD0084SjR-AU0hlDQB5T8Xdg9w3mxmaDJVeSr4Ps)

5. Next, click sign and verify to connect your decentralised wallet with the platform.

![](https://lh7-us.googleusercontent.com/LnNbgXiHEEmCtTNYoTcp8NdQvQAc8P0jxWQMZoyUzjIXE1ZgxAoFOdcDgmxuD-MzoPKShEy\_mpZHlZqXvHOHEj2VuUabR9xAzfn4jFRBRf70gSakeqbbJoQ4LpxJ0h8LaDyqvFfGxZsKpwlbIuk8C7A)

6. If you have connected with your email address, there will be a new Particle Wallet created for you. Copy the wallet address. You will need to deposit small amount of ETH to pay for gas fee. Next, deposit the USDT to your Particle Wallet.

![](https://lh7-us.googleusercontent.com/YVoNKn5C5R4vxfPMo4DaJEUbzc-IH1FKbrfnUabldXYmg4kdM0Xoa8yBx8rOCXS0nW35KAU4e3wwEQnxaybgZGW\_bfAckFhl\_dCrlsLGw4ip7laWTiG1\_A399hStPYFPcep3Fi7p0gGOxSnaQePR8V0)

7. Next, deposit USDT to start trading by clicking on the “Deposit” button. Deposits will be automatically in your exchange balance after 16 confirmations on Ethereum chain.

![](https://lh7-us.googleusercontent.com/txRnD7WzNwtr2slTM-xXGUBpXvYd0oLN32NruBTByMVeroltChKk\_C7-sWueJYoBLCNIpXc6wEr8oBDzqUjcTkFFHZY\_b-p-x-0jbf8Tb7t2WP9Szve0JSqZfOxK0fEFoapYdSqpGmc6htnDYxxIu9Q)

### **Trading**

* Deposit USDT via the 'Deposit' button
* The order panel is in the right hand side. There you can input your order type, limit price (if applicable), and the size of your trade.
* You can also right click on a price level of the orderbook to quickly place a trade at that price.&#x20;

![](<.gitbook/assets/image (25).png>)

* RabbitX also features advanced chart trading features that allows you to right click on the chart to place trades! You will also be able to see your positions and orders directly from the chart. Learn more about our [chart trader](chart-trader.md).

<figure><img src=".gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

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
