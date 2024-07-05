# Funding Rate

The Funding Rate is comprised of two parts: the **Interest Rate** and the **Premium Basis** . The funding rate aims to keep the traded price of the perpetual contract in line with the underlying reference price. The contract mimics how margin-trading markets work as buyers and sellers of the contract exchange interest payments periodically. RabbitX does not charge any fees on funding.&#x20;

### Calculation

<pre><code>Funding Payment = Position Notional * Funding Rate 

where
<strong>    Funding Rate = 1-hour TWAP(Premium Basis) / 8 + Interest Rate
</strong>    Premium = (Market Mid - Spot Index Price) 
    Premium Basis = Premium / Spot Index Price
</code></pre>

\*Basis is capped at +/- 2% from the index price unless specified otherwise

\*Funding rate is capped at 0.25% per hour unless specified otherwise

### Interest Rate Component

The Interest Rate is a function of interest rates between the base currency and the quote currency. For example, for BTC-USD the base currency would be BTC while the quote currency would be USD.&#x20;

```
Interest Rate (I) = (Quote Currency Interest - Base Currency Interest)
```

RabbitX uses a fixed Interest Rate for cryptocurrency markets of 0.125bps.

#### Explanation

When the perpetual contract is trading above the spot index price over a 1-hour TWAP, the funding rate is positive, and shorts will receive funding payments that are paid for by longs. Conversely, when the perpetual contract is trading below the spot index price over a 1-hour TWAP, the funding rate is negative, and longs will receive funding payments that are paid for by shorts.&#x20;

When the funding rate is positive, longs pay shorts. When the funding rate is negative, shorts pay longs. You will only pay or receive funding if you hold a position at the time funding is paid. Funding is paid at the start of every hour.

Funding rate is scaled to realise the premium basis over a period of 8 hours. That means, for example, that if a certain perpetual market trades consistently at a 0.1% premium relative to the underlying, long traders may expect to pay \~0.1% every 8 hours, and short traders may expect to earn a \~0.1% return every 8 hours (not accounting for the interest rate component).

#### Funding rate caps

RabbitX imposes a funding rate cap to prevent market manipulations. The absolute funding rate is capped at 0.25% per hour.
