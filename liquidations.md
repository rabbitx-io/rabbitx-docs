# Liquidations

The RabbitX risk-management engine is based on rigorous research and testing to ensure fair and orderly liquidations. The RabbitX cutting-edge risk model is built to protect both our traders and the exchange. RabbitX liquidations ensures a seamless trading experience that safeguards both the platform's integrity and user investments, maintaining a balanced and stable market environment.&#x20;

### Liquidation Process

RabbitX employs a comprehensive 2-step waterfall structure to efficiently handle liquidations. Our primary aim is to proactively mitigate potential risks associated with this process. The first step involves assessing the asset's value in real-time, ensuring that collateral requirements are met, thus averting unnecessary liquidations. Positions and unrealised profits/loss are calculated in real time using the fair price.&#x20;

#### What Happens During Liquidation?

* When your account falls below the maintenance margin of the position, your account enters a "liqudiating" state
* System automatically cancels all existing open orders
* Positions are gradually closed in small increments by a combination VWAP and TWAP algorithm. The process is designed to minimize market impact and protect the trader's capital.
* The liquidation process uses a combination of time-weighted average price (TWAP) and volume-weighted average price (VWAP) algorithms. The following description describes how the liquidation process works:
  * **Gradual unwinding process begins:**
    * Orders are placed in chunks of **10% of the position** per iteration.
    * Minimum order size is enforced ($1000 or 10% of the position, whichever is ).
    * Liquidation size is capped at **0.01% of the exchange’s 30-day ADV** (Average Daily Volume) to prevent excessive market impact.
    * The order is then split into five child orders and are placed strategically in the order book:
      * 1/5 at best offer +1 tick
      * 1/5 at best offer
      * 1/5 at best bid +1 tick
      * 2/5 hitting the best bid
    * If no bids or offers exist, the last index price is used as the reference.
* Process repeats every 6 seconds until the margin recovers above the maintenance margin. During this process, traders keep 100% of the proceeds and remaining positions.
* If prices drop much faster than the liquidation process is able to unwind the position, and if your margin falls below the auto-close margin fraction, the RabbitX insurance takes over your entire position at the zero price.

#### Margin Requirements

| Markets | Max Leverage | ACMF  | MMF  | IMF |
| ------- | ------------ | ----- | ---- | --- |
| BTC/ETH | 50x          | 0.5%  | 1%   | 2%  |
| Others  | 20x          | 1.25% | 2.5% | 5%  |

### Estimated Liquidation Price

The estimated liquidation price of positions on RabbitX follows the following formula:

$$
\boxed{ P_{\mathrm{liqBTC}} = \frac{ \sum \mathrm{MM}_{\text{other}} \;-\; \mathrm{AE} \;+\; \text{side}_{BTC}\,\bigl(M\,\mathrm{size}_{BTC}\bigr) }{ \mathrm{size}_{BTC}\,\bigl(\text{side}_{BTC} \;-\; \mathrm{MMF}\bigr) } }
$$

### Insurance Fund

If RabbitX Insurance Fund equity falls below zero, then opposing positions will be auto-deleveraged at the Insurance Fund zero-price. Auto-deleveraging is the final step taken only when the Insurance Fund equity falls below zero. RabbitX takes every possible step to avoid auto-deleveraging and has implemented an algorithm to minimise the impact of auto-deleveraging when it does occur.&#x20;

RabbitX uses an Insurance Fund to avoid auto-deleveraging in traders’ positions. The fund is used as a buffer for liquidation orders before they are taken over by the auto-deleveraging system.

The Insurance Fund grows from liquidations that were able to be executed in the market at a price better than the zero price of the liquidated position. If liquidations are executed at a price worse than the zero price, losses will be absorbed by the Insurance Fund.

If RabbitX Insurance Fund equity falls below zero, then opposing positions will be auto-deleveraged at the Insurance Fund zero-price. Auto-deleveraging is the final step taken only when the Insurance Fund equity falls below zero. RabbitX takes every possible step to avoid auto-deleveraging, including algorithmic efforts to minimise its impact when it does occur.&#x20;



Refer to our [Index Price](index-price.md) section for more details.&#x20;

_Notes:_\
_1. While RabbitX aims to reduce the likelihood of auto-deleveraging to a minimum, it is still possible._\
_2. The estimated liquidation price is only an estimate. When an account gets liquidated will depend on multiple factors, including the fair price, the performance of all the contracts, the currency your collateral is in, among other factors._\
_3. US residents are restricted from using RabbitX._\
_4. None of this is investment advice._\
