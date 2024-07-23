# Authentication

### Authenticating with API Key/Secret

#### HTTP Headers

The authentication of requests is done by sending the following HTTP headers:

`RBT-SIGNATURE`: Signature of the request generated with your secret key. It is calculated as hex(HMAC\_SHA256(secret, payload)). Example given below.

`RBT-API-KEY`: Your API key.

`RBT-TS`: A UNIX (in seconds) timestamp after which the request is no longer valid. This is to prevent replay attacks. Only accepts integers.

_`Note: UNIX timestamps are in seconds. For example, 2018-02-08T04:30:37Z is 1518064237.`_

#### Example: Generating RBT-SIGNATURE

[Click ](../generate-your-api-keys/api-key-usage.md)to read more about signing with API key and secrets. Github example [here](https://github.com/rabbitx-io/rabbitx-python-client/blob/main/rabbitx/payload.py).&#x20;

```python
PAYLOAD_KEY_METHOD = 'method'
PAYLOAD_KEY_PATH = 'path'

REQUIRED_KEYS = [PAYLOAD_KEY_METHOD, PAYLOAD_KEY_PATH]

api_key = '<YOUR API KEY>'
api_secret = '<YOUR API SECRET>'

def hex2bytes(value: str) -> bytes:
    if value.startswith('0x'):
        value = value[2:]

    return bytes.fromhex(value)

class Payload:

    timestamp: int
    data: dict[str, str]

    def __init__(self, timestamp: int, data: dict[str, str]):
        self.timestamp = timestamp
        self.data = data

        for k in REQUIRED_KEYS:
            if k in data:
                continue

            raise KeyError

    @property
    def hash(self) -> bytes:
        '''
        Returns the hash of the payload where the params are sorted in 
        alphabetical order.
        '''
        keys = list(self.data.keys())
        keys.sort()
        message = [f'{k}={str(self.data[k]).lower()}' if type(self.data[k]) == bool else f'{k}={self.data[k]}' for k in keys]
        message.append(str(self.timestamp))
        message = ''.join(message)

        h = hashlib.sha256()
        h.update(message.encode())

        return h.digest()

    def sign(self, secret: str) -> str:
        '''
        Returns HMAC-SHA256 signature after signing payload hash with
        user secret. 
        '''
        secret_bytes = hex2bytes(secret)

        return '0x' + hmac.new(secret_bytes, self.hash, hashlib.sha256).hexdigest()

    def verify(self, signature: str, secret: str) -> bool:
        expected_signature = self.sign(secret)

        if expected_signature != signature:
            return False

        current_timestamp = int(datetime.now().timestamp())

        if current_timestamp >= self.timestamp:
            return False

        return True
```

```python
def sign_request(data):
    expiration_timestamp = _expiration_timestamp()
    payload = Payload(expiration_timestamp, data)
    _signature = payload.sign(api_secret)
    
def headers(self) -> dict[str, str]:
    headers = {'RBT-TS': str(self.expiration_timestamp)}

    if self.api_key:
        headers['RBT-API-KEY'] = self.api_key

    if self._signature:
        headers['RBT-SIGNATURE'] = self._signature

    return headers
        
data = dict(marketID='BTC-USD',
           price=19300,
           side='LONG', 
           size=1, 
           type='LIMIT', 
           method='POST', 
           path='/orders')
           
payload = Payload(_expiration_timestamp(), data)
client._signature = payload.sign(api_secret)
resp = session.post(f'{url}/orders', json=data, headers=client.headers()).json()
```

### Wallet Private Key Onboarding (expert users)

If you would like to onboard with your wallet private key and generate a set of API key and secrets programmatically instead of from the frontend, you can retrieve your account API key and secret by calling the onboarding endpoint and signing a message with your wallet private key. However, note that this method is generally not recommended. Github example [here](https://github.com/rabbitx-io/rabbitx-python-client/blob/main/rabbitx/client/endpoints/onboarding.py).&#x20;

```python
from rabbitx import const
from rabbitx.client import Client, OrderSide, OrderType

private_key = '<YOUR WALLET PRIVATE KEY>'
client = Client(api_url=const.DEV_URL, private_key=private_key)
onboarding_resp = client.onboarding.onboarding()

order_resp = client.orders.create('BTC-USD', 19000, OrderSide.LONG, 1, OrderType.LIMIT)
```

#### Private Key Authentication Steps

Your wallet private key is used to onboard and retrieve a set of API key and secrets.&#x20;

First call the `/onboarding` endpoint such as in the example below. Save the response API key and secret to be used for signing private endpoint requests.

{% hint style="info" %}
expires must be less than or equal to 600 seconds.
{% endhint %}

```python
from eth_account.messages import encode_defunct
from hexbytes import HexBytes
from web3.auto import w3
from datetime import datetime
import requests

onboarding_message = 'Welcome to RabbitX!\n\nClick to sign in and on-board your wallet for trading perpetuals.\n\nThis request will not trigger a blockchain transaction or cost any gas fees. This signature only proves you are the true owner of this wallet.\n\nBy signing this message you agree to the terms and conditions of the exchange.'
url = 'https://rbt-api-dev.strips.finance'
private_key = '<YOUR WALLET PRIVATE KEY>'
wallet = '<YOUR WALLET ADDRESS>'
expires = 600

session = requests.Session()

def _expiration_timestamp():
    return int(datetime.now().timestamp() + expires)

def _header() -> dict:
    expiration_timestamp = _expiration_timestamp()
    return {'RBT-TS': str(expiration_timestamp)}
    
def hex2bytes(value: str) -> bytes:
    if value.startswith('0x'):
        value = value[2:]

    return bytes.fromhex(value)

def metamask_sign(message, timestamp: int, private_key: str):
    private_key = hex2bytes(private_key)
    metamask_message = f'{message}\n{timestamp}'
    message = encode_defunct(metamask_message.encode())
    signed_message = w3.eth.account.sign_message(message, private_key=private_key)

    return signed_message.signature.hex()

def _prepare_signature(private_key) -> str:
    expiration_timestamp = _expiration_timestamp()
    signature = metamask_sign(onboarding_message, expiration_timestamp, private_key)
    signature = bytearray(hex2bytes(signature))
    signature[-1] = signature[-1] % 27

    return '0x' + signature.hex()

def onboard(private_key: str) -> dict:
    signature = _prepare_signature(private_key)
    data = dict(wallet=wallet, signature=signature, isClient=False)
    resp = session.post(f'{url}/onboarding', json=data, headers=_header()).json()
    
    return resp
    
if __name__ == '__main__':
    onboarding_resp = onboard(private_key)
    api_secret = onboarding_resp['result'][0]['apiSecret']['Secret']
```

