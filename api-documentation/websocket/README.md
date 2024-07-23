# Websocket

### General Information

RabbitX uses a centrifuge scalable real-time websocket for publishing messages. We recommend using one of the client SDKs available on the official centrifuge [page](https://centrifugal.dev/docs/transports/client\_sdk).&#x20;

### List of centrifuge websocket client SDKs[​](https://centrifugal.dev/docs/transports/client\_sdk#list-of-client-sdks) <a href="#list-of-client-sdks" id="list-of-client-sdks"></a>

* [centrifuge-js](https://github.com/centrifugal/centrifuge-js) – for browser, NodeJS and React Native
* [centrifuge-python](https://github.com/centrifugal/centrifuge-python) – for Python
* [centrifuge-go](https://github.com/centrifugal/centrifuge-go) – for Go language
* [centrifuge-dart](https://github.com/centrifugal/centrifuge-dart) – for Dart and Flutter
* [centrifuge-swift](https://github.com/centrifugal/centrifuge-swift) – for native iOS development
* [centrifuge-java](https://github.com/centrifugal/centrifuge-java) – for native Android development and general Java

Testnet websocket endpoint: `wss://api.testnet.rabbitx.io/ws`

Mainnet websocket endpoint: `wss://api.prod.rabbitx.io/ws`

RabbitX offers a complete pub/sub API with table diffing over WebSocket. You may subscribe to real-time changes on any available channel. All channels require [authentication](./#authentication).

Websocket packets may contain multiple messages separated with `\n`. It is recommended to split the message string before parsing the json.

```
def on_message(self, ws: WebSocketApp, message: str):
        for line in message.split('\n'):
            try:
                data = json.loads(line)
            except Exception as e:
                print(u'\u001b[31m ~~~ EXCEPTION ~~~')
                print(e)
                print(message, u'u\u001b[0m')
                return
```

### Authentication

Before subscribing to channels, you must first authenticate using the JWT token received through onboarding. You only need to authenticate once at the beginning. To authenticate, send the following message:

```
data = {'connect': {'token':"<jwt token>", name='js'}, 'id'=1}
```

`jwt_token` can be retrieved by [onboarding](../private-endpoints/authentication.md).

Once onboarded, to subscribe to a channel, send

```
{"subscribe": {'channel':"<channel name>", 'name':"js"}, 'id': "<internal counter>"}
```

Note: Jwt tokens expire in 48hrs. If your JWT token is expired, you will need to update it. If your JWT token is expired, the connection will be disconnected and you will need to resubscribe with a new token.

### Initial snapshot

The initial snapshot will send ALL information about the account. Subsequent messages will only send account change updates.&#x20;

Initial messages will always be in the following format

```
{'id':<internal counter>, 'subscribe':{'data':<data>}}
```

### Updates

Subsequent messages will only send account updates.&#x20;

Update messages are in the following format

```
{'push':{'channel':<channel name>, 'pub':{'data':<data>}}}
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
"trade:<symbol>"
"orderbook:<symbol>"
"market:<symbol>"
"account@<profile_id>"  // contains account balances, fills, orders, transfers
```

`profile_id` is retrieved by [onboarding](../private-endpoints/authentication.md).

Websocket connections go through the following lifecycle:

* Establish a websocket connection with `wss://api.testnet.rabbitx.io/ws/`
* Authenticate with JWT token
* Subscribe to a channel with `{"subscribe": {'channel':"trade:BTC-USD", 'name':"js"}, 'id': "<counter increment>"}`
* Receive data from channels
* Handle pings at regular intervals: send an empty frame to the server`{}` when you get an empty message from the exchange.

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

