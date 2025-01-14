# Orders

### Get account order status

Get your account orders.

> Update 13 December 2024: The endpoint now requires **`market_id`** to be included when querying an order by **`client_order_id`**. This change ensures faster and more accurate query performance.

```
GET /orders
```

```json
Parameters
{
    order_id: 'BTC-USD@1777'   // (optional)
    client_order_id: ''        // (must be combined with corresponding market_id) (optional)
    status: 'open',            // (optional) 'open', 'closed', 'canceled', 'rejected', 'processing', 'amending', 'cancelingall', 'canceling'
    market_id: 'BTC-USD',      // (optional)
    start_time: 1669629461258298  // (optional) epoch time in microseconds
    end_time: 1669629461258298    // (optional)
    p_limit: 100, // max rows returned, max 1000
    p_page: 0, // pagination page, index begins at 0
    p_order: "DESC" // default "DESC" for descending and "ASC" for ascending
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
            'client_order_id':''
            'status': 'open',
            'timestamp': 1669629461258298,
            'total_filled_size': '0',
            'time_in_force':'post_only'},
           {'id': 'BTC-USD@1777',
            'initial_size': '1',
            'market_id': 'BTC-USD',
            'order_type': 'market',
            'price': '21210',
            'profile_id': 4,
            'reason': '',
            'side': 'long',
            'size': '1',
            'client_order_id':''
            'status': 'open',
            'timestamp': 1669629461258298,
            'total_filled_size': '0',
            'time_in_force':'post_only'}
    ]
}
```

Tip: Orders are indexed by timestamp; if start\_time is not specified, the response will take longer as it will parse through your full order history. Queries with start\_time parameter could be up to 10x faster than queries without start\_time.

### Place orders

#### Limit and market orders

Submitted orders will immediately return a response saying that the order is in 'processing' status and will include an order ID. To verify the status of the order is 'confirmed', we recommend subscribing to the accounts websocket channel. Alternatively, check the order status by order ID.

```
POST /orders
```

```json
Parameters
{
    market_id: 'BTC-USD',
    price: 19800,
    side: 'long',        // 'long' or 'short'
    size: 0.45, 
    type: 'limit'        // 'market' or 'limit'
    client_order_id: ''  // (optional)
    time_in_force: 'post_only' // (optional) 'good_till_cancel' 'post_only' 'immediate_or_cancel' 'fill_or_kill'
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
        'client_order_id':''
        'type': 'limit',
        'time_in_force':'post_only'}
    ]
}
```

To keep an orderly market, RabbitX has a 1,000 open order limit per account.

#### Position stop loss and take profits

```json
Parameters
{
    market_id: 'BTC-USD',
    price: 19800,
    side: 'long',              // 'long' or 'short'
    size: 1.00,                // size is percentage of the position. 0.5 means 50% of the position. 1.0 means 100% of the position.
    type: 'stop_loss'          // 'stop_loss' or 'take_profit'
    type: 'limit'              // 'market' or 'limit'
    client_order_id: ''        // (optional)
    trigger_price: 20000       // required
    time_in_force: 'post_only' // (optional) 'good_till_cancel' 'post_only' 'immediate_or_cancel' 'fill_or_kill'
}
```

#### Stop limit and stop market

```json
Parameters
{
    market_id: 'BTC-USD',
    price: 19800,              // required for stop_limit order type
    side: 'long',              // 'long' or 'short'
    size: 0.45, 
    type: 'stop_limit'         // 'stop_limit' or 'stop_market'
    client_order_id: ''        // (optional)
    trigger_price: 20000       // required
    time_in_force: 'post_only' // (optional) 'good_till_cancel' 'post_only' 'immediate_or_cancel' 'fill_or_kill'
}
```

### Cancel orders

```
DELETE /orders
```

```json
Parameters
{
    order_id: 'BTC-USD@1859'
    market_id: 'BTC-USD'
    client_order_id: ''        // (optional)
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
Parameters
{
    order_id: 'BTC-USD@1872',
    market_id: 'BTC-USD'
    price: 19800,
    size: 0.45, (optional)
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
