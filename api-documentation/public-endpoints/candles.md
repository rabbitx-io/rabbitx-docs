# Candles

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
