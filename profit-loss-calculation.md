# Profit / Loss Calculation

## Perpetual Contracts

### Trading P\&L

Jon is long 100 BTC with an average price of $10,000. The fair price of BTC-USD is currently $10,250. His unrealized P\&L is equal to:

```
Unrealised Profit = 100 * ($10,250 - $10,000) = $25,000
```

Jon decides to sell 50 BTC at $10,300 and realise some profits. Jon's position decreases to 50 BTC, and his realised profit is:

```
Realised Profit = 50 * ($10,300 - $10,000) = $15,000
```

The realised P\&L is based on the price at which you close your position, which may be different from the fair price.

### Funding P\&L

For RabbitX perpetual contracts, there are hourly funding payments received and paid between long and short positions. When the funding rate is positive, longs pay funding and shorts receive funding. When the funding rate is negative, shorts pay funding and longs receive funding.&#x20;

```
Funding Received / Paid = Position Notional * Funding Rate
```

Jon is long 100 BTC, and the next funding rate is -0.01%. The fair price for BTC-USD at the time funding is paid is $10,000.

```
Funding Received = 100 * 10,000 * 0.01% = $100
```

You will only pay or receive funding if you hold a position at the time funding is paid. Funding is paid at the start of every hour. Funding P\&L is credited or deducted directly from your account balance.

View this [link](funding-rate.md) to see how the funding rate is calculated.
