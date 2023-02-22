# Authentication

### Reference implementation

[https://github.com/rabbitx-io/rabbitx-python-client/blob/main/rabbitx/client/endpoints/onboarding.py](https://github.com/rabbitx-io/rabbitx-python-client/blob/main/rabbitx/client/endpoints/onboarding.py)

#### Example: Onboarding

```python
from rabbitx import const
from rabbitx.client import Client, OrderSide, OrderType

private_key = '<YOUR PRIVATE KEY>'
client = Client(api_url=const.DEV_URL, private_key=private_key)
onboarding_resp = client.onboarding.onboarding()

order_resp = client.orders.create('BTC-USD', 19000, OrderSide.LONG, 1, OrderType.LIMIT)
```

#### Authentication Steps

note: expires must be greater than or equal to 600 secs.

```python
from eth_account.messages import encode_defunct
from hexbytes import HexBytes
from web3.auto import w3
from datetime import datetime
import requests

onboarding_message = 'Welcome to Rabbit DEX'
url = 'https://rbt-api-dev.strips.finance'
private_key = '<YOUR PRIVATE KEY>'
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

#### Example: Authenticating Private Endpoints

```python
PAYLOAD_KEY_METHOD = 'method'
PAYLOAD_KEY_PATH = 'path'

REQUIRED_KEYS = [PAYLOAD_KEY_METHOD, PAYLOAD_KEY_PATH]

onboarding_resp = onboard(private_key)
api_secret = onboarding_resp['result'][0]['apiSecret']['Secret']

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
        keys = list(self.data.keys())
        keys.sort()
        message = [f'{k}={str(self.data[k]).lower()}' if type(self.data[k]) == bool else f'{k}={self.data[k]}' for k in keys]
        message.append(str(self.timestamp))
        message = ''.join(message)

        h = hashlib.sha256()
        h.update(message.encode())

        return h.digest()

    def sign(self, secret: str) -> str:
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
    
onboarding_resp = onboard(private_key)
api_secret = onboarding_resp['result'][0]['apiSecret']['Secret']
api_key = onboarding_resp['result'][0]['apiSecret']['Key']

data = dict(marketID='BTC-USD',
           price=19300,
           side='LONG', 
           size=1, 
           type='LIMIT', 
           method='POST', 
           path='/orders')
           
payload = Payload(_expiration_timestamp(), data)
_signature = payload.sign(api_secret)
headers = _header(api_key, _signature)
resp = session.post(f'{url}/orders', json=data, headers=_header()).json()
```
