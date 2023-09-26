# Authentication

### Reference implementation

[https://github.com/rabbitx-io/rabbitx-python-client/blob/main/rabbitx/client/endpoints/onboarding.py](https://github.com/rabbitx-io/rabbitx-python-client/blob/main/rabbitx/client/endpoints/onboarding.py)

### Onboarding with API Key/Secret

To create a API Key and API Secret, go to the app and click on the :gear: icon

![](<../../.gitbook/assets/image (20).png>)

You will then be prompted to sign a message "Welcome to Rabbit DEX" with your wallet to authenticate you. This message is safe to sign.&#x20;

![](<../../.gitbook/assets/image (23).png>)

You will then be prompted to create a new api key by specifying the length of expiration of the api key along with any ip restrictions that you would like to set.

![](<../../.gitbook/assets/image (24).png>)

Once your api key is created, you will be able to copy the API Key, Secret, Public and Private JWT tokens.&#x20;

* You will need the API Key, Secret to place orders and retrieve private data through REST
* Private JWT token for websocket private account data
* Refresh token is used to renew your keys

Note: you can renew your tokens by clicking the "Renew Now" button to renew it for 30 days.

#### Example: Authenticating Private Endpoints

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

### Private Key Onboarding (expert users)

If you would like to onboard with your wallet private key instead of generating an api key and secret, you can retrieve your account api key and secret by calling the onboarding endpoint and signing a message with your wallet private key. However, not that this method requires you to export your private key to safe location and is generally not recommended.

```python
from rabbitx import const
from rabbitx.client import Client, OrderSide, OrderType

private_key = '<YOUR WALLET PRIVATE KEY>'
client = Client(api_url=const.DEV_URL, private_key=private_key)
onboarding_resp = client.onboarding.onboarding()

order_resp = client.orders.create('BTC-USD', 19000, OrderSide.LONG, 1, OrderType.LIMIT)
```

#### Private Key Authentication Steps

note: expires must be greater than or equal to 600 secs.

```python
from eth_account.messages import encode_defunct
from hexbytes import HexBytes
from web3.auto import w3
from datetime import datetime
import requests

onboarding_message = 'Welcome to Rabbit DEX'
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

