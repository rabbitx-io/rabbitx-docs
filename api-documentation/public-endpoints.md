# Public Endpoints

## General Info

*   The base REST endpoint for testnet:

    ```go
    https://api.testnet.rabbitx.io
    ```
*   The websocket endpoint for testnet:

    ```go
    wss://api.testnet.rabbitx.io/ws
    ```
* All endpoints return either a JSON object or an array.
* All private endpoints require onboarding first.

### Reference implementation

Python: [https://github.com/rabbitx-io/rabbitx-python-client](https://github.com/rabbitx-io/rabbitx-python-client)

Examples: [https://github.com/rabbitx-io/rabbitx-python-client/tree/main/examples](https://github.com/rabbitx-io/rabbitx-python-client/tree/main/examples)

#### Python Installation

```bash
git clone https://github.com/rabbitx-io/rabbitx-python-client.git
cd rabbitx-python-client
pip install .
```

## Market Info

Get basic market info and metadata.

```
GET /markets
```

<pre class="language-json"><code class="lang-json">Params
{
<strong>market_id: "BTC-USD"    // (optional) "BTC-USD", "ETH-USD", "SOL-USD"
</strong>}
</code></pre>

```go
Response
{
	market_id           string
	status              string
	min_initial_margin  string
	forced_margin       string
	liquidation_margin  string
	min_tick            string
	min_order           string
	best_bid            string
	best_ask            string
	market_price        string
	index_price         string
	last_trade_price    string
	fair_price          string

	last_trade_price_24high              string
	last_trade_price_24low               string
	average_daily_volume                 string
	instant_funding_rate                 string
	instant_daily_volume                 string
	last_funding_rate                    string
	market_price_24h_change_premium      string
	market_price_24h_change_basis        string
	average_daily_volume_change_premium  string
	average_daily_volume_change_basis    string
	average_daily_volume_q		     string

	last_update_time         int64 
	last_update_sequence     int64 
	last_funding_update_time int64
}
    
```

## Trades

```
GET /trades
```

```json
Params
{
market_id: "BTC-USD",
limit: 100,
}
```

{% code overflow="wrap" %}
```go
Response
{
	id            string 
	market_id     string 
	timestamp     int64  
	price         string 
	size          string 
	liquidation   bool   
	taker_size    string // "long", "short"
}
```
{% endcode %}

## Orderbook

Get market orderbook snapshot.

```
GET markets/orderbook
```

```json
Params
{
market_id: "BTC-USD"
}
```

```go
Response 
{
	market_id string               
	bids      [string, string]  // returns array of (price, quantity)
	asks      [string, string]  // returns array of (price, quantity)
	sequence  uint                 
	timestamp int64               
}
```

## Candles

Get candles data.

```
GET /candles
```

```json
Params
{
market_id: "BTC-USD",
timestamp_from: 1662807004,
timestamp_to: 16638930040,
period: 5 // one of 1, 5, 15, 30, 60, 240, 1440
}
```

```go
Response
{
	time   int64 
	low    string
	high   string
	open   string
	close  string
	volume string
}
```

__

_Notes:_\
_The following documentation is provided as-is and Rabbit<mark style="color:red;">X</mark> accepts no responsibility for the accuracy of the data received, and carries no liability whatsoever for any claimed losses arising in connection with inaccuracies with the API._&#x20;
