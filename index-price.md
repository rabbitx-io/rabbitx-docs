# Index Price

Rabbit<mark style="color:red;">X</mark> uses an index price to calculate the hourly funding rate. The index price aims to track the underlying spot market price. For example, the Bitcoin index price tracks the price of spot Bitcoin on multiple spot exchanges.

### Index Calculation Methodology

Rabbit<mark style="color:red;">X</mark> index price is calculated as a median of the market prices of multiple constituent exchange. Constituent exchange candidates include both centralized and decentralized exchanges.

#### Index price protection mechanism

* **Unresponsive price source:** If any price source is unresponsive, or returns an error, the price source is removed until we start receiving accurate prices again.&#x20;
* **Single price source deviation:** If any price source deviates more than 5% from the median, the price source is removed.&#x20;

### Fair Price Calculation

The fair price is used to calculate trader positions' unrealized profit and loss (PnL). The unrealized PnL is used in calculation of the trader's account equity and account margin.&#x20;

_Note:_

_Rabbit<mark style="color:red;">X</mark> uses a proprietary protection mechanism to prevent and discard malformed, anomalous, or inaccurate data. For the avoidance of doubt, and in accordance with the Rabbit<mark style="color:red;">X</mark> Terms of Service, Rabbit<mark style="color:red;">X</mark> accepts no responsibility for the accuracy of the data received from any exchange, and carries no liability whatsoever for any claimed losses arising in connection with its calculation and publication of such index._&#x20;

__
