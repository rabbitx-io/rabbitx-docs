# Index Price

RabbitX uses an index price to calculate the hourly funding rate. The index price aims to track the underlying spot market price. For example, the Bitcoin index price tracks the price of spot Bitcoin on multiple spot exchanges.

### Index Calculation Methodology

RabbitX index price is calculated as the median of the market prices of multiple constituent exchanges. Constituent exchange candidates include both centralised and decentralised exchanges.

#### Index price protection mechanism

* **Unresponsive price source:** If any price source is unresponsive or returns an error, the price source is removed until we start receiving accurate prices again.&#x20;
* **Single price source deviation:** If any price source deviates more than 5% from the median, the price source is removed.&#x20;

### Fair Price Calculation

The fair price is used to calculate trader positions' unrealized profit and loss (P\&L) and also liquidations. The unrealized P\&L is used in the calculation of the trader's account equity and account margin.&#x20;

$$FairPrice=Median(Price_1, Price_2, MarketPrice)$$

$$Price_1=IndexPrice*(1+Average(60min\ basis))$$

$$Price_2=IndexPrice*(1+Average(30min\ basis))$$

Note: 30min, 60min basis is clamped within +/- 1%.

Our fair price uses a robust methodology in order to protect traders against unfair liquidations caused by 'scam wicks'.

_Note:_

_RabbitX uses a proprietary protection mechanism to prevent and discard malformed, anomalous, or inaccurate data. For the avoidance of doubt, and in accordance with the RabbitX Terms of Service, RabbitX accepts no responsibility for the accuracy of the data received from any exchange, and carries no liability whatsoever for any claimed losses arising in connection with its calculation and publication of such index._&#x20;

