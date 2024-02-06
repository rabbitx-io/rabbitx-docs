# RabbitX Fusion AMM

<figure><img src=".gitbook/assets/image (32).png" alt="" width="563"><figcaption></figcaption></figure>

Providing liquidity is hard if you’re not a professional market maker. You need trading and technical expertise, hundreds of thousands dollars worth of infrastructure, and a team of traders monitoring 24/7.

Whereas Automated Market Maker (AMM) based perpetual DEXs often have limited markets available for trading. This constrains your execution quality and ability to trade new markets with speed and size.

### Introducing RabbitX Fusion Automated Market Maker Powered by Elixir

Introducing the RabbitX Fusion AMM, your ticket to LP’ing on the RabbitX orderbook.

In partnership with Elixir, RabbitX is excited to introduce the Fusion AMM (FAMM). With FAMM, you deposit your USDT collateral and Elixir’s sophisticated, automated strategies trade on RabbitX in a way that both provides liquidity and earns passive yield for you. The ‘passively active’ FAMM uses automated strategies so your capital is actively managed like a pro MM, while you passively stake and earn.

With FAMM, you don’t need to be a pro market maker to LP on the RabbitX orderbook. Just deposit into the FAMM, and enjoy those yields!

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

* Stake operation
  * input: how many USDT value you are willing to stake
  * Shares issued to you will be your USDT staking amount / price per share
  * price per share = TVL / total shares issued
* At staking, there will be some ETH charged including the gas fee to call function. With the current ethereum gas price in mainnet, a deposit/withdrawal would require a $10 ETH fee (around 0.0044 ETH) + gas tx cost
  * Please pay attention to the total charge before you confirm your transaction
  * gas fee: the gas paid to call stake function to send the money from your wallet to elixir smart contract
  * amount: the pre-charged gas by elixir to call following functions to deposit the money from vault to rabbitx smart contract
  * RabbitX doesn’t charge / keep any of the eth paid for any stake and unstake transaction
  * If the transaction failed due to elixir estimated pre-charge gas being insufficient: your stake amount won’t be taken from your wallet.
  * Please let us know if you ever encounter this issue - we will report to Elixir to improve their gas estimation
* You will receive notification once stake is completed.

**After successful staking:**

<figure><img src=".gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

* You will see your updated shares in this vault under Vault details page. Please note your TVL (Net Asset Value) might not be updated immediately due to some latency in update frequency. Your NAV will be updated as long later
* You will be able to find your stake history in recent activity. However, please note currently Elixir is still in beta version, you won’t be able to see your activity history if you clean the cache of your browser or switch to a different browser. All transaction history will also be trackable on-chain if you click the vault contract address on the vault details page

### Withdrawing Liquidity

* Unstake operation
  * You can choose percentage% of your shares to be redeemed, and your estimated withdrawal amount will be share price \* redeemed shares
  * similar as of unstake, you will be charged with some ETH \~$10 based on current eth price

<figure><img src=".gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

* Once unstake request is accepted, you will be able to track your pending unstake request status under recent activity. In addition, you will receive right-top corner notification of your unstake transaction queue position in the block.

<figure><img src=".gitbook/assets/image (37).png" alt="" width="329"><figcaption></figcaption></figure>

* Once your unstake request is confirmed in the block, you will receive a notification on top-right corner notifying you that unstake request is processed

<figure><img src=".gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

* After Unstake is processed succesfully, you will see success stats and now you can wait for the withdrawable to be claimable (which can vary from few minutes to 6 hours)
  * Please note you might lose your history if you switch your browser
* Between few minutes \~ max 6 hours after your unstake activity is processed, your withdrawal will be claimable
  * Please note your claimable withdrawal will NEVER disappear even you switch your browser / clean your cache
  * as long as you have some claimable withdrawal, you will be able to view and claim after you log in with your wallet
