# Account Operations

Available account operations:

1. Get account information
2. Set leverage
3. Update JWT token

### Get account information

Get your account information

```
GET /account
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": [
    {
    'account_equity': '10000000',
    'account_leverage': '1',
    'account_margin': '1',
    'balance': '10000000',
    'cum_trading_volume': '0',
    'cum_unrealized_pnl': '0',
    'health': '1',
    'id': 13,
    'last_liq_check': 0,
    'last_update': 1670396580648597,
    'leverage': {'BTC-USD': '20', 'ETH-USD': '1', 'SOL-USD': '1'},
    'profile_type': 'trader',
    'status': 'active',
    'total_notional': '0',
    'total_order_margin': '0',
    'total_position_margin': '0',
    'wallet': '0x8481cb01Ec35d43C116C3c272Fb026e6dD465e08',
    'withdrawable_balance': '10000000'}
    ]
}
```

### Update leverage

Update the leverage per market

```
PUT /account/leverage
```

```json
Params
{
market_id: 'BTC-USD',        // (required)
leverage: 20,               // (required) integer from 1 to 20
}
```

{% code overflow="wrap" %}
```json
Example response

{
    "success": true,
    "error": "",
    "result": [
    {
        'account_equity': '10000000',
        'account_leverage': '1',
        'account_margin': '1',
        'balance': '10000000',
        'cum_trading_volume': '0',
        'cum_unrealized_pnl': '0',
        'health': '1',
        'id': 13,
        'last_liq_check': 0,
        'last_update': 1670396631838889,
        'leverage': {'BTC-USD': '20', 'ETH-USD': '1', 'SOL-USD': '1'},
        'profile_type': 'trader',
        'status': 'active',
        'total_notional': '0',
        'total_order_margin': '0',
        'total_position_margin': '0',
        'wallet': '0x8481cb01Ec35d43C116C3c272Fb026e6dD465e08',
        'withdrawable_balance': '10000000'
     }
 ]
}
```
{% endcode %}

### Update JWT token

Update your JWT token (if expired).

```
POST /jwt
```

```
Params
{
is_client: true,        // (required)
refresh_token: "<insert jwt token here>" // (required)
}
```

```
Example response

{
    "success": true,
    "error": "",
    "result": ["<jwt token>"]
}
```
