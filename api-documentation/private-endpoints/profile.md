# Profile

### Get profile

Get profile tier information.

```
GET /profile
```

```json
Example response

{
    "success": true,
    "error": "",
    "result": 
            [
                {
                  "tier_status": {
                    "current": {
                      "tier": 2,
                      "title": "VIP 2 (Gold)",
                      "min_volume": "5000000"
                    },
                    "next": {
                      "tier": 3,
                      "title": "VIP 3 (Platinum)",
                      "min_volume": "10000000"
                    },
                    "needed_volume": "4630999.406908"
                  }
                }
            ]
}
```

