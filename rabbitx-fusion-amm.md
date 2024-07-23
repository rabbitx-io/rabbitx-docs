# RabbitX Fusion AMM

<figure><img src=".gitbook/assets/image (32).png" alt="" width="563"><figcaption></figcaption></figure>

Providing liquidity is hard if you’re not a professional market maker. You need trading and technical expertise, hundreds of thousands of dollars worth of infrastructure, and a team of traders monitoring 24/7.

Automated Market Maker (AMM)-based perpetual DEXs often have limited markets available for trading. This constrains your execution quality and ability to trade new markets with speed and size.

### Introducing RabbitX Fusion Automated Market Maker Powered by Elixir

Introducing the RabbitX Fusion AMM, your ticket to LP’ing on the RabbitX orderbook.

In partnership with Elixir, RabbitX is excited to introduce the Fusion AMM (FAMM). With FAMM, you deposit your USDT collateral and Elixir’s sophisticated, automated strategies trade on RabbitX in a way that both provides liquidity and earns passive yield for you. The ‘passively active’ FAMM uses automated strategies, so your capital is actively managed like a pro MM while you passively stake and earn.

With FAMM, you don’t need to be a pro market maker to LP on the RabbitX orderbook. Just deposit into the FAMM and enjoy those yields!

Not only can you make passive yield staking with FAMM, you can also earn RBX while doing so!

### Earn RBX Rewards

25,000,000 (2.5%) of RBX tokens will be allocated to Elixir vaults over 2 years. Token rewards are distributed on a weekly basis, equally weighted across all markets on RabbitX. Your RBX rewards are based on your amount and time staked.

```
Reward APY Calculation
Reward apy = 0.5 * 1/31 * rbx price * 25m / tvl
```

### Guide: How To Stake

Navigate to [https://app.rabbitx.io/vaults](https://app.rabbitx.io/vaults) and connect your wallet.

<figure><img src=".gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (34).png" alt="" width="375"><figcaption></figcaption></figure>

* Stake operation:
  * Input: how much USDT value you are willing to stake.
  * Shares issued to you will be your USDT staking amount / price per share.
  * Price per share = TVL / total shares issued.
* At staking, there will be some ETH charged, including the gas fee to call the function. With the current ethereum gas price on mainnet, a deposit/withdrawal would require a $10 ETH fee (around 0.0044 ETH) + gas tx cost
  * Please pay attention to the total charge before you confirm your transaction.
  * Gas fee: The gas paid to call the stake function to send the money from your wallet to Elixir's smart contract.
  * Amount: The pre-charged gas by Elixir to call the following functions to deposit the money from the vault into RabbitX's smart contract.
  * RabbitX doesn’t charge or keep any of the ETH paid for any stake or unstake transaction.
  * If the transaction fails due to Elixir's estimated pre-charge gas being insufficient, your stake amount won’t be taken from your wallet.
  * Please let us know if you ever encounter this issue - we will report it to Elixir to improve their gas estimation.
* You will receive a notification once the stake is completed.

**After successful staking:**

<figure><img src=".gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

* You will see your updated shares in this vault under the 'Vault' details page. Please note that your NAV (Net Asset Value) might not be updated immediately due to some latency in the update frequency. Your NAV will be updated later.
* You will be able to find your stake history in recent activity. However, please note that Elixir is still in beta, so you won’t be able to see your activity history if you clean the cache of your browser or switch to a different browser. All transaction history will also be trackable on-chain if you click the vault contract address on the 'Vault' details page.

### Withdrawing Liquidity

* Unstake operation
  * You can choose the percentage of your shares to be redeemed, and your estimated withdrawal amount will be the share price \* redeemed shares.
  * Similarly to unstaking, you will be charged some ETH (\~$10) based on the current ETH price.

<figure><img src=".gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

* Once the unstake request is accepted, you will be able to track your pending unstake request status under recent activity. In addition, you will get a notification at the top-right with your unstake transaction queue position in the block.

<figure><img src=".gitbook/assets/image (37).png" alt="" width="329"><figcaption></figcaption></figure>

* Once your unstake request is confirmed in the block, you will get a notification at the top-right corner notifying you that the unstake request is processed.

<figure><img src=".gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

* After the unstake is successfully processed, it will be marked as 'Success', and now you'll have to wait for the withdrawal to be claimable (the waiting time can vary from a few minutes to 6 hours).
  * Please note that you might lose your history if you switch your browser.
* Your withdrawal will be claimable after a waiting time that can go from a few minutes to a maximum 6 hours after your unstake activity is processed.
  * Please note that your claimable withdrawal will never disappear, even if you switch your browser or clean your cache.
  * As long as you have some claimable withdrawals, you will be able to view and claim them after you log in with your wallet.
