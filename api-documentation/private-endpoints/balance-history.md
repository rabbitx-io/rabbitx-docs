# Balance History

### Get balance history

Gets the account balance changes history.

```
GET /balanceops
```

```json
Params:
{
    ops_type: 'deposit',       // (optional) 'deposit', 'withdraw', 'funding', 'pnl', 'fee'
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
            {'amount': '-0.0178801',
             'id': '421887c4-ddfb-447d-a0bb-6d8ec006f651',
             'ops_id2': '421887c4-ddfb-447d-a0bb-6d8ec006f651',
             'ops_type': 'fee',
             'profile_id': 7615,
             'reason': '',
             'status': 'success',
             'timestamp': 1676648452088704,
             'txhash': '',
             'wallet': ''},
            {'amount': '-0.0178801',
             'id': 'dff2013a-6dae-4375-9cf7-09e54a2a47f7',
             'ops_id2': 'dff2013a-6dae-4375-9cf7-09e54a2a47f7',
             'ops_type': 'fee',
             'profile_id': 7615,
             'reason': '',
             'status': 'success',
             'timestamp': 1676648322405711,
             'txhash': '',
             'wallet': ''}
    ]
}
```
