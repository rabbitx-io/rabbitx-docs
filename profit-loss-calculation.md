# Profit / Loss Calculation

## Perpetual Contracts

### Trading PNL

Jon is long 100 BTC with an average price of $10,000. The fair price of BTC-USD is currently $10,250. His unrealized PnL is equal to:

```
Unrealized Profit = 100 * ($10,250 - $10,000) = $25,000
```

Jon decides to sell 50 BTC at $10,300 and realize some profits. Jon's position decreases to 50 BTC, and his realized profit is:

```
Realized Profit = 50 * ($10,300 - $10,000) = $15,000
```

Realized PnL is based on the price that you close your position, which may be different from the fair price.

### Funding PNL

For RabbitX perpetual contracts, there are hourly funding payments received / paid between long and short positions. When the funding rate is positive, longs pay funding and shorts receive funding. When the funding rate is negative, shorts pay funding and longs receive funding.&#x20;

```
Funding Received / Paid = Position Notional * Funding Rate
```

Jon is long 100 BTC and the next funding rate is -0.01%. The fair price for BTC-USD at the time funding is paid is $10,000.

```
Funding Received = 100 * 10,000 * 0.01% = $100
```

You will only pay or receive funding if you hold a position at the time funding is paid. Funding is paid at the start of every hour. Funding PnL is credited / deducted directly from your account balance.

View this [link](funding-rate.md) to see how the funding rate is calculated.
