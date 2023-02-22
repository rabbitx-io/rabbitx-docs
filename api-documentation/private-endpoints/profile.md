# Profile

### Get profile

Get profile information.

```
GET /profile
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": 
            {'account_equity': '10100.5942298516373318',
             'account_leverage': '0.13022857567255437197804012528243472907',
             'account_margin': '7.6788062438338535850313140021256117976',
             'balance': '10037.1782298516373318',
             'cum_trading_volume': '1378.802',
             'cum_unrealized_pnl': '63.416000000000000000000000000000000088',
             'health': '1',
             'id': 7615,
             'last_liq_check': 0,
             'last_update': 1676649580751868,
             'leverage': {'BTC-USD': '20', 'ETH-USD': '1', 'SOL-USD': '1'},
             'profile_type': 'trader',
             'status': 'active',
             'total_notional': '1315.386',
             'total_order_margin': '0',
             'total_position_margin': '65.7693',
             'wallet': '0x22a06bcbe144414399117ae98be847bdc79f0dc3',
             'withdrawable_balance': '9971.4089298516373318'}
}
```
