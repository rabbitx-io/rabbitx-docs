# Margin Calculation

RabbitX uses a state-of-the-art risk system that seamlessly and efficiently simulates orders post-match with unmatched precision and speed, ensuring real-time atomic safety checks for every order placement in a high-performance, in-memory copy of the matching engine. Our matching engine does all of this without missing a beat. We call this our CoreGuard Risk Engine by RabbitX.&#x20;

### Margin Calculation

$$
AccountMargin=AccountEquity/TotalPositionNotional
$$

$$
TotalPositionNotional=\sum (Qty*fairPrice)
$$

$$
WalletBalance = Deposits - Withdrawals + RealizedPnL - Fees + Funding
$$

$$
Withdrawalable Balance = min(Account Equity, Wallet Balance) - Order Margin - Position Margin
$$

$$
PositionMargin=\sum(PositionQty*Price_{market})/Leverage_{market}
$$

$$
OrderMargin=\sum(OrderQty_{market}*Price_{market})/Leverage_{market}
$$ 

### Risk Checks
1. When an order is placed, our risk engine calculates the required Order Margin based on the leverage selected by the user for the market (note: to give users more flexibility for their risk management, leverage is set independently for each market). 
2. The order is then simulated in our CoreGuard Risk Engine, and the Account Margin, Position Margin, Order Margin are all recalculated based on the post-match simulation.
3. If the order results in the account Withdrawable Balance < 0 OR the account margin < 3% then the order is rejected. 

#### FAQ: Why am I seeing a post-match: WB = -xxx error?
This is due to insufficient Withdrawable Balance in your account. You can try the following to increase your Withdrawable Balance:
1. Cancel open orders (this will free up Order Margin)
2. Increase your market leverage  (this will reduce your Order Margin)
3. Try to deposit more funds
4. Close some positions (this will reduce your Position Margin)

#### FAQ: Why can't I close my position and I see a post-match error?
Unfortunately, due to the very strict nature of our CoreGuard Risk Engine, if the order placed results in a negative Withdrawable Balance, your order will be rejected. Try the following to increase your Withdrawable Balance:

1. Cancel open orders (this will free up Order Margin)
2. Increase your market leverage  (this will reduce your Order Margin)
3. Try to deposit more funds
4. Use market order to close some positions (this will decrease your post-match Position Margin)

Note: We understand some users are still experiencing an issue even if their account leverage is 20x and do not have any open orders. Our team is working hard to upgrade the CoreGuard Risk Engine to allow closing orders to be accepted as long as the order is immediately executable to reduce the position.
