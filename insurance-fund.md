# Insurance Fund

RabbitX uses an Insurance Fund to avoid auto-deleveraging in traders’ positions. The fund is used as a buffer for liquidation orders before they are taken over by the auto-deleveraging system.

The Insurance Fund grows from liquidations that were able to be executed in the market at a price better than the zero price of the liquidated position. If liquidations are executed at a price worse than the zero price, losses will be absorbed by the Insurance Fund.

If RabbitX Insurance Fund equity falls below zero, then opposing positions will be auto-deleveraged at the Insurance Fund zero-price. Auto-deleveraging is the final step taken only when the Insurance Fund equity falls below zero. RabbitX takes every possible step to avoid auto-deleveraging, including algorithmic efforts to minimize its impact when it does occur.&#x20;

