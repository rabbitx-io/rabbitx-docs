# Trades

## Trades

```
GET /trades
```

```json
Params
{
    market_id: "BTC-USD",
    p_limit: 100, // max rows returned, max 1000
    p_page: 0, // pagination page, index begins at 0
    p_order: "DESC" // default "DESC" for descending and "ASC" for ascending
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
