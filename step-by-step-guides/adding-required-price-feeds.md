# Adding required Price Feeds

## Price Feed Store (PFS)

The Price Feed Store is a chain-specific registry that lists which tokens and price feeds can be used within Gearbox on that chain.&#x20;

{% hint style="warning" %}
For a token to be used as collateral, it must first be added to the Price Feed Store, along with a list of available price feeds.
{% endhint %}

Only the **Instance Owner**—a chain-specific multisig—can add or update entries in the Price Feed Store. This role acts as a neutral technical gatekeeper, ensuring safe and verified configurations while staying out of risk or business decisions.

{% hint style="success" %}
The Instance Owner multisig is open to participation from active curators and chain contributors, making the process transparent and inclusive without compromising protocol safety.
{% endhint %}

## How to work with PFS?

Interface for accessing each chain's PFS is located at [https://permissionless.gearbox.foundation/instances](https://permissionless.gearbox.foundation/instances/1).

**Demo of PFS setup workflow:**

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F9n0QLqkiJru3BYkpyr8F%2Fuploads%2F6cnMp2oRapw5fEHWZQag%2Fpfs%20setup.mp4?alt=media&token=a75497fb-8505-49aa-8198-69a8cc258b41" %}

## What price feed sources are already integrated? _(Click on feed to see details)_

<table><thead><tr><th>Price source</th><th width="159.078125">Feed type</th><th>Supported collaterals &#x26; features</th></tr></thead><tbody><tr><td><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds#external-feeds"><em><strong>Chainlink, Redstone push, EO</strong></em><br>AggregatorV3Interface - compatible external price providers</a></td><td>External</td><td>Blue-chip tokens</td></tr><tr><td><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds#erc4626-exchange-rate"><em><strong>ERC4626 exchange rate</strong></em></a></td><td>ERC4626</td><td>Most of the yield-bearing vaults</td></tr><tr><td><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds#pyth"><em><strong>Pyth</strong></em></a></td><td>Pyth</td><td>Blue chip &#x26; emerging tokens</td></tr><tr><td><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds#redstone-pull"><em><strong>Redstone pull</strong></em></a></td><td>Redstone</td><td>Deployed on any EVM on day 0</td></tr><tr><td><em><strong>Upper bound</strong></em></td><td>Bounded</td><td><ul><li>Bound borrowed tokens to protect borrowers from liquidations</li><li>Bound collateral tokens to protect LPs from price manipulation</li></ul></td></tr><tr><td><em><strong>Multiply 2 feeds price</strong></em></td><td>Composite</td><td>Optimal way to price correlated token pairs</td></tr><tr><td><em><strong>Constant price</strong></em></td><td>Constant</td><td><ul><li>Hardcode pegged assets</li><li>Apply premium or discount combining with composite feed</li></ul></td></tr><tr><td><em><strong>Curve LP</strong></em> </td><td>Curve_crypto<br>Curve_stable</td><td>Collateralize Curve LP tokens</td></tr><tr><td><em><strong>Token price from Curve Pool</strong></em></td><td>Curve TWAP</td><td>Collateralize experimental tokens</td></tr><tr><td><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds#pendle-pt"><em><strong>Pendle PT</strong></em></a></td><td>Pendle PT TWAP</td><td>Get TWAP market price of PTs</td></tr><tr><td><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds#kodiak-island"><em><strong>Kodiak Island</strong></em></a></td><td>Kodiak_island</td><td>Get island share price</td></tr></tbody></table>

## Setup details

<details>

<summary>Pyth</summary>

**Click New Feed and select Pyth type**

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

_**Pyth dashboard with feeds info:**_ [_**https://insights.pyth.network/price-feeds**_](https://insights.pyth.network/price-feeds)

* Name:&#x20;
  * Specify token Symbol and Price methodology
  * Examples:
    * Name: RLP (Redemption rate)\
      Feed: [https://insights.pyth.network/price-feeds/Crypto.RLP%2FUSD.RR](https://insights.pyth.network/price-feeds/Crypto.RLP%2FUSD.RR)
    * Name: RLP (Market)\
      Feed: [https://insights.pyth.network/price-feeds/Crypto.RLP%2FUSD](https://insights.pyth.network/price-feeds/Crypto.RLP%2FUSD)
* Token:
  * Token address\
    Needed for Gearbox contracts to understand what pull feed needs to be updated
* descriptionTicker
  * The same as name\
    This parameter is to be removed later
*   priceFeedId

    <figure><img src="../.gitbook/assets/Screenshot 2025-08-04 at 13.46.43.png" alt=""><figcaption></figcaption></figure>
* Pyth
  * Address of Pyth singleton contract on the target chain\
    see here: [https://docs.pyth.network/price-feeds/contract-addresses/evm](https://docs.pyth.network/price-feeds/contract-addresses/evm)
* maxConfToPriceRatio (takes value in bps: 300 = 3%)
  * Except for the current price, Pyth returns confidence interval
  * If the width of confidence interval in % is larger than this parameter, feed ourput is considered invalid causing tx revert
    * Example (consider maxConfToPriceRatio = 3%)
      * Valid price:
        * Price: 3000
        * Confidence interval: 15
        * confToPriceRatio = 15/3000 = 0.5%
      * Invalid price:
        * Price: 3000
        * Confidence interval: 120
        * confToPriceRatio = 120/3000 = 4%
* Staleness Period
  * Gearbox contracts track the timestamp of last Feed's update\
    If the update happened more than Staleness Period seconds ago, feed value should be updated or the contracts will revert
  * Recommended value for Pull feeds: 240s = 4min

</details>

<details>

<summary>External feeds</summary>

**Click New Feed and select External type**

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

_**Dashboards of external providers:**_

* _Redstone:_ [_**https://app.redstone.finance/app/feeds/**_](https://app.redstone.finance/app/feeds/)
* _Chainlink:_ [_**https://docs.chain.link/data-feeds/price-feeds/addresses?page=1\&testnetPage=1**_](https://docs.chain.link/data-feeds/price-feeds/addresses?page=1\&testnetPage=1)
* _EO:_ [_**https://docs.eo.app/docs/eprice/feeds-addresses/price-feed-addresses**_](https://docs.eo.app/docs/eprice/feeds-addresses/price-feed-addresses)
* _Some_ _protocols may provide custom feeds compatible with AggregatorV3Interface_
  * [_Resolv_](https://docs.resolv.xyz/litepaper/for-developers/smart-contracts/price-oracles)
  * [_Midas_](https://docs.midas.app/defi-integration/price-oracle)&#x20;

### _Config parameters:_

* Name:&#x20;
  * Specify token Symbol and Provider name
  * Examples:
    * USDC (Chainlink)
    * hemiBTC (EO)
    * ETH (Redstone Push)
    * mTBILL (Midas NAV)
* priceFeedAddress
  * Address of deployed feed

- Staleness Period (in seconds)
  * Gearbox contracts track the timestamp of last Feed's update\
    If the update happened more than Staleness Period seconds ago contracts will revert\
    \
    &#xNAN;_**Motivation**: If the feed with heartbeat of 24 hours wasn't updated in the last 30 hours, smth bad happened with the oracle providers and protocol operations are blocked waiting for Curator to interfere_
  * Recommended value:
    * Heartbeat + 15 minutes for slower chains (Ethereum)
      * 87 300s = 24h + 15min
    * Heartbeat + 2 minutes for faster chains
      * 86 520s = 24h + 2min

</details>

<details>

<summary>ERC4626 exchange rate</summary>

_This contract fetches mint/redeem rate from specified erc4626 vault and multiplies it by the underlying feed output to return the vault shares' USD price._

**Click New Feed and select ERC4626 type**

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

### _Config parameters:_

* Name:&#x20;
  * Specify token Symbol and underlying feed price Provider name
  * Example:
    * Name: sDAI (Chainlink)\
      Will mean that this feed takes ERC4626 sDAI/DAI exchange rate directly from sDAI contract + DAI/USD price from Chainlink
* Vault:
  * Address of ERC4626 vault to fetch mint/redeem rate from.
* underlyingPriceFeed:
  * Select existing price feed
  * Example:
    * If the specified vault it sUSDe, then underlying price feed should return USDe/USD price.

{% hint style="info" %}
To understand what asset's feed should be passed as underlying, go to the ERC4626 vault contract and call its _**asset()**_ method — you will get the address of the token which is vault's underlying.
{% endhint %}

</details>

<details>

<summary>Redstone pull</summary>

**Click New Feed and select Redstone type**

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### _Config parameters:_

* Name:&#x20;
  *   Specify token Symbol and Price methodology

      Examples:

      * Name: ezETH (Market)\
        Feed: [https://app.redstone.finance/app/token/ezETH/](https://app.redstone.finance/app/token/ezETH/)
      * Name: ezETH (Fundamental)\
        Feed: [https://app.redstone.finance/app/token/ezETH\_FUNDAMENTAL/](https://app.redstone.finance/app/token/ezETH_FUNDAMENTAL/)

- Token:
  * Token address\
    Needed for Gearbox contracts to understand what pull feed needs to be updated
- descriptionTicker
  * The same as name\
    This parameter is to be removed later
- dataServiceId
  * Most likely should be kept untouched\
    Internal variable for non-standard sources of redstone data
- dataFeedId
  *   The same as Symbol in Redstone UI

      <figure><img src="../.gitbook/assets/Screenshot 2025-08-05 at 13.16.04.png" alt=""><figcaption></figcaption></figure>

* signersThreshold
  * Minimum amount of signatures from Redstone nodes to have for the feed's result to be deemed valid.
  * Redstone currently have maximum of 5 nodes.
  * The safest option is to set this value to 5 (this was historically used in Gearbox), but sometimes couple of Redstone nodes may stop working for a short periods of time.
* Signer 1/2/3/4/5
  * Most likely should be kept untouched\
    Redstone have fixed list of signers' addresses that rarely (if ever) changes

</details>

<details>

<summary>Kodiak island</summary>

**Click New Feed and select Kodiak\_island type**

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### _Config parameters:_

* Name:&#x20;
  * Specify token Symbol and sources of Underlying Prices\
    Example:
    * Name: iBERA-iBGT (Pyth; Redstone push)
      * [Island](https://app.kodiak.finance/#/liquidity/pools/0x24afceb372b755f4953e738d6b38e9e4646d9f57?farm=0x199f156bba61496401dc2a009b5f69eb9a7e6f21\&chain=berachain_mainnet)
      * Feed0: [Pyth iBERA](https://insights.pyth.network/price-feeds/Crypto.IBERA%2FUSD)
      * Feed1: [Redstone push iBGT](https://app.redstone.finance/app/feeds/berachain/ibgt/)

- kodiakIsland:
  * Island Address
- PriceFeed0
  * Select the feed from already added to price token with 0'th index in terms of USD
- PriceFeed1
  * Select the feed from already added to price token with 1'st index in terms of USD
- descriptionTicker
  * The same as name\
    This parameter is to be removed later

</details>

<details>

<summary>Pendle PT</summary>

**Click New Feed and select Pendle PT TWAP type**

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

### _Config parameters:_

* Name:&#x20;
  * Specify token Symbol and source of Underlying Price\
    Example:
    * Name: PT-sUSDE-25SEP2025 (Chainlink)
      * Underlying feed: sUSDe/USD (Chainlink)

- market
  *   Pendle Market address

      <figure><img src="../.gitbook/assets/Screenshot 2025-08-05 at 19.23.34 (1).png" alt=""><figcaption></figcaption></figure>
- UnderlyingPriceFeed
  * The feed contract is able to fetch price of PT token in terms of SY token from the Pendle Market and then multiplies it by SY price in terms of USD ⇒ underlying feed is an intended method to price SY in terms of USD.
- priceToSy
  * _**Most likely you need to check this box**_ (if on the previous step you set underlying price feed to be equal to SY price)
  * If you don't check this box, you will need to use asset price as underlying price feed. (read more about the difference between Asset and SY [here](https://docs.pendle.finance/Developers/Contracts/StandardizedYield#asset-of-sy--assetinfo-function))
- twapWindow
  * The window length in seconds for averaging market price
  * Value of 1800s was usually used for previous deployments

</details>

<details>

<summary>Curve Stable</summary>

**Click New Feed and select Curve\_stable type**

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

### _Config parameters:_

* **Name**
  * Specify pool Symbol and sources of Underlying Prices\
    Example:
    * Name: crvUSD-USDC (Chainlink)
      * [Pool](https://www.curve.finance/dex/ethereum/pools/factory-crvusd-0/deposit/)
      * Feed0: Chainlink crvUSD
      * Feed1: Chainlink USDC
* **Token**
  *   LP token address

      <figure><img src="https://docs.gearbox.fi/gearbox-permissionless-doc/~gitbook/image?url=https%3A%2F%2F494588385-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F9n0QLqkiJru3BYkpyr8F%252Fuploads%252FDNyLJqP4FiZ2ieqprrRM%252Fimage.png%3Falt%3Dmedia%26token%3Da94cbfe5-0096-4e51-a6a4-431cf0433eaf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=2912918f&#x26;sv=2" alt=""><figcaption></figcaption></figure>

- **Pool**
  *   The address of the pool

      <figure><img src="https://docs.gearbox.fi/gearbox-permissionless-doc/~gitbook/image?url=https%3A%2F%2F494588385-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F9n0QLqkiJru3BYkpyr8F%252Fuploads%252FQU3m8Ui1TQBK31vk8eZ7%252Fimage.png%3Falt%3Dmedia%26token%3D2e363ea8-33aa-4be3-8b15-a8baa8faea65&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=392f40bc&#x26;sv=2" alt=""><figcaption></figcaption></figure>
- underlyingPriceFeed 0/1/2/3
  * Select a feed from allowed list to price pool's tokens at given indexes
  * If pool has only 2 tokens in it, specify only underlyingPriceFeed0 & 1

</details>
