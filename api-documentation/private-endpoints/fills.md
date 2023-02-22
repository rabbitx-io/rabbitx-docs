# Fills

### Get fills

Get account fills. Filter by market or start\_time, end\_time.

```
GET /fills
```

```json
Params:
{
    market_id: 'BTC-USD'    // (optional)
    start_time: 1623654624  // (optional)
    end_time: 1673668624    // (optional)
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

### Get fills by order id

Get all account fills for a single order id.

```
GET /fills/order
```

```
Params:
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
