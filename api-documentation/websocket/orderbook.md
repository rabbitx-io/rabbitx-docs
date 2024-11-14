# Orderbook

Subscribe to the channel name `orderbook:<symbol>` to get real-time orderbook updates.

The initial snapshot will send all the open orders in the orderbook sorted by price on bids (lowest to highest) and on asks (lowest to highest). A non-decreasing `sequence` number is returned on each update.

Orderbook updates are keyed by **price level**. Orderbook data is returned as:

```json
{'market_id': 'BTC-USD', 'bids': [[price, size], ...], 'asks': [[price, size], ...], 'sequence': 9097270, 'timestamp': 1665996854}
```

If the bid size at the price level 19,800 changed to 10.2, the _bids_ field would be \[\[19800, 10.2]]. If there are no more bids at the price level 19,800, then the _bids_ filed would be \[\[19800, 0]].&#x20;

_Each orderbook update increments `sequence` number by +1. If you have skipped a sequence number, you must resubscribe to get the most accurate orderbook state._

#### Example data

```

{'asks': [['25.4631', '73.63'],
          ['25.6858', '530.33'],
          ['25.6959', '390.66'],
          ['25.6983', '58.39'],
          ['25.7', '52.69'],
          ['25.8114', '12.49'],
          ['25.8443', '120.46'],
          ['25.8549', '68.56'],
          ['25.8763', '3.76'],
          ['25.9', '10'],
          ['25.9052', '57.9']],
'bids':
          ['25.3353', '103.61'],
          ['25.3459', '1056.52'],
          ['25.3565', '18730.93'],
          ['25.3989', '459.26'],
          ['25.4095', '165.35'],
          ['25.4201', '725.64'],
          ['25.4307', '1273.91'],
          ['25.4413', '998.33'],
          ['25.452', '2640.82'],
          ['25.4626', '611.76']],
 'market_id': 'SOL-USD',
 'sequence': 9097270,
 'timestamp': 1677226216475971}
```
