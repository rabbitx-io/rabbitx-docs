# Liquidations

The Rabbit<mark style="color:red;">X</mark> risk-management engine is based on rigorous research and testing to ensure fair and orderly liquidations. The Rabbit<mark style="color:red;">X</mark> cutting-edge risk model is built to protect both our traders and the exchange.&#x20;

### Margin Requirements

<table><thead><tr><th>Name</th><th>Account Margin</th><th data-hidden>Initial Margin</th></tr></thead><tbody><tr><td>Full Liquidation Margin</td><td>2%</td><td>5%</td></tr><tr><td>Partial Liquidation Maintenance Margin</td><td>3%</td><td>5%</td></tr></tbody></table>

### Liquidation Waterfalls

Rabbit<mark style="color:red;">X</mark> utilizes a 3-step waterfall structure to process liquidations.&#x20;

#### Waterfall #1

When an account's equity falls below the maintenance margin requirement it will undergo partial liquidation until the account is back above the maintenance margin requirement. While in liquidation, users will not be able to place new orders, cancel orders, or withdraw funds. When the account's equity is back above the maintenance margin requirement, it will no longer be in liquidation.&#x20;

#### Waterfall #2

If an account's equity falls below the liquidation margin, the account will be fully liquidated at the zero-price. A portion of the remaining collateral (if any) will go to the Insurance Fund. If Rabbit<mark style="color:red;">X</mark> is unable to liquidate the position at a price better than the zero-price, the losses will be taken by the Insurance Fund.

#### Waterfall #3

If Rabbit<mark style="color:red;">X</mark> Insurance Fund equity falls below zero, then opposing positions will be auto-deleveraged at the Insurance Fund zero-price. Auto-deleveraging is the final step taken only when the Insurance Fund equity falls below zero. Rabbit<mark style="color:red;">X</mark> takes every possible step to avoid auto-deleveraging and has implemented an algorithm to minimize the impact of auto-deleveraging when it does occur.&#x20;



Read more about the [Insurance Fund](insurance-fund.md).&#x20;

Zero-price is the price of the position that sets the account equity to zero.

Refer to our [Index Price](index-price.md) section for more details.&#x20;

_Notes:_\
_1. While RabbitX aims to reduce the likelihood of auto-deleveraging to a minimum, it is still possible._\
_2. Estimated liquidation price is only an estimate. When an account gets liquidated will depend on multiple factors including the fair price, performance of all contracts, the currency your collateral is in, among other factors._\
_3. US residents are restricted from using Rabbit<mark style="color:red;">X</mark>._\
_4. None of this is investment advice._\
__
