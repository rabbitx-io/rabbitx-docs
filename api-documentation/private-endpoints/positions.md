# Positions

### Get positions

Get account open positions.&#x20;

```
GET /positions
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": [
            {'entry_price': '25532.188679245283018867924528301886794',
              'fair_price': '24351',
              'id': 'pos-BTC-USD-tr-7615',
              'liquidation_price': '26027.959333211210844477010441472797217',
              'margin': '64.53015',
              'market_id': 'BTC-USD',
              'notional': '1290.603',
              'profile_id': 7615,
              'side': 'short',
              'size': '0.053',
              'unrealized_pnl': '62.603000000000000000000000000000000082'}
    ]
}
```
