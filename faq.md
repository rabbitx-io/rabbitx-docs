---
description: Frequently Asked Questions
---

# Frequently Asked Questions

### What are ZK Rollups?

ZK Rollups refers to zero-knowledge rollups, a concept conceived of in 1985 and now the premiere and best means of scaling Ethereum. ZK rollups are a hybrid scaling solution on the Ethereum mainnet that increases throughput and lowers transaction costs. **ZK-rollups** bundle (or 'roll up') transactions into batches that are executed offchain. Offchain computation reduces the amount of data that has to be posted to the blockchain. ZK-rollup operators submit a summary of the changes required to represent all the transactions in a batch rather than sending each transaction individually.&#x20;

### Wen token?

RBX token has been announced. The ERC20 contract address is `0x3Ba925fdeAe6B46d0BB4d424D829982Cb2F7309e` . Please read this twitter announcement for more details [https://twitter.com/rabbitx\_io/status/1651800369578790913](https://twitter.com/rabbitx\_io/status/1651800369578790913).

### Where can I find the RabbitX API?

Trading APIs are available at [Broken link](broken-reference "mention")

### How did you come up with the name RabbitX

RabbitX is fun and fast as hell. Also, bunnies are adorable.

### What do I need to do to start trading?

Simply deposit through your wallet and you're ready to start trading!

### Can anyone trade?

Yes! As long as you have a wallet, you can deposit on the exchange and start trading. We're completely permissionless.

### Will there be a trader rewards program?

Yes. Coming soon :tm:

### What is TradingView?

TradingView is one of the world’s leading charting and trading platforms, offering an array of technical, drawing and analytical tools. Supercharged by robust technologies across browser, desktop and mobile apps, the platform provides unparalleled access to live data, e.g. [BTC USD](https://www.tradingview.com/symbols/BTCUSD/) and [ETH USD](https://www.tradingview.com/symbols/ETHUSD/), the latest news, financial reports, and integrations with selected brokers. Visit TradingView [here](https://www.tradingview.com/).

### Why am I experiencing the "POST\_CHECK\_MARGIN" error?

Please read our [Margin Calculation ](margin-calculation.md#faq-why-cant-i-close-my-position-and-i-see-a-post-match-error)documentation for more details.

### How does your liquidation engine work?

RabbitX employs a partial liquidation strategy that minimises the negative impact of liquidations on users. Check out this [link](liquidations.md) for more information.

### Why is my market order unfilled?

To protect traders from adverse price movements when executing a market order, if the execution price of a market order deviates beyond 5%, the exchange will automatically place the remaining unfilled portion of the order at 5% away from the fair price.

### What is market leverage?

You can choose a different leverage for each market. For example, you can choose a market leverage of 20x for BTC-USD and a market leverage of 5x for ETH-USD. Your account leverage is your current account open positions notional / account equity. Market leverage is applied to your open positions and active orders in that market.

### What is withdrawable balance?

Withdrawable balance is the amount available for withdrawal. It is min(wallet balance, account equity) - order margin - position margin. You will not be able to place new orders if your withdrawable balance is 0.

### What are fair price and market price?

Fair price is the price used to mark your position unrealised P\&L. Market price is the mid price between the current best bid and best offer.

### Why hasn't my withdrawal arrived yet?

Please note the process for withdrawals:

* The withdrawn amount will be immediately deducted from your wallet balance on RabbitX.
* You will see the withdrawn amount initially displayed as 'Pending' in your 'Transfers' tab.
* In 'Transferring' status, your withdrawal is now being processed.
* You will then be able to claim your requested withdrawal amount back to your wallet. You must initiate the claim and sign the transaction from the 'Transfers' tab.

<figure><img src=".gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure>

