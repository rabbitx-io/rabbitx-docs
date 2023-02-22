# Funding Rate

### Calculation

```
Funding Payment = Position Notional * Funding Rate 

where
Funding Rate = 1-hour TWAP(Basis) / 24
Premium = (Market Price - Spot Index Price) 
Basis = Premium / Spot Index Price
```

#### Explanation

When the perpetual contract is trading above the spot index price over a 1-hour TWAP, the funding rate is positive, and shorts will receive funding payments that are paid for by longs. Conversely, when the perpetual contract is trading below the spot index price over a 1-hour TWAP, the funding rate is negative, and longs will receive funding payments that are paid for by shorts.&#x20;

When the funding rate is positive, longs pay shorts. When the funding rate is negative, shorts pay longs. You will only pay or receive funding if you hold a position at the time funding is paid. Funding is paid at the start of every hour.

Rabbit<mark style="color:red;">X</mark> does not charge any fees on funding.&#x20;

#### Funding rate caps

Rabbit<mark style="color:red;">X</mark> imposes a funding rate cap to prevent market manipulations. The absolute funding rate is capped at 1% per hour.
