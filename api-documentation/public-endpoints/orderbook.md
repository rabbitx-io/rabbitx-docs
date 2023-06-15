# Orderbook

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

### Guide to managing a local orderbook

1. Open a stream to **wss://stream.binance.com:9443/ws/bnbbtc@depth**
2. Buffer the events you receive from the stream
3. Get a depth snapshot from \*\*[https://www.binance.com/api/v1/depth?symbol=BNBBTC\&limit=1000](https://www.binance.com/api/v1/depth?symbol=BNBBTC\&limit=1000)"
4. Drop any event where `u` is <= `lastUpdateId` in the snapshot
5. The first processed should have `U` <= `lastUpdateId`+1 **AND** `u` >= `lastUpdateId`+1
6. While listening to the stream, each new event's `U` should be equal to the previous event's `u`+1
7. The data in each event is the **absolute** quantity for a price level
8. If the quantity is 0, **remove** the price level
9. Receiving an event that removes a price level that is not in your local order book can happen and is normal.
