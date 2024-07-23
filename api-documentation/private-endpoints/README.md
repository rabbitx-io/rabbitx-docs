# Private Endpoints

### Security

For onboarding with private keys, we suggest using AWS KMS service or Secrets Manager.&#x20;

The Secrets Manager is a service that helps protect access to your applications, services, and IT resources. This protection does not require an upfront investment or on-going maintenance costs. Unlike AWS KMS, Secrets Manager is designed to protect text blobs.

To learn more about AWS KMS or Secrets Manager, refer to the official AWS documentation.

KMS [https://docs.aws.amazon.com/kms/latest/developerguide/getting-started.html](https://docs.aws.amazon.com/kms/latest/developerguide/getting-started.html)

Secrets Manager [https://docs.aws.amazon.com/secretsmanager/latest/userguide/create\_secret.html](https://docs.aws.amazon.com/secretsmanager/latest/userguide/create\_secret.html)

### Reference implementation

Python: [https://github.com/rabbitx-io/rabbitx-python-client](https://github.com/rabbitx-io/rabbitx-python-client)

Examples: [https://github.com/rabbitx-io/rabbitx-python-client/tree/main/examples](https://github.com/rabbitx-io/rabbitx-python-client/tree/main/examples)

#### Python Installation

```bash
git clone https://github.com/rabbitx-io/rabbitx-python-client.git
cd rabbitx-python-client
pip install .
```

#### Examples

```bash
cd examples
python rest.py
python ws.py
```

#### Example Scripts

```python
from rabbitx import const
from rabbitx.client import Client, CandlePeriod, OrderSide, OrderType

if __name__ == '__main__':
    private_key = '<YOUR PRIVATE KEY>'
    client = Client(api_url=const.DEV_URL, private_key=private_key)

    markets = client.markets.list()
    print('available markets:\n', markets)

    orderbook = client.orderbook.get('BTC-USD')
    print('orderbook for BTC-USD:\n', orderbook)

    client.onboarding.onboarding()

    order_1 = client.orders.create(
        'BTC-USD',
        19000,
        OrderSide.LONG,
        1,
        OrderType.LIMIT,
    )
    print('\n\n\norder creation:\n', order_1)

    order_2 = client.orders.create(
        'BTC-USD',
        19000,
        OrderSide.SHORT,
        1,
        OrderType.LIMIT,
    )

    client.orders.amend(order_1['id'], 19000, 2, OrderType.MARKET)
    client.orders.cancel(order_1['id'])

    orders = client.orders.list(client.current_timestamp - 10, client.current_timestamp + 10)
    print('\n\n\nget order list:\n', orders)

    account = client.account.get()
    print('\n\n\naccount:\n', orders)

    # check jwt is valid (for stage env)
    client.account.validate(client._jwt)

    new_leverage = client.account.set_leverage('BTC-USD', 10)
    print('\n\n\nnew leverage:\n', new_leverage)

    candles = client.candles.list(
        'BTC-USD',
        client.current_timestamp - 10,
        client.current_timestamp + 10,
        CandlePeriod.M1,
    )
    print('\n\n\ncandles:\n', candles)

    new_jwt = client.jwt.update()
    print('\n\n\nnew jwt:\n', candles)

    fills = client.fills.list(
        client.current_timestamp - 10,
        client.current_timestamp + 10,
        0,
        100,
        ['BTC-USD', 'SOL-USD'],
    )
    print('\n\n\nfills:\n', candles)

```
