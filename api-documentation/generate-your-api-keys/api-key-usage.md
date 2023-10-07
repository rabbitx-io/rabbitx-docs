# API Key Usage

## Signing with API Key

Authentication is done by sending requests with the following HTTP headers.

#### HTTP Headers

> `RBT-SIGNATURE` : Signature of the request generated with your secret key. It is calculated as hex(HMAC\_SHA256(secret, payload)). Read how to generate signatures in the section below.
>
> `RBT-API-KEY` : Your API key.
>
> `RBT-TS` : A UNIX (in seconds) timestamp after which the request is no longer valid. This is to prevent replay attacks. Only accepts integers.
>
> _`Note: UNIX timestamps are in seconds. For example, 2018-02-08T04:30:37Z is 1518064237.`_

#### Generating Signatures

The signature generated is calculated as hex(HMAC\_SHA256(secret, payload\_hash)).

Steps to generate a valid signature:

1. Sort request data params by alphabetical order
2. Create a message string by appending data params keys in the format "key1=value1key2=value2key3=value3"
3. Append unix timestamp to the end of the message string. Example "key1=value1key2=value2key3=value31696692099"
4. Get the payload hash by taking the hash of message string using SHA256 encoding.
5. Signature is '0x'+HEX(HMAC\_SHA256(secret, payload\_hash))

{% hint style="info" %}
boolean values are expressed as lowercase "true" or "false".
{% endhint %}

**Example python code:**

```python
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
        provided by user secret. 
        '''
        secret_bytes = hex2bytes(secret)

        return '0x' + hmac.new(secret_bytes, self.hash, hashlib.sha256).hexdigest()

```
