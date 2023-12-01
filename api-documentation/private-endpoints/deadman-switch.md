# Deadman Switch

RabbitX offers “Deadman Switch” functionality to help prevent unexpected losses from network malfunctions. If you are putting up significant risk on RabbitX, it can be nerve-wracking to think of what might happen if you or your datacenter loses connectivity.

The exchange will cancel all orders on all markets for your account if it has yet to receive any new/cancel/amend order requests for a period of time.

#### Activating Deadman Switch&#x20;

```
GET /cancel_all_after
```

GET /cancel\_all\_after response: profile\_id timeout - in milliseconds last\_updated - time in milliseconds when we saw requests from you status - the current status: "active" - means that we see requests "canceled" - means that there were not requests during timeout and orders were canceled. Will be automatically reactivated once see any request.

```
POST /cancel_all_after
```

```go
Params:
{
    period: 600 // in milliseconds
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



Response: profile\_id timeout last\_updated status

```
DELETE /cancel_all_after
```

DELETE /cancel\_all\_after Response: (the deleted info) profile\_id timeout last\_updated status

Example: You want to activate deadman switch to cancel all your orders if there is no activity for 6 seconds.

Step 1: activate the deadman switch after POST /cancel\_all\_after with period = 600

Step 2: start sending any request from the list:

1. POST /orders
2. PUT /orders
3. DELETE /orders
4. DELETE /orders/cancel\_all
5. POST /cancel\_all\_after

Step 3: The system will check if during period of 600 milliseconds, not any of 1-5 requests received, it will cancel all orders on all markets

Step 4: To deactivate the deadman switch send DELETE /cancel\_all\_after
