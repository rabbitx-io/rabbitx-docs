# Rate Limits

RabbitX implements an **IP-based Token-Based Rate Limiting** mechanism to ensure fair use of the API and prevent abuse. This rate limiting applies to all REST API requests made to the platform.

### Rate Limiting Overview

* **Shared Token Bucket Capacity:** 1200 tokens per minute (1-minute sliding window).
* **Token Consumption:** Each request type consumes a predefined number of tokens from the shared bucket.
* **Replenishment:** Tokens reset every minute.

### Token Consumption by Endpoint

The following table outlines the token cost for each API endpoint:

| **Endpoint**                  | **Tokens Consumed** |
| ----------------------------- | ------------------: |
| `POST /onboarding`            |                 100 |
| `GET /account`                |                  20 |
| `PUT /account/leverage`       |                  20 |
| `POST /jwt`                   |                  20 |
| `POST /orders`                |                   1 |
| `PUT /orders`                 |                   1 |
| `DELETE /orders`              |                   1 |
| `GET /fills`                  |                  10 |
| `GET /positions`              |                  10 |
| `GET /profile`                |                  10 |
| **Unauthenticated Endpoints** |      10 per request |

**Default Behavior:** All unauthenticated endpoints consume **10 tokens** per request.

### Rate Limit Headers

RabbitX provides the following headers in API responses to help clients manage their rate limits effectively:

* **`X-RateLimit-Limit`**: The total number of tokens allowed in the current window (default: 1200 tokens).
* **`X-RateLimit-Remaining`**: The number of tokens remaining in the current window.
* **`X-RateLimit-Reset`**: The UTC timestamp when the token bucket will reset.
* **`X-RateLimit-Retry-After`**: The number of seconds clients should wait before retrying after hitting the rate limit.

### For Market Makers

Large market makers may request increased rate limits for high-volume trading. To request an increase, please open a support ticket through RabbitX's official Discord channel. Include your wallet address and specify your need for a rate limit increase.

[**RabbitX Discord Channel Link**](https://discord.com/invite/rabbitx)

### Best Practices

1. **Monitor Rate Limit Headers:** Use the returned headers to avoid exceeding the token limit.
2. **Optimize Requests:** Minimize unnecessary API calls and use WebSocket to obtain updates if that's supported.
3. **Exponential Backoff:** Implement a backoff strategy to avoid rate limit errors.

This rate-limiting policy ensures reliable service for all users while preventing abuse. If you require higher rate limits, please contact RabbitX support.

