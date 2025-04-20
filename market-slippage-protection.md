# Market Slippage Protection

## Slippage Protection

RabbitX is committed to providing a secure and seamless trading experience. To protect traders from unintended order execution caused by fat-finger errors or extreme market volatility, we've implemented a Slippage Protection feature.

### What is Slippage Protection?

Slippage Protection ensures that if your order is placed significantly away from the current market price, it will automatically be adjusted to an improved price level within a defined slippage tolerance. This protects your trades from excessive slippage and unintended market impacts.

### How Does Slippage Protection Work?

When you place an order, RabbitX automatically applies the following price caps to prevent excessive slippage. The maximum allowable slippage tolerance for each market is dynamically set to&#x20;

Maximum Slippage = min(Maintenance Margin) / 2

This ensures that the higher the leverage, the lower the slippage tolerance, protecting your positions precisely when you need it the most.

### Benefits of Slippage Protection

* **Avoid Fat-Finger Mistakes**: Prevent unintended large losses due to accidental incorrect order placement.
* **Better Price Execution**: Enjoy better price executions especially during volatile market conditions.

With RabbitX's Slippage Protection, trade confidently knowing that your risk is effectively managed, allowing you to focus on making strategic trading decisions.
