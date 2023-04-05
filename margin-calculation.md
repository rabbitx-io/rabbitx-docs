# Margin Calculation

RabbitX uses a state-of-the-art risk system that seamlessly and efficiently simulates orders post-match with unmatched precision and speed, ensuring real-time atomic safety checks for every order placement in a high-performance, in-memory copy of the matching engine. Our matching engine does all of this without missing a beat. We call this our CoreGuard Risk Engine by RabbitX.&#x20;

### Margin Calculation

$$
AccountMargin\%=AccountEquity/TotalPositionNotional
$$

$$
PositionMargin=\sum(PositionQty*Price_{market})/Leverage_{market}
$$

