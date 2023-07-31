# Market Info

## Market Info

Get basic market info and metadata.

```
GET /markets
```

<pre class="language-json"><code class="lang-json">Params
{
<strong>market_id: "BTC-USD"    // (optional) "BTC-USD", "ETH-USD", "SOL-USD"
</strong>}
</code></pre>

```go
Response
{
	market_id           string
	status              string
	min_initial_margin  string
	forced_margin       string
	liquidation_margin  string
	min_tick            string
	min_order           string
	best_bid            string
	best_ask            string
	market_price        string
	index_price         string
	last_trade_price    string
	fair_price          string

	last_trade_price_24high              string
	last_trade_price_24low               string
	average_daily_volume                 string
	instant_funding_rate                 string
	instant_daily_volume                 string
	last_funding_rate_basis              string
	market_price_24h_change_premium      string
	market_price_24h_change_basis        string
	average_daily_volume_change_premium  string
	average_daily_volume_change_basis    string
	average_daily_volume_q		     string

	last_update_time         int64 
	last_update_sequence     int64 
	last_funding_update_time int64
}
    
```
