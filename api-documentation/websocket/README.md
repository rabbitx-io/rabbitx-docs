# Websocket

### General Information

Websocket endpoint: "<mark style="color:red;">wss://rbt-api-dev.strips.finance/ws</mark>"

Rabbit<mark style="color:red;">X</mark> offers a complete pub/sub API with table diffing over WebSocket. You may subscribe to real-time changes on any available channel. Private channels require authentication.

To subscribe to a channel, simply send

```
{"subscribe": "<channel name>"}
```

#### Public channels

```
"trade:<marketID>"
"orderbook:<marketID>"
"market:<marketID>"
```

#### Private channels

```
"account#<profileID>"
```

#### Authentication

To authenticate to a private websocket channel send the following message:

```
data = {'connect': {'token':jwt_token, name='js'}, 'id'=1}
```

jwt\_token can be retrieved by [onboarding](./#undefined).



Websocket connections go through the following lifecycle:

* Establish a websocket connection with **wss://rabbitx.io/ws/**
* (Optional) Authenticate with AUTH jwt (above)
* Send pings at regular intervals: `{'op': 'ping'}`. You will see an `{'type': 'pong'}` response.
* Subscribe to a channel with `{'op': 'subscribe', 'channel': ['trades', 'orderbook']}`
* Receive data `{'type': 'update', 'channel': 'trades', 'market': 'BTC-USD', 'data': {'id': 15884651, 'price': 5231.0, 'size': 0.07, 'side': 'sell', 'liquidation': false, 'time': '2021-08-12T03:03:31.656050+00:00'}}`
* Unsubscribe `{'op': 'unsubscribe', 'channel': 'trades', 'market': 'BTC-USD'}`
* Receive unsubsubscribe response `{'type': 'unsubscribed', 'channel': 'trades', 'market': 'BTC-USD'}`

### Reference implementation

Python: [https://github.com/rabbitx-io/rabbitx-python-client](https://github.com/rabbitx-io/rabbitx-python-client)

Examples: [https://github.com/rabbitx-io/rabbitx-python-client/blob/main/examples/ws.py](https://github.com/rabbitx-io/rabbitx-python-client/blob/main/examples/ws.py)

#### Example Script

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

#### Example Responses

```python
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

```python
{'marketID': 'BTC-USD', 'bids': [[price, size], ...], 'asks': [[price, size], ...], 'checksum': 'not_implemented', 'timestamp': 1665996854}
```

If the bid size at the price level 19,800 changed to 10.2, the _bids_ field would be \[\[19800, 10.2]]. If there are no more bids at the price level 19,800, then the _bids_ filed would be \[\[19800, 0]].
