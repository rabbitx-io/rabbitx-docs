# Deadman Switch

RabbitX offers “Deadman Switch” functionality to help prevent unexpected losses from network malfunctions. If you are putting up significant risk on RabbitX, it can be nerve-wracking to think of what might happen if you or your datacenter loses connectivity.

Deadman switch automatically cancels all your orders after a certain period of time (minimum 1 ms) if you get disconnected from your. The deadman switch feature is set up such that if the client does not send any instructions/actions for orders for N seconds then the exchange will automatically cancel all open orders by the client immediately.

Example: You want to activate the deadman switch to cancel all your orders if there is no activity for 6 seconds.

Step 1: Activate the the deadman switch after POST /cancel\_all\_after with period = 600

Step 2: Start sending any request from the list:

1. POST /orders
2. PUT /orders
3. DELETE /orders
4. DELETE /orders/cancel\_all
5. POST /cancel\_all\_after

Step 3: The system will check if, during a period of 600 milliseconds, not any of 1-5 requests received, it will cancel all orders on all markets

Step 4: To deactivate the deadman switch, send DELETE /cancel\_all\_after

{% hint style="info" %}
After activating the deadman switch, the exchange will cancel all orders for your account if it has yet to receive any **actions including new/cancel/amend order requests** for a period of time.
{% endhint %}

#### Activating Deadman Switch on a Market

```
POST /cancel_all_after
```

```go
Params:
{
    market_id: 'BTC-USD' // market id
    timeout: 600 // in milliseconds
}
```

```go
Example response

{
    "success": true,
    "error": "",
    "result":
            {
                market_id:'BTC-USD'
                profile_id:1
                timeout:600 // in milliseconds
                last_updated: 1701324346000000
                status: "active" // status could be 'active' or 'canceled'
            }
}
```

#### Getting Deadman Switch on a Market

```
GET /cancel_all_after
```

```go
Params:
{
    market_id: 'BTC-USD' // market id
}
```

```go
Example response

{
    "success": true,
    "error": "",
    "result":
            {
                profile_id:1
                timeout:600 // in milliseconds
                last_updated: 1701324346000000
                status: "active" // status could be 'active' or 'canceled'
            }
}
```

GET /cancel\_all\_after response: profile\_id timeout - in milliseconds last\_updated - time in milliseconds when we saw requests from you status - the current status: "active" means that the deadman switch is active for the market. If the deadman mode isn't active for a market, then the result will return empty.

#### Removing Deadman Switch on a Market

```
DELETE /cancel_all_after
```

```go
Params:
{
    market_id: 'BTC-USD' // market id
}
```

```go
Example response

{
    "success": true,
    "error": "",
    "result": None
}
```

