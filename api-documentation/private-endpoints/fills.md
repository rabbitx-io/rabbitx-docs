# Fills

### Get fills

Get account fills. Filter by market or start\_time, end\_time.

```
GET /fills
```

```json
Parameters
{
    market_id: 'BTC-USD'    // (optional)
    start_time: 1669629461258298  // (optional) timestamp in microseconds
    end_time: 1669629461258298  // (optional) timestamp in microseconds
    p_limit: 100, // max rows returned, max 1000
    p_page: 0, // pagination page, index begins at 0
    p_order: "DESC" // default "DESC" for descending and "ASC" for ascending
}
```

```json
Example response:
{
    "success": true,
    "error": "",
    "result": [
            {'fee': '-0.0178801',
              'id': 'BTC-USD-62581592',
              'is_maker': False,
              'liquidation': False,
              'market_id': 'BTC-USD',
              'order_id': 'BTC-USD@6509736',
              'price': '25543',
              'profile_id': 7615,
              'side': 'short',
              'size': '0.001',
              'timestamp': 1676648452088704,
              'trade_id': 'BTC-USD-62581590'},
             {'fee': '-0.0178801',
              'id': 'BTC-USD-62581571',
              'is_maker': False,
              'liquidation': False,
              'market_id': 'BTC-USD',
              'order_id': 'BTC-USD@6509702',
              'price': '25543',
              'profile_id': 7615,
              'side': 'short',
              'size': '0.001',
              'timestamp': 1676648322405711,
              'trade_id': 'BTC-USD-62581569'}
    ]
}
```

Tip: Fills are indexed by timestamp; if start\_time is not specified, the response will take longer as it will parse through your full order history. Queries with start\_time parameter could be up to 10x faster than queries without start\_time.

### Get fills by order id

Get all account fills for a single order id.

```
GET /fills/order
```

```
Parameters
{
    order_id: 'BTC-USD@445126'  // (required)
}
```

```json
Example response:
{
    "success": true,
    "error": "",
    "result": [
            {'fee': '-0.0178801',
              'id': 'BTC-USD-62581592',
              'is_maker': False,
              'liquidation': False,
              'market_id': 'BTC-USD',
              'order_id': 'BTC-USD@6509736',
              'price': '25543',
              'profile_id': 7615,
              'side': 'short',
              'size': '0.001',
              'timestamp': 1676648452088704,
              'trade_id': 'BTC-USD-62581590'},
             {'fee': '-0.0178801',
              'id': 'BTC-USD-62581571',
              'is_maker': False,
              'liquidation': False,
              'market_id': 'BTC-USD',
              'order_id': 'BTC-USD@6509702',
              'price': '25543',
              'profile_id': 7615,
              'side': 'short',
              'size': '0.001',
              'timestamp': 1676648322405711,
              'trade_id': 'BTC-USD-62581569'}
    ]
}j
```
