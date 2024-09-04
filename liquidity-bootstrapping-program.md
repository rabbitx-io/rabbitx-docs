# Liquidity Bootstrapping Program

### Liquidity Incentive Program

To attract more liquidity to RabbitX, the Liquidity Incentive Program is a scheme that offers incentives to liquidity providers who provide deep, two-sided markets.

The RabbitX Liquidity Incentive Program has been carefully designed to maximise the liquidity of the exchange and reward liquidity providers that supply effective liquidity.

The incentive program will provide 7.5% of the initial token supply of RabbitX tokens (75,000,000 RBX) to be distributed to Liquidity Providers (LP) over two years based on metrics measuring the LP's spread, depth and uptime. The program is currently open; apply through the link below.

[Apply here](https://forms.gle/Ze127AbDjvqiBj4ZA)

RBX token on [Coingecko](https://www.coingecko.com/en/coins/rabbitx).

### Eligibility

LPs must have maker volumes greater than 0.5% of the total exchange maker volume and have a minimum of 90% uptime each month to be eligible to participate. LPs participating in the incentive program will not be eligible for any other rewards, including airdrops, trading rewards, etc. LPs accounts in the incentive program will not be counted towards referral rewards.

### Motivation

Liquidity on RabbitX is crucial for several reasons. Firstly, liquidity makes it easier for traders to execute trades quickly, efficiently, and at a fair price. This is because there is less slippage, which occurs when there is not enough liquidity in the market, causing orders to be filled at a different price than intended. In a highly liquid market, orders can be executed at or close to the current market price, which benefits traders by minimising costs and maximising profits.

Secondly, high levels of liquidity attract more traders to the exchange, which in turn attracts more liquidity and creates a virtuous cycle. This creates a network effect where traders are more likely to trade on a platform with high liquidity as it offers better trading opportunities and more choices in terms of trading pairs.

Finally, a highly liquid market promotes stability and security. In times of high volatility or market stress, liquidity helps to absorb sudden surges in demand or supply, preventing sharp price movements that could harm market stability. This, in turn, helps to build trust in the platform and increase confidence among traders.

### Goal

The program's goal is to incentivize market liquidity based on three metrics:

1. Two-way Bid/Ask spread
2. Two-way Bid/Ask size
3. Uptime

#### Fee Schedule

| Tier               | Maker Volume (monthly)         | Maker Fee | Taker Fee |
| ------------------ | ------------------------------ | --------- | --------- |
| Liquidity Provider | 0.5%+ of exchange maker volume | -0.015%   | 0.025%    |

#### Program Details

7.5% of the initial token supply of RabbitX (75,000,000 RBX) will be distributed to liquidity providers based on the $$Q_{FINAL}$$ measuring the liquidity provider's width, depth and uptime per monthly epoch.

$$
Q_{FINAL} = Q_{EPOCH}^{0.65}*MakerVolume^{0.35}*UptimeScore
$$

**Calculation methodology**

The following methodology calculates how much token reward each liquidity provider receives per monthly epoch. Liquidity providers earn token rewards proportionate to their relative share of $$Q_{FINAL}$$.

Orders below a certain minimum depth (MinDepth) per market are excluded, and orders over a certain maximum spread (mid-market spread) (MaxSpread) are also excluded. Snapshots are taken every minute using random sampling.

{% hint style="info" %}
_Note: starting 1 October 2023, Spread will be clamped to 0.005% or 0.00005._ \
_Spread = max(0.00005, Spread)_
{% endhint %}

Calculation steps:

1. Calculate  $$Q_{bid}=\frac{BidDepth_1}{(Spread_1)^{1.5}}+\frac{BidDepth_2}{(Spread_2)^{1.5}}+\frac{BidDepth_3}{(Spread_3)^{1.5}}...$$

for each order where BidDepth > MinDepth and with Spread < MaxSpread(Mid-Market)

For example, Assume a liquidity provider has multiple open bid orders (1 BTC at $29,995, 5 BTC at $29960, 10 BTC at $29,500) on the BTC-USD order book, and BTC is currently at $30,000 (based on mid price). Assume MinDepth is $5000, MaxSpread vs. mid-market is $60, or 20 Basis Points ($60/30000). A basis point is 0.01% = 0.0001.

The second order, 10 BTC at $29,500, is not qualified, as the order spread exceeds the max spread.

$$Q_{BID} = 1*29995/(5/30000)^{1.5} + 5*29960/(40/30000)^{1.5}$$

2. Calculate $$Q_{ask}=\frac{AskDepth_1}{(Spread_1)^{1.5}}+\frac{AskDepth_2}{(Spread_2)^{1.5}}+\frac{AskDepth_3}{(Spread_3)^{1.5}}...$$

for each order where AskDepth > MinDepth and with Spread < MaxSpread(Mid-Market)

3. Q\_BID and Q\_ASK are calculated every minute at random intervals.
4. Encourage 2-sided liquidity by taking the minimum of Q\_bid and Q\_ask (that means if the market maker only provides liquidity on one side, they will get 0 by missing the other side).

$$Q_{MIN}= min(Q_{BID},Q_{ASK})$$

5. _Q\_EPOCH_ is the sum of all Q\_MIN in a given epoch

$$Q_{EPOCH} = \sum^{}_{n}Q{MIN}_n$$

6. _Uptime\_EPOCH_ is the percentage of time in an epoch that a given market maker was live and quoting on both the bid and ask sides with order sizes greater than the stated order minimum and spreads smaller than the stated maximum spread.
7. Calculating uptime:

$$Uptime_{EPOCH}=\frac{\sum_{}^{}Count(Q_{MIN}>0)}{24*60*30}$$

$$UptimeScore=1/(1.1-Uptime_{EPOCH})$$

<figure><img src=".gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

9. Rewards and uptimes are calculated per market. Each market has a % allocation of total rewards per month.&#x20;
10. MakerVolume is the total volume that the liquidity provider traded from the maker side.
11. Q\_Final normalises Q\_epoch to account for uptime and also maker volume

$$Q_{FINAL} = Q_{EPOCH}^{0.65}*MakerVolume^{0.35}*UptimeScore$$

The rewards are then distributed based on the Q\_final score of each market

$$reward_{market}=\frac{Q_{FINAL}}{\sum{Q_{FINAL}}}$$

_If a new market is added during the month, the rewards for that market will be distributed pro-rata according to the time remaining in the month._

Parameters of the market maker's requirements may change each month based on market makers feedback on the current market conditions.



### FAQ

#### Who is eligible to participate?

Anyone who meets the minimum requirements is eligible to participate in this program. Drop us a message in Discord, or apply through the link at the top of this page.

#### **What are the maximum acceptable spreads per market?**

| Market                  | Max distance from market-mid |
| ----------------------- | ---------------------------- |
| BTC/USD                 | 20 bps                       |
| ETH/USD                 | 20 bps                       |
| Other perpetual markets | 50 bps                       |

#### **What is the minimum cumulative depth ($) per market?**

| Market                  | Min Depth |
| ----------------------- | --------- |
| BTC/USD                 | $50,000   |
| ETH/USD                 | $50,000   |
| Other perpetual markets | $25,000   |

#### What is the token reward allocation per market?

Rewards allocation per market may change given a 7-day notice. New coin listing rewards are pro-rated based on time.&#x20;

| Market          | Rewards Allocation | Min Spread Req |
| --------------- | ------------------ | -------------- |
| BTC-USD         | 7.50%              | 0.20%          |
| ETH-USD         | 7.50%              | 0.20%          |
| SOL-USD         | 7.50%              | 0.50%          |
| DOGE-USD        | 1.46%              | 0.50%          |
| BCH-USD         | 1.46%              | 0.50%          |
| XRP-USD         | 1.46%              | 0.50%          |
| MKR-USD         | 1.46%              | 0.50%          |
| AAVE-USD        | 1.46%              | 0.50%          |
| LINK-USD        | 1.46%              | 0.50%          |
| MATIC-USD       | 1.46%              | 0.50%          |
| LDO-USD         | 1.46%              | 0.50%          |
| SUI-USD         | 1.46%              | 0.50%          |
| PEPE1000-USD    | 1.46%              | 0.50%          |
| WLD-USD         | 1.46%              | 0.50%          |
| TON-USD         | 1.46%              | 0.50%          |
| STX-USD         | 1.46%              | 0.50%          |
| ARB-USD         | 1.46%              | 0.50%          |
| APT-USD         | 1.46%              | 0.50%          |
| INJ-USD         | 1.46%              | 0.50%          |
| BNB-USD         | 1.46%              | 0.50%          |
| RNDR-USD        | 1.46%              | 0.50%          |
| TRB-USD         | 1.46%              | 0.50%          |
| STG-USD         | 1.46%              | 0.50%          |
| RLB-USD         | 1.46%              | 0.50%          |
| ORDI-USD        | 1.46%              | 0.50%          |
| SATS1000000-USD | 1.46%              | 0.50%          |
| TIA-USD         | 1.46%              | 0.50%          |
| BLUR-USD        | 1.46%              | 0.50%          |
| JTO-USD         | 1.46%              | 0.50%          |
| MEME-USD        | 1.46%              | 0.50%          |
| SEI-USD         | 1.46%              | 0.50%          |
| YES-USD         | 1.46%              | 0.50%          |
| WIF-USD         | 1.46%              | 0.50%          |
| STRK-USD        | 1.46%              | 0.50%          |
| SHIB1000-USD    | 1.46%              | 0.50%          |
| BOME-USD        | 1.46%              | 0.50%          |
| SLERF-USD       | 1.46%              | 0.50%          |
| W-USD           | 1.46%              | 0.50%          |
| ENA-USD         | 1.46%              | 0.50%          |
| PAC-USD         | 1.46%              | 0.50%          |
| MAGA-USD        | 1.46%              | 0.50%          |
| TRUMP-USD       | 1.46%              | 0.50%          |
| MOG-USD         | 1.46%              | 0.50%          |
| NOT-USD         | 1.46%              | 0.50%          |
| MOTHER-USD      | 1.46%              | 0.50%          |
| BONK-USD        | 1.46%              | 0.50%          |
| TAIKO-USD       | 1.46%              | 0.50%          |
| FLOKI-USD       | 1.46%              | 0.50%          |
| BLAST-USD       | 1.46%              | 0.50%          |
| AVAX-USD        | 1.46%              | 0.50%          |
| PENDLE-USD      | 1.46%              | 0.50%          |
| JUP-USD         | 1.46%              | 0.50%          |
| FTM-USD         | 1.46%              | 0.50%          |
| SUN-USD         | 1.46%              | 0.50%          |
| POPCAT-USD      | 1.46%              | 0.50%          |
| DOGS-USD        | 1.46%              | 0.50%          |

#### What is the minimum uptime requirement?

To remain in the program, it is required to have at least 90% uptime.

#### When will token rewards be distributed?

The token rewards earned during each epoch will be subject to a vesting period of 3 months, meaning that they will become available gradually over time. The initial distribution of rewards will occur 30 days after the end of each epoch.

#### Rewards Emission

A total of 7.5% of the token supply will be distributed to liquidity providers. 0.18% of token supply will be allocated to early liquidity providers during March and April for supporting our initial launch. Monthly rewards will increase to 4,411,765 RBX tokens for the first 15 months and slowly decrease over time. Emission schedules may change with a 30-day notice. Any changes in the schedule will be communicated well in advance.

<figure><img src=".gitbook/assets/image (2) (3) (1).png" alt=""><figcaption></figcaption></figure>

![Liquidity Incentive Rewards Emission Schedule](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d576031f-8cd6-45c9-8510-518f394780d6/Untitled.png)

| Month    | RBX rewards per month | Cumulative rewards | % supply |
| -------- | --------------------- | ------------------ | -------- |
| Mar 2023 | 800,000               | 800,000            | 0.08%    |
| Apr 2023 | 1,000,000             | 1,800,000          | 0.18%    |
| May 2023 | 2,137,254             | 3,937,254          | 0.39%    |
| Jun 2023 | 3,274,508             | 7,211,762          | 0.72%    |
| Jul 2023 | 4,411,765             | 11,623,527         | 1.16%    |
| Aug 2023 | 4,411,765             | 16,035,291         | 1.60%    |
| Sep 2023 | 4,411,765             | 20,447,056         | 2.04%    |
| Oct 2023 | 4,411,765             | 24,858,821         | 2.49%    |
| Nov 2023 | 4,411,765             | 29,270,586         | 2.93%    |
| Dec 2023 | 4,411,765             | 33,682,350         | 3.37%    |
| Jan 2024 | 4,411,765             | 38,094,115         | 3.81%    |
| Feb 2024 | 4,411,765             | 42,505,880         | 4.25%    |
| Mar 2024 | 4,411,765             | 46,917,644         | 4.69%    |
| Apr 2024 | 4,411,765             | 51,329,409         | 5.13%    |
| May 2024 | 4,411,765             | 55,741,174         | 5.57%    |
| Jun 2024 | 3,952,454             | 59,693,627         | 5.97%    |
| Jul 2024 | 3,493,143             | 63,186,770         | 6.32%    |
| Aug 2024 | 3,033,832             | 66,220,602         | 6.62%    |
| Sep 2024 | 2,574,521             | 68,795,122         | 6.88%    |
| Oct 2024 | 2,115,209             | 70,910,332         | 7.09%    |
| Nov 2024 | 1,655,898             | 72,566,230         | 7.26%    |
| Dec 2024 | 1,196,587             | 73,762,817         | 7.38%    |
| Jan 2025 | 737,276               | 74,500,094         | 7.45%    |
| Feb 2025 | 499,906               | 75,000,000         | 7.50%    |
