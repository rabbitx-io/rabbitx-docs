# Trades

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
