---
description: Frequently Asked Questions
---

# Frequently Asked Questions

### Where can I find the RabbitX API?

Trading APIs are available at [Broken link](broken-reference "mention")

### What do I need to do to start trading?

Simply deposit through your wallet and you're ready to start trading!

### Can anyone trade?

Yes! As long as you have a wallet, you can deposit on the exchange and start trading. We're completely permissionless.

### Why am I experiencing the "POST\_CHECK\_MARGIN" error?

Please read our [Margin Calculation ](margin-calculation.md#faq-why-cant-i-close-my-position-and-i-see-a-post-match-error)documentation for more details.

### How do I set a TP (Take Profit) and SL (Stop Loss)?

Take Profit (TP) and Stop Loss (SL) can be set after the opening of a position.

<figure><img src=".gitbook/assets/Screenshot 2025-01-14 at 16.58.26.png" alt=""><figcaption></figcaption></figure>

### Why am I experiencing the "POST\_MATCH\_ERROR\_WB" error?

This message means that placing the order would put your account in a negative margin, leading to an instant liquidation. To avoid this, you should reduce your position size or increase your leverage.

### Why am I experiencing the "Invalid payload signature" error?

This error occurs when your session has expired or the payload signature is invalid. To resolve it, simply sign out and log back in to refresh your session.

### Why am I experiencing the "Take Profit must be >/\<x" error?

For short positions, the Take Profit (TP) must be set below the fair price (FP). Similarly, for long positions, the TP must be set above the FP. This rule prevents immediate execution of the order at an undesirable price. Adjust your TP to ensure it complies with the fair price logic.

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

### What if I still can't find the answer I need?

If you need further assistance, please open a ticket on our Discord channel [here](https://discord.com/invite/rabbitx), and our team will get back to you as soon as possible.

