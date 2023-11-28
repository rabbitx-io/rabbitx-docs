# Orderbook

## Orderbook

Get market orderbook snapshot.

```
GET /markets/orderbook
```

```json
Params
{
market_id: "BTC-USD"
p_limit: 100, // max 1000
p_page: 0, // page starts at 0
p_order: "DESC" // default "DESC" for descending and "ASC" for ascending
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

### Guide to managing a local orderbook

1. Open a stream to **wss://api.prod.rabbitx.io/ws**
2. You will receive an orderbook snapshot on initial subscribe
3. Subsequent websocket events from the orderbook channel will give orderbook updates
4. Use the sequence number to keep track&#x20;
5. If a sequence number is skipped, get a depth snapshot from **https://api.prod.rabbitx.io/markets/orderbook**
6. Drop any event where sequence is <= sequence in the snapshot
7. The data in each event is the **absolute** quantity for a price level
8. If the quantity is 0, **remove** the price level
