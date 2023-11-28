# Funding Rate

## Funding Rate

Get market funding rate history.

```
GET /markets/fundingrate
```

```json
Params
{
market_id: "BTC-USD"
p_limit: 100, // (optional) max 1000
start_time: 1697691500000000, // (optional) time in microseconds
end_time: 1697691600000000, // (optional) time in microseconds
p_page: 0, // (optional) pagination
p_order: "DESC" // (optional) default "DESC" for descending and "ASC" for ascending
}
```

```go
Response 
{
	market_id string               
	funding_rate string
	timestamp int64               
}
```
