# Websocket

### General Information

Websocket endpoint: "wss://api.testnet.rabbitx.io/ws"

Rabbit<mark style="color:red;">X</mark> offers a complete pub/sub API with table diffing over WebSocket. You may subscribe to real-time changes on any available channel. All channels require [authentication](./#authentication).

### Authentication

Before subscribing to channels, you must first authenticate using JWT token received through onboarding. You only need to authenticate once at the beginning. To authenticate, send the following message:

```
data = {'connect': {'token':"<jwt token>", name='js'}, 'id'=1}
```

`jwt_token` can be retrieved by [onboarding](../private-endpoints/authentication.md).

Once onboarded, to subscribe to a channel, send

```
{"subscribe": {'channel':"<channel name>", 'name':"js"}, 'id': "<counter increment>"}
```

#### Reference implementation for channel subscription

```python
def on_open(self, ws: WebSocketApp):
    # authenticate 
    data = dict(connect=dict(token=self.session._jwt, name='js'), id=1)
    ws.send(json.dumps(data)) 
    
    channels = [f'account@{self.session.profile_id}']

    for market_id in self.market_ids:
        channels.append(f'orderbook:{market_id}')
        channels.append(f'trade:{market_id}')
        channels.append(f'market:{market_id}')

    channels = list(set(channels))

    # subscribe to channels
    for idx, ch in enumerate(channels):
        data = dict(subscribe=dict(channel=ch, name='js'), id=idx + 1)
        self._id_to_channel[idx + 1] = ch
        ws.send(json.dumps(data)) 

```

### Channels

```
"trade:<market_id>"
"orderbook:<market_id>"
"market:<market_id>"
"account@<profile_id>"  // contains account balances, fills, orders, transfers
```

`profile_id` is retrieved by [onboarding](../private-endpoints/authentication.md).

Websocket connections go through the following lifecycle:

* Establish a websocket connection with **wss://api.testnet.rabbitx.io/ws/**
* Authenticate with jwt token
* Subscribe to a channel with {"subscribe": {'channel':"trade:BTC-USD", 'name':"js"}, 'id': "\<counter increment>"}
* Receive data from channels
* Handle pings at regular intervals: `{'op': 'ping'}`. You will see an `{'type': 'pong'}` response.

### Reference implementation

Python: [https://github.com/rabbitx-io/rabbitx-python-client](https://github.com/rabbitx-io/rabbitx-python-client)

Examples: [https://github.com/rabbitx-io/rabbitx-python-client/blob/main/examples/ws.py](https://github.com/rabbitx-io/rabbitx-python-client/blob/main/examples/ws.py)

#### Example script

```python
from websocket import WebSocketApp

from rabbitx import const
from rabbitx.client import Client, WSClient, WSClientCallback


class TestWebSocketCallback(WSClientCallback):

    def account_init(self, profile_id: int, data, ws: WebSocketApp):
        print('account_init', profile_id, data)

    def account_data(self, profile_id: int, data, ws: WebSocketApp):
        print('account_data', profile_id, data)

    def orderbook_init(self, market_id: str, data, ws: WebSocketApp):
        print('orderbook_init', market_id, data)

    def orderbook_data(self, market_id: str, data, ws: WebSocketApp):
        print('orderbook_data', market_id, data)

    def market_init(self, market_id: str, data, ws: WebSocketApp):
        print('market_init', market_id, data)

    def market_data(self, market_id: str, data, ws: WebSocketApp):
        print('market_data', market_id, data)

    def trade_init(self, market_id: str, data, ws: WebSocketApp):
        print('trade_init', market_id, data)

    def trade_data(self, market_id: str, data, ws: WebSocketApp):
        print('trade_data', market_id, data)


if __name__ == '__main__':
    private_key = '<YOUR PRIVATE KEY>'
    client = Client(api_url=const.DEV_URL, private_key=private_key)
    client.onboarding.onboarding()

    wsc = WSClient(const.WS_DEV_URL, client, TestWebSocketCallback(), ['BTC-USD', 'SOL-USD'])
    wsc.run()

```

#### Example responses

```json
# Example websocket response

market_init "BTC-USD"
{'id': 'BTC-USD', 'status': 'active', 'minInitialMargin': 0.05, 'maintenanceMargin': 0.03, 'liquidationMargin': 0.02, 'minTick': 1, 'minOrder': 0.0001, 'bestBid': 19000, 'bestAsk': 19950, 'marketPrice': 19475, 'indexPrice': 19056.525, 'lastTradePrice': 19000, 'fairPrice': 19345.718387096775, 'instantFundingRate': 0.012467630555878564, 'instantDailyVolume': 5085874.244599999, 'lastFundingRate': 0.0044839357004183445, 'marketPrice24hChangePremium': -719.5, 'marketPrice24hChangeBasis': -0.03562851271385773, 'marketPrice24hHigh': 19899, 'marketPrice24hLow': 17426, 'marketVolume24h': 1598212.544499999, 'marketVolume24hChangePremium': -1870449.155600001, 'marketVolume24hChangeBasis': -0.539242312257225}

market_update "BTC-USD"
{'id': 'BTC-USD', 'status': 'active', 'minInitialMargin': 0.05, 'maintenanceMargin': 0.03, 'liquidationMargin': 0.02, 'minTick': 1, 'minOrder': 0.0001, 'bestBid': 19000, 'bestAsk': 19950, 'marketPrice': 19475, 'indexPrice': 19056.525, 'lastTradePrice': 19000, 'fairPrice': 19345.718387096775, 'instantFundingRate': 0.012467630555878564, 'instantDailyVolume': 5085874.244599999, 'lastFundingRate': 0.0044839357004183445, 'marketPrice24hChangePremium': -719.5, 'marketPrice24hChangeBasis': -0.03562851271385773, 'marketPrice24hHigh': 19899, 'marketPrice24hLow': 17426, 'marketVolume24h': 1598212.544499999, 'marketVolume24hChangePremium': -1870449.155600001, 'marketVolume24hChangeBasis': -0.539242312257225}

trade_init "BTC-USD"
[
{'id': 937, 'marketID': 'BTC-USD', 'timestamp': 1663868945, 'price': 19000, 'size': 1, 'liquidation': False, 'takerSide': 'short'}, 
{'id': 934, 'marketID': 'BTC-USD', 'timestamp': 1663868869, 'price': 19000, 'size': 1, 'liquidation': False, 'takerSide': 'short'}, 
{'id': 931, 'marketID': 'BTC-USD', 'timestamp': 1663867991, 'price': 19000, 'size': 1, 'liquidation': False, 'takerSide': 'short'}
]

orderbook_init "BTC-USD"
{'marketID': 'BTC-USD', 'bids': [[20445, 19.1007], ...], 'asks': [[23453, 100], ...], 'checksum': 'not_implemented', 'timestamp': 1665996854}

orderbook_update "BTC-USD"
{'marketID': 'BTC-USD', 'bids': [[20445, 0]], 'checksum': 'not_implemented', 'timestamp': 1665996854}
```

#### Orderbook&#x20;

The initial snapshot will send all the open orders in the orderbook sorted by price on bids (highest to lowest) and on asks (lowest to highest).&#x20;

Orderbook updates are keyed by **price level**. Orderbook data is returned as:

```json
{'marketID': 'BTC-USD', 'bids': [[price, size], ...], 'asks': [[price, size], ...], 'checksum': 'not_implemented', 'timestamp': 1665996854}
```

If the bid size at the price level 19,800 changed to 10.2, the _bids_ field would be \[\[19800, 10.2]]. If there are no more bids at the price level 19,800, then the _bids_ filed would be \[\[19800, 0]].

#### Trades

Subscribe to real-time market trade updates.

```json
[{'id': 'ETH-USD-13230788',
  'liquidation': False,
  'market_id': 'ETH-USD',
  'price': '1751.5',
  'size': '0.061',
  'taker_side': 'short',
  'timestamp': 1677222281960306},
 {'id': 'ETH-USD-13230785',
  'liquidation': False,
  'market_id': 'ETH-USD',
  'price': '1751.5',
  'size': '1.066',
  'taker_side': 'short',
  'timestamp': 1677222213001608},
  ...]
```

#### Market info

Subscribe to real-time market information updates.

```
{'average_daily_volume': '2401820.374635',
 'average_daily_volume_change_basis': '0',
 'average_daily_volume_change_premium': '0',
 'average_daily_volume_q': '94024.7',
 'best_ask': '25.4949',
 'best_bid': '25.4944',
 'fair_price': '24.1895',
 'forced_margin': '0.03',
 'id': 'SOL-USD',
 'index_price': '23.95',
 'instant_daily_volume': '0',
 'instant_funding_rate': '0.00273966823038845141406334164590479235',
 'last_funding_rate_basis': '0.00275322341295428046383659139400384672',
 'last_funding_update_time': 1677223163016247,
 'last_trade_price': '25.4944',
 'last_trade_price_24h_change_basis': '-0.02196647101699466758737100548586335213',
 'last_trade_price_24h_change_premium': '-0.5726',
 'last_trade_price_24high': '27.9',
 'last_trade_price_24low': '19.3886',
 'last_update_sequence': 9093289,
 'last_update_time': 1677223553148672,
 'liquidation_margin': '0.02',
 'market_price': '25.49465',
 'min_initial_margin': '0.05',
 'min_order': '0.01',
 'min_tick': '0.0001',
 'status': 'active'}
```
