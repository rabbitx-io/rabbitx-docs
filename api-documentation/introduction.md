# Introduction

By using any API provided by RabbitX, you agree to its Terms of Use and Privacy Policy. If you do not agree to the foregoing, then do not use any such API.

All documentation herein is provided ​“AS IS”. RabbitX makes no other warranties, express or implied, and hereby disclaims all implied warranties, including any warranty of merchantability and warranty of fitness for a particular purpose.

## General Info

#### Mainnet endpoints

```go
// REST
https://api.rabbitx.com

// Alternative REST
https://api.prod.rabbitx.io

// Websocket
wss://api.prod.rabbitx.io/ws
```

#### Testnet endpoints

```go
// REST
https://api.testnet.rabbitx.io
// Websocket
wss://api.testnet.rabbitx.io/ws
```

* All endpoints return either a JSON object or an array.
* All private endpoints require [authentication](private-endpoints/authentication.md).

### Reference implementation

Python: [https://github.com/rabbitx-io/rabbitx-python-client](https://github.com/rabbitx-io/rabbitx-python-client)

Examples: [https://github.com/rabbitx-io/rabbitx-python-client/tree/main/examples](https://github.com/rabbitx-io/rabbitx-python-client/tree/main/examples)

### Rate Limit

There is a rate limit of 20 orders/sec per account. Rate limits will return a 429 error code.
