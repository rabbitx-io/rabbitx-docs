# Orders

### Get account order status

Get your account orders

```
GET /orders
```

```json
Params
{
    status: 'open',            // (optional) 'open', 'closed', 'canceled', 'rejected', 'processing', 'amending', 'cancelingall', 'canceling'
    market_id: 'BTC-USD',      // (optional)
    start_time: 1673668624     // (optional)
    end_time: 1673668624       // (optional)
}
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": [
           {'id': 'BTC-USD@1777',
            'initial_size': '1',
            'market_id': 'BTC-USD',
            'order_type': 'market',
            'price': '21210',
            'profile_id': 4,
            'reason': '',
            'side': 'long',
            'size': '1',
            'status': 'open',
            'timestamp': 1669629461258298,
            'total_filled_size': '0'},
           {'id': 'BTC-USD@1777',
            'initial_size': '1',
            'market_id': 'BTC-USD',
            'order_type': 'market',
            'price': '21210',
            'profile_id': 4,
            'reason': '',
            'side': 'long',
            'size': '1',
            'status': 'open',
            'timestamp': 1669629461258298,
            'total_filled_size': '0'}
    ]
}
```

### Place orders

Submitted orders will immediately return a response that the order is in "processing" state and will include an order ID. To verify the status of the order is "confirmed", we recommend subscribing to the accounts websocket channel. Alternatively, check the order status by the order ID.

```
POST /orders
```

```json
Params
{
    market_id: 'BTC-USD',
    price: 19800,
    side: 'long',    // accepts 'long' or 'short'
    size: 0.45, 
    type: 'limit'    // accepts 'market' or 'limit'
}
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": [
        {'id': 'BTC-USD@1848',
        'is_liquidation': False,
        'market_id': 'BTC-USD',
        'price': '10000',
        'profile_id': 4,
        'side': 'long',
        'size': '1',
        'status': 'processing',
        'type': 'limit'}
    ]
}
```

To keep an orderly market, RabbitX has a 1,000 open order limit per account.

### Cancel orders

```
DELETE /orders
```

```json
Params
{
    order_id: 'BTC-USD@1859'
    market_id: 'BTC-USD'
}
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": [
        {'id': 'BTC-USD@1859',
         'market_id': 'BTC-USD',
         'profile_id': 4,
         'status': 'canceling'}
    ]
}

```

### Amend orders

```
PUT /orders
```

```json
Params
{
    order_id: 'BTC-USD@1872',
    market_id: 'BTC-USD'
    price: 19800,
    size: 0.45, 
}
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": [
        {'id': 'BTC-USD@1872',
        'market_id': 'BTC-USD',
        'price': '10001',
        'profile_id': 4,
        'size': '2',
        'status': 'amending'}
    ]
}
```

### Cancel all orders

```
DELETE /orders/cancel_all
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": []
}
```
