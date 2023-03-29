# Data Structure

### Response structure

```go
type DataResponse[T any] struct {
	Res   T      `msgpack:"res" json:"res"`
	Error string `msgpack:"error" json:"error"`
}


type ProfileData struct {
	ProfileID           uint                        `msgpack:"id" json:"id"`
	ProfileType         *string                     `msgpack:"profile_type" json:"profile_type,omitempty"`
	Status              *string                     `msgpack:"status" json:"status,omitempty"`
	Wallet              *string                     `msgpack:"wallet" json:"wallet,omitempty"`
	LastUpdate          *int64                      `msgpack:"last_update" json:"last_update,omitempty"`
	Balance             *tdecimal.Decimal           `msgpack:"balance" json:"balance,omitempty"`
	AccountEquity       *tdecimal.Decimal           `msgpack:"account_equity" json:"account_equity,omitempty"`
	TotalPositionMargin *tdecimal.Decimal           `msgpack:"total_position_margin" json:"total_position_margin,omitempty"`
	TotalOrderMargin    *tdecimal.Decimal           `msgpack:"total_order_margin" json:"total_order_margin,omitempty"`
	TotalNotional       *tdecimal.Decimal           `msgpack:"total_notional" json:"total_notional,omitempty"`
	AccountMargin       *tdecimal.Decimal           `msgpack:"account_margin" json:"account_margin,omitempty"`
	WithdrawbleBalance  *tdecimal.Decimal           `msgpack:"withdrawable_balance" json:"withdrawable_balance,omitempty"`
	CumUnrealizedPnl    *tdecimal.Decimal           `msgpack:"cum_unrealized_pnl" json:"cum_unrealized_pnl,omitempty"`
	Health              *tdecimal.Decimal           `msgpack:"health" json:"health,omitempty"`
	AccountLeverage     *tdecimal.Decimal           `msgpack:"account_leverage" json:"account_leverage,omitempty"`
	CumTradingVolume    *tdecimal.Decimal           `msgpack:"cum_trading_volume" json:"cum_trading_volume,omitempty"`
	Leverage            map[string]tdecimal.Decimal `msgpack:"leverage" json:"leverage,omitempty"`
	LastLiqCheck        *int64                      `msgpack:"last_liq_check" json:"last_liq_check,omitempty"`
	Positions     []*PositionData        `msgpack:"positions" json:"positions,omitempty"`
	Orders        []*OrderData           `msgpack:"orders" json:"orders,omitempty"`
	Fills         []*FillData            `msgpack:"fills" json:"fills,omitempty"`
	Notifications []*ProfileNotification `msgpack:"notifications" json:"profile_notifications,omitempty"`
}


type OrderData struct {
	OrderId         string           `msgpack:"id" json:"id"`
	ProfileID       uint             `msgpack:"profile_id" json:"profile_id"`
	MarketID        string           `msgpack:"market_id" json:"market_id"`
	OrderType       string           `msgpack:"order_type" json:"order_type"`
	Status          string           `msgpack:"status" json:"status"`
	Price           tdecimal.Decimal `msgpack:"price" json:"price"`
	Size            tdecimal.Decimal `msgpack:"size" json:"size"`
	InitialSize     tdecimal.Decimal `msgpack:"initial_size" json:"initial_size"`
	TotalFilledSize tdecimal.Decimal `msgpack:"total_filled_size" json:"total_filled_size"`
	Side            string           `msgpack:"side" json:"side"`
	Timestamp       int64            `msgpack:"timestamp" json:"timestamp"`
	Reason          string           `msgpack:"reason" json:"reason"`
}


type PositionData struct {
	PositionID        string            `msgpack:"id" json:"id"`
	MarketID          string            `msgpack:"market_id" json:"market_id"`
	ProfileID         uint              `msgpack:"profile_id" json:"profile_id"`
	Size              tdecimal.Decimal  `msgpack:"size" json:"size"`
	Side              string            `msgpack:"side" json:"side"`
	EntryPrice        tdecimal.Decimal  `msgpack:"entry_price" json:"entry_price"`
	UnrealizedPnlFair *tdecimal.Decimal `msgpack:"unrealized_pnl" json:"unrealized_pnl,omitempty"`
	NotionalFair      *tdecimal.Decimal `msgpack:"notional" json:"notional,omitempty"`
	Margin            *tdecimal.Decimal `msgpack:"margin" json:"margin,omitempty"`
	LiquidationPrice  *tdecimal.Decimal `msgpack:"liquidation_price" json:"liquidation_price,omitempty"`
	FairPrice         *tdecimal.Decimal `msgpack:"fair_price" json:"fair_price,omitempty"`
}


type MarketData struct {
	MarketID          string            `msgpack:"id" json:"id"`
	Status            *string           `msgpack:"status" json:"status,omitempty"`
	MinInitialMargin  *tdecimal.Decimal `msgpack:"min_initial_margin" json:"min_initial_margin,omitempty"`
	ForcedMargin      *tdecimal.Decimal `msgpack:"forced_margin" json:"forced_margin,omitempty"`
	LiquidationMargin *tdecimal.Decimal `msgpack:"liquidation_margin" json:"liquidation_margin,omitempty"`
	MinTick           *tdecimal.Decimal `msgpack:"min_tick" json:"min_tick,omitempty"`
	MinOrder          *tdecimal.Decimal `msgpack:"min_order" json:"min_order,omitempty"`
	BestBid           *tdecimal.Decimal `msgpack:"best_bid" json:"best_bid,omitempty"`
	BestAsk           *tdecimal.Decimal `msgpack:"best_ask" json:"best_ask,omitempty"`
	MarketPrice       *tdecimal.Decimal `msgpack:"market_price" json:"market_price,omitempty"`
	IndexPrice        *tdecimal.Decimal `msgpack:"index_price" json:"index_price,omitempty"`
	LastTradePrice    *tdecimal.Decimal `msgpack:"last_trade_price" json:"last_trade_price,omitempty"`
	FairPrice         *tdecimal.Decimal `msgpack:"fair_price" json:"fair_price,omitempty"`

	LastTradePrice24High *tdecimal.Decimal `msgpack:"last_trade_price_24high" json:"last_trade_price_24high,omitempty"`
	LastTradePrice24Low  *tdecimal.Decimal `msgpack:"last_trade_price_24low" json:"last_trade_price_24low,omitempty"`

	AverageDailyVolume              *tdecimal.Decimal `msgpack:"average_daily_volume" json:"average_daily_volume,omitempty"`
	InstantFundingRate              *tdecimal.Decimal `msgpack:"instant_funding_rate" json:"instant_funding_rate,omitempty"`
	InstantDailyVolume              *tdecimal.Decimal `msgpack:"instant_daily_volume" json:"instant_daily_volume,omitempty"`
	LastFundingRate                 *tdecimal.Decimal `msgpack:"last_funding_rate_basis" json:"last_funding_rate_basis,omitempty"`
	LastTradePrice24ChangePremium   *tdecimal.Decimal `msgpack:"last_trade_price_24h_change_premium" json:"last_trade_price_24h_change_premium,omitempty"`
	LastTradePrice24ChangeBasis     *tdecimal.Decimal `msgpack:"last_trade_price_24h_change_basis" json:"last_trade_price_24h_change_basis,omitempty"`
	AverageDailyVolumeChangePremium *tdecimal.Decimal `msgpack:"average_daily_volume_change_premium" json:"average_daily_volume_change_premium,omitempty"`
	AverageDailyVolumeChangeBasis   *tdecimal.Decimal `msgpack:"average_daily_volume_change_basis" json:"average_daily_volume_change_basis,omitempty"`

	LastUpdateTime        int64             `msgpack:"last_update_time" json:"last_update_time,omitempty"`
	LastUpdateSequence    int64             `msgpack:"last_update_sequence" json:"last_update_sequence,omitempty"`
	AverageDailyVolumeQ   *tdecimal.Decimal `msgpack:"average_daily_volume_q" json:"average_daily_volume_q,omitempty"`
	LastFundingUpdateTime int64             `msgpack:"last_funding_update_time" json:"last_funding_update_time,omitempty"`
}


type TradeData struct {
	TradeId     string           `msgpack:"id" json:"id"`
	MarketId    string           `msgpack:"market_id" json:"market_id"`
	Timestamp   uint64           `msgpack:"timestamp" json:"timestamp"`
	Price       tdecimal.Decimal `msgpack:"price" json:"price"`
	Size        tdecimal.Decimal `msgpack:"size" json:"size"`
	Liquidation bool             `msgpack:"liquidation"  json:"liquidation"`
	TakerSide   string           `msgpack:"taker_side"  json:"taker_side"`
}


type FillData struct {
	Id          string           `msgpack:"id" json:"id"`
	ProfileId   uint             `msgpack:"profile_id" json:"profile_id"`
	MarketId    string           `msgpack:"market_id" json:"market_id"`
	OrderId     string           `msgpack:"order_id" json:"order_id"`
	Timestamp   int64            `msgpack:"timestamp" json:"timestamp"`
	TradeId     string           `msgpack:"trade_id" json:"trade_id"`
	Price       tdecimal.Decimal `msgpack:"price" json:"price"`
	Size        tdecimal.Decimal `msgpack:"size" json:"size"`
	Side        string           `msgpack:"side"  json:"side"`
	IsMaker     bool             `msgpack:"is_maker"  json:"is_maker"`
	Fee         tdecimal.Decimal `msgpack:"fee" json:"fee"`
	Liquidation bool             `msgpack:"liquidation"  json:"liquidation"`
	ShardId     string           `msgpack:"shard_id" json:"-"`
	ArchiveId   int              `msgpack:"archive_id" json:"-"`
}


type OrderbookData struct {
	MarketID  string               `msgpack:"market_id" json:"market_id"`
	Bids      [][]tdecimal.Decimal `msgpack:"bids" json:"bids,omitempty"`
	Asks      [][]tdecimal.Decimal `msgpack:"asks" json:"asks,omitempty"`
	Sequence  uint                 `msgpack:"sequence" json:"sequence"`
	Timestamp int64                `msgpack:"timestamp" json:"timestamp"`
}


type CandleData struct {
	Time   int64            `msgpack:"time" json:"time"`
	Low    tdecimal.Decimal `msgpack:"low" json:"low"`
	High   tdecimal.Decimal `msgpack:"high" json:"high"`
	Open   tdecimal.Decimal `msgpack:"open" json:"open"`
	Close  tdecimal.Decimal `msgpack:"close" json:"close"`
	Volume tdecimal.Decimal `msgpack:"volume" json:"volume"`
}


type Profile struct {
	ProfileId uint   `msgpack:"profile_id" json:"id"`
	Type      string `msgpack:"profile_type" json:"profile_type"`
	Status    string `msgpack:"status" json:"status"`
	Wallet    string `msgpack:"wallet" json:"wallet"`
}

type BalanceOps struct {
	OpsId     string           `msgpack:"id" json:"id"`
	Status    string           `msgpack:"status" json:"status"`
	Reason    string           `msgpack:"reason" json:"reason"`
	Txhash    string           `msgpack:"txhash" json:"txhash"`
	ProfileId uint             `msgpack:"profile_id" json:"profile_id"`
	Wallet    string           `msgpack:"wallet" json:"wallet"`
	Type      string           `msgpack:"ops_type" json:"ops_type"`
	Id2       string           `msgpack:"ops_id2" json:"ops_id2"`
	Amount    tdecimal.Decimal `msgpack:"amount" json:"amount"`
	Timestamp int64            `msgpack:"timestamp" json:"timestamp"`
	ShardId   string           `msgpack:"shard_id" json:"shard_id"`
}



```
