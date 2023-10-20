# Responses Data Structure

### Responses data structure

All documentation herein is provided ​“AS IS”. RabbitX makes no other warranties, express or implied, and hereby disclaims all implied warranties, including any warranty of merchantability and warranty of fitness for a particular purpose.

The data structure model below is provided for golang.

<pre class="language-javascript"><code class="lang-javascript"><strong>REST response format:
</strong>{
result: &#x3C;result>,
err: &#x3C;error>
}

Trades data:
{
        "id": string,
        "market_id": string,
        "timestamp": uint,     // in microseconds
        "price": float,
        "size": float,     
        "liquidation": bool,
        "taker_side": string    // "long", "short"
 }


Orderbook data:
{
	'market_id': string, 
	'bids': [[float, float]],    // [[bid_price, bid_size], ...]
	'asks': [[float, float]],    // [[ask_price, ask_size], ...]
	'sequence': uint,
	'timestamp': uint
}


Candles data:
{
	'time': int64,
	'low': float,
	'high': float,
	'open': float,
	'close': float,
	'volume': float
}

Profile data:
{
    "id": uint,
    "profile_type": string,
    "status": string,
    "wallet": string,
    "last_update": uint,          // in microseconds
    "balance": float,
    "account_equity": float,
    "total_position_margin": float,
    "total_order_margin": float,
    "total_notional": float,
    "account_margin": float,
    "withdrawable_balance": float,
    "cum_unrealized_pnl": float,
    "health": float,
    "account_leverage": float,
    "cum_trading_volume": float,
    "leverage": {string:float},    // {"BTC-USD":20, "SOL-USD":20}
    "last_liq_check": int
}


Order data:
{
        "client_order_id": string,
        "created_at": uint,
        "id": string,
        "initial_size": float,
        "market_id": string,
        "order_type": string,             // "limit", "market", "stop_loss", "take_profit", "stop_limit", "stop_market"
        "price": float,
        "profile_id": uint,
        "reason": string,
        "side": string,                   // "long", "short"
        "size": float,
        "size_percent": float,            // only for position stoploss/take profit
        "status": string,
        "time_in_force": string,          // good_till_cancel, post_only, immediate_or_cancel, fill_or_kill
        "timestamp": uint,                // in microseconds
        "total_filled_size": float,
        "trigger_price": float,           // for stop limit, stop market, stop loss, take profit
        "updated_at": uint
}


Position data:
{
        "id": string,
        "market_id": string,
        "profile_id": uint,
        "size": float,
        "side": string,        // "long", "short"
        "entry_price": float,
        "unrealized_pnl": float,
        "notional": float,
        "margin": float,
        "liquidation_price": float,
        "fair_price": float,
        "stop_loss": float,
        "take_profit": float,
}


Market info:
{
    "id": string,
    "status": string,
    "min_initial_margin": float,
    "forced_margin": float,
    "liquidation_margin": float,
    "min_tick": float,
    "min_order": float,
    "best_bid": float,
    "best_ask": float,
    "market_price": float,
    "index_price": float,
    "last_trade_price": float,
    "fair_price": float,
    "instant_funding_rate": float,
    "last_funding_rate_basis": float,
    "last_update_time": uint,            // in microseconds
    "last_update_sequence": uint,
    "average_daily_volume_q": float,
    "last_funding_update_time": uint,    // in microseconds
    "icon_url": string,
    "market_title": string,
    "average_daily_volume": float,
    "last_trade_price_24high": float,
    "last_trade_price_24low": float,
    "last_trade_price_24h_change_premium": float,
    "last_trade_price_24h_change_basis": float,
    "average_daily_volume_change_premium": float,
    "average_daily_volume_change_basis": float
}


Account fills data:
{
        "id": string,
        "profile_id": uint,
        "market_id": string,
        "order_id": string,
        "timestamp": uint, // in microseconds
        "trade_id": string,
        "price": float,
        "size": float,
        "side": string,  // "long", "short"
        "is_maker": bool,
        "fee": float,
        "liquidation": bool
}


Balance Operations:
{
	"id": string,
	"status": string, 
	"reason": string,
	"txhash": string,
	"profile_id": uint, 
	"wallet": string,
	"ops_type": string,        // "deposit", "fee", "funding", "pnl", "withdrawal"
	"ops_id2": string, 
	"amount": float, 
	"timestamp": uint,        // in microseconds
	"due_block": uint,
	"shard_id": string,
}
</code></pre>

### Error Codes

```json
ERR_INTEGRITY_ERROR = 'INTEGRITY_ERROR'
ERR_ORDER_NOT_FOUND = 'ORDER_NOT_FOUND'
ERR_POSITION_NOT_FOUND = 'POSITION_NOT_FOUND'
ERR_ORDERBOOK_ENTRY_NOT_FOUND = 'ORDERBOOK_ENTRY_NOT_FOUND'
ERR_ORDER_LIMIT_REACHED = 'ORDER_LIMIT_REACHED'
ERR_ORDER_NOTIONAL_EXCEEDED = 'ORDER_NOTIONAL_EXCEEDED'
ERR_WRONG_ORDER_SIZE = 'WRONG_ORDER_SIZE'
ERR_WRONG_ORDER_SIDE = 'WRONG_ORDER_SIDE'
ERR_WRONG_ORDER_STATUS = 'WRONG_ORDER_STATUS'
ERR_WRONG_TIME_IN_FORCE = 'WRONG_TIME_IN_FORCE'
ERR_WRONG_ORDER_TYPE = 'WRONG_ORDER_TYPE'
ERR_ORDER_PRICE_OVERFLOW = 'ORDER_PRICE_OVERFLOW'
ERR_ORDER_IMMEDIATE_EXECUTION = 'ORDER_IMMEDIATE_EXECUTION'
ERR_CLIENT_ORDER_ID_DUPLICATE = 'CLIENT_ORDER_ID_DUPLICATE'
ERR_NO_CONDITION_MET = 'NO_CONDITION_MET'
ERR_NOT_YOUR_ORDER = 'NOT_YOUR_ORDER'
ERR_PROFILE_NOT_ACTIVE = 'PROFILE_NOT_ACTIVE'
ERR_MARKET_NOT_ACTIVE = 'MARKET_NOT_ACTIVE'
ERR_WRONG_MARKET_ID = 'WRONG_MARKET_ID'
ERR_CLIENT_ORDER_ID_TOO_LARGE = 'CLIENT_ORDER_ID_TOO_LARGE'
ERR_TIME_IN_FORCE_FOK_ERROR = 'TIME_IN_FORCE_FOK_ERROR'
ERR_TIME_IN_FORCE_IOC_ERROR = 'TIME_IN_FORCE_IOC_ERROR'
ERR_TIME_IN_FORCE_POSTONLY_ERROR = 'TIME_IN_FORCE_POSTONLY_ERROR'
ERR_NOTHING_TO_AMEND = 'NOTHING_TO_AMEND'
ERR_REVERT_INVALID_ROW = "INVALID_ROW"
ERR_REVERT_TAKER_AND_MAKER_SAME = "TAKER_AND_MAKER_SAME"
ERR_REVERT_NO_TAKER = "NO_TAKER"
ERR_REVERT_UNKNOWN_SIDE = "UNKNOWN_SIDE"
ERR_REVERT_NO_SUCH_MARKET = "NO_SUCH_MARKET"
ERR_REVERT_CANT_BIND = "CANT_BIND"
ERR_REVERT_ALREADY_EXIST = "ALREADY_EXIST"
ERR_REVERT_INVALID_HEADER = "INVALID_HEADER"
ERR_API_SECRET_UPDATE = "ERR_API_SECRET_UPDATE"
ERR_NO_SUCH_KEY = "NO_SUCH_KEY"
ERR_REFRESH_TOKEN_NOT_FOUND = "REFRESH_TOKEN_NOT_FOUND"
ERR_NO_API_KEY_FOR_REFRESH_TOKEN = "NO_API_KEY_FOR_REFRESH_TOKEN"
ERR_NOT_YOUR_REFRESH_TOKEN = "NOT_YOUR_REFRESH_TOKEN"
ERR_API_JWT_UPDATE_ERROR = "API_JWT_UPDATE_ERROR"
ERR_API_SECRET_UPDATE_ERROR = "API_SECRET_UPDATE_ERROR"
ERR_KEY_EXPIRED = "KEY_EXPIRED"
ERR_NOT_ALLOWED_FOR_IP = "NOT_ALLOWED_FOR_IP"
ERR_NOT_YOUR_KEY = "NOT_YOUR_KEY"
ERR_MAX_SECRETS_EXCEED = "MAX_SECRETS_EXCEED"
```
