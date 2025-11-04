# Configuring Adapters

## What are adapters?

The Credit Account design enables active interaction with the DeFi ecosystem while borrowing — such as swapping tokens, depositing into vaults, claiming rewards, and more. However, allowing arbitrary operations poses security risks.&#x20;

> Adapters — modular contracts that enable secure, controlled interactions with external protocols.

## Why do curators need to configure adapters?

Having adapters properly configured in the market is essential for allowing collateral swaps, 1-click leverage and other UX features of Gearbox protocol.

{% hint style="info" %}
Existing offchain infra (Front End, Liquidator) rely on router for finding paths from/to available collaterals. Router is not part of Gearbox protocol, therefore it’s not present in Bytecode repository. Router is used by Gearbox SDK to provide swap paths and it doesn’t interact with core contracts directly.
{% endhint %}

## What protocols are already integrated?

| Protocol                                                                                                                                                                                                                                                                                                                                                                            | Supported actions                                    |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| <p><em><strong>Uniswap, Sushiswap, Oku Trade</strong></em><br><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#uniswap-sushiswap-v2">V2</a>, <a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#uniswap-sushiswap-pancakeswap-iguanadex-oku-trade-v3">V3</a></p>              | Swaps                                                |
| <p><em><strong>Pancakeswap, IguanaDEX</strong></em><br><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#uniswap-sushiswap-pancakeswap-iguanadex-oku-trade-v3">V3</a>, <a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#pancakeswap-iguanadex-stableswap">StableSwap</a></p> | Swaps, Stableswap LP deposits                        |
| <p><em><strong>Balancer</strong></em><br><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#balancer-v2">V2</a>, <a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#balancer-v3">V3</a></p>                                                                                     | Swaps, V2 LP deposits                                |
| <p><em><strong>Curve</strong></em> <br><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#curve-stableswap-cryptoswap-and-stableng">Stableswap, CryptoSwap, Stable NG</a></p>                                                                                                                                                     | Swaps, LP deposits                                   |
| [_**Pendle**_](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#curve-stableswap-cryptoswap-and-stableng)                                                                                                                                                                                                                                | PT swaps                                             |
| <p><a href="https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#mellow-erc4626"><em><strong>Mellow</strong></em></a><br>ERC4626 vaults, DVstETH</p>                                                                                                                                                                                         | Instant deposits, Delayed withdrawals                |
| <p><em><strong>Velodrome, Aerodrome</strong></em> <br>V3, Stableswap</p>                                                                                                                                                                                                                                                                                                            | Swaps                                                |
| <p><em><strong>Camelot, Thena</strong> (Algebra AMM dexes)</em><br>V3</p>                                                                                                                                                                                                                                                                                                           | Swaps                                                |
| _**Napier**_                                                                                                                                                                                                                                                                                                                                                                        | PT Swaps, LP deposits                                |
| _**Convex**_                                                                                                                                                                                                                                                                                                                                                                        | Staking LP, claiming rewards                         |
| [_**Fluid DEX**_](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#fluid-dex)                                                                                                                                                                                                                                                            | Swaps                                                |
| <p><em><strong>Camelot, Thena, Quickswap</strong></em> (Algebra AMM)<br>V3</p>                                                                                                                                                                                                                                                                                                      | Swaps                                                |
| _**Trader Joe**_                                                                                                                                                                                                                                                                                                                                                                    | Swaps                                                |
| _**Infrared**_                                                                                                                                                                                                                                                                                                                                                                      | Staking LP, claiming rewards                         |
| _**Sky**_                                                                                                                                                                                                                                                                                                                                                                           | DAI - USDS conversion, Staking USDS for SKY          |
| _**Lido**_                                                                                                                                                                                                                                                                                                                                                                          | stETH - wstETH conversion                            |
| [_**ERC4626**_](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#erc4626)                                                                                                                                                                                                                                                                | Instant deposits and withdrawals (whenever possible) |
| [_**Kodiak Island**_](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters#erc4626)                                                                                                                                                                                                                                                          | Deposit into Island, Swaps in pool                   |

All the source code and audit reports of the contracts can be found in [Bytecode Repository](https://permissionless.gearbox.foundation/bytecode). Use search, click on the target contract and then **View Source** or **View Report**. All the Adapters can be found by searching for the ADAPTER domain in Bytecode Repository.

[setup example (BNB chain: USD1 pool, USDX collateral)](https://www.notion.so/Adapter-setup-example-BNB-chain-USD1-pool-USDX-collateral-208145c16224807fa1a0d318c01bc1ae?pvs=21)

[setup example (Ethereum chain: tBTC pool, uptBTC collateral)](https://www.notion.so/Adapter-setup-example-Ethereum-chain-tBTC-pool-uptBTC-collateral-20e145c1622480c886d8d43dc5e9f5bb?pvs=21)

[setup example (Ethereum chain: USDC pool, frxUSD/USDf collateral)](https://gearboxprotocol.notion.site/Adapter-setup-example-Ethereum-chain-USDC-pool-frxUSD-USDf-collateral-24c145c16224809d80d2d171e1128317?source=copy_link)

<details>

<summary><strong>Uniswap, Sushiswap V2</strong></summary>

## Router configuration

For the router on the chain to support swaps, Uniswap V2 worker should be configured.

It requires passing the following addresses:

* SwapRouter



*   **Add UniswapV2 adapter (requires providing router address):**

    <figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

    * Uni V2 deployment addresses: [https://docs.uniswap.org/contracts/v2/reference/smart-contracts/v2-deployments](https://docs.uniswap.org/contracts/v2/reference/smart-contracts/v2-deployments)
    * Sushi V2 deployment addresses: [https://github.com/sushiswap/v2-core/tree/master/deployments](https://github.com/sushiswap/v2-core/tree/master/deployments)



{% hint style="warning" %}
Before allowing pools in adapter, please ensure that tokens from a pair are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add WETH/USDC pool both WETH and USDC must be added before._
{% endhint %}

*   **Configure adapter to whitelist pools:**

    <figure><img src="../.gitbook/assets/Screenshot 2025-07-30 at 11.42.58.png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>
* Uni V2
  *   Configuration requires specifying tokens from a pair

      <figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>
  * Sushi V2
    *   Configuration requires specifying tokens from a pair

        <figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><strong>Uniswap, Sushiswap, Pancakeswap, IguanaDEX, Oku trade V3</strong></summary>

## Router configuration

For the router on the chain to support swaps, Uniswap V3 worker should be configured.

It requires passing the following addresses:

* SwapRouter
* QuoterV2



*   **Add UniswapV3 adapter (requires providing SwapRouter address):**

    <figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

    * Uni V3 deployment addresses: [https://docs.uniswap.org/contracts/v3/reference/deployments/](https://docs.uniswap.org/contracts/v3/reference/deployments/)
    * Sushi V3 deployment addresses: [https://github.com/sushiswap/v3-periphery/tree/master/deployments](https://github.com/sushiswap/v3-periphery/tree/master/deployments)
    * Oku Trade deployment addresses: [https://docs.oku.trade/home/extra-information/deployed-contracts](https://docs.oku.trade/home/extra-information/deployed-contracts)
    * PancakeSwap deployment addresses: [https://developer.pancakeswap.finance/contracts/v3/addresses](https://developer.pancakeswap.finance/contracts/v3/addresses)
    * IguanaDEX deployment addresses: [https://docs.iguanadex.com/iguanadex-on-mainnet/contract-addresses](https://docs.iguanadex.com/iguanadex-on-mainnet/contract-addresses)

{% hint style="info" %}
Router deployment must have bytecode of Uniswap's [SwapRouter.sol](https://github.com/Uniswap/v3-periphery/blob/v1.0.0/contracts/SwapRouter.sol) contract. Sometimes it has only [SwapRouter02](https://github.com/Uniswap/swap-router-contracts/blob/main/contracts/SwapRouter02.sol) deployment specified.\
\
On some chains that was already solved by deploying required implementation of router (see below).\
If it's not, reach out to Gearbox contributors.
{% endhint %}

* Custom SwapRouter deployments:
  * Uni V3
    * [BNB chain](https://bscscan.com/address/0xe7aC922b9751C7aca3A46D5505F36d5BbB1456b6#code)
  * Oku Trade
    * [Etherlink](https://explorer.etherlink.com/address/0x2afB54fcaECd41BE4Ecd05d7bd2e193F2F05B99d?tab=contract)
    * [Plasma](https://plasmascan.to/address/0x9Ed7DFCDE80838f9FfaF4e7fFCe5CcE4737c3e3b)

{% hint style="warning" %}
Before allowing pools in adapter, please ensure that tokens from a pair are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add WETH/USDC pool both WETH and USDC must be added before._
{% endhint %}

*   **Configure adapter to whitelist pools:**\
    &#xNAN;_&#x43;onfiguration requires specifying tokens and fee from a pair_



    <figure><img src="../.gitbook/assets/Screenshot 2025-07-30 at 12.23.10 (1).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>
*   Uni V3

    <figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>
*   Sushi V3

    <figure><img src="../.gitbook/assets/Screenshot 2025-07-30 at 12.21.22.png" alt=""><figcaption></figcaption></figure>
* [PancakeSwap](https://pancakeswap.finance/info/v3/pairs), [IguanaDEX](https://www.iguanadex.com/info/v3?chain=etherlink)

<figure><img src="../.gitbook/assets/Screenshot 2025-07-30 at 12.28.59.png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><strong>Velodrome, Aerodrome Concentrated Liquidity (Slipstream)</strong></summary>

For the router on the chain to support swaps, Uniswap V3 worker should be configured.

It requires passing the following addresses:

* SwapRouter
* Quoter



*   **Add UniswapV3 adapter (requires providing SwapRouter address):**

    <figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

    * Velodrome V3 (Slipstream) multichain deployment addresses: [https://github.com/velodrome-finance/superchain-slipstream/blob/main/deployment-addresses](https://github.com/velodrome-finance/superchain-slipstream/blob/main/deployment-addresses)
    * Aerodrome V3 (Slipstream) [https://github.com/aerodrome-finance/slipstream?tab=readme-ov-file#deployment](https://github.com/aerodrome-finance/slipstream?tab=readme-ov-file#deployment)
*   **Configure adapter to whitelist pools:**\
    &#xNAN;_&#x43;onfiguration requires specifying tokens and fee from a pair_



    <figure><img src="../.gitbook/assets/Screenshot 2025-07-30 at 12.23.10 (1).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>
*   Fee is a number specified in UI divided by 10000\
    e.g. Concentrated Volatile 100 ⇒ fee = 0.01%\
    Concentrated Stable 1 ⇒ fee = 0.0001%

    <figure><img src="../.gitbook/assets/Screenshot 2025-11-04 at 18.27.03.png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><strong>Curve StableSwap, CryptoSwap and StableNG</strong></summary>

* **How to understand what's the type of the pool of interest:**
  1. Go to the block explorer page of Curve Address provider on a chain of interest:\
     [https://docs.curve.finance/deployments/integration/](https://docs.curve.finance/deployments/integration/)
  2. Call Address Provider's get\_address method with id = 7 to get address of MetaRegistry\
     On Mainnet MetaRegistry is located [here](https://etherscan.io/address/0xF98B45FA17DE75FB1aD0e7aFD971b0ca00e379fC).
  3. Call get\_registry\_handlers\_by\_pool of MetaRegistry, passing target pool address as argument.
  4. Check non-zero address from step 3. output. It usually has clues in first lines of its code.

{% hint style="warning" %}
Before adding adapter, please ensure that tokens from a pool and pool LP token itself are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add 3Pool (USDC/USDT/DAI) adapter both USDC, USDT, DAI and 3Pool token itself must be added before._\
\
_learn how to find pool's token address below._
{% endhint %}

*   _**If the pool is not Stable NG:**_\
    &#xNAN;_&#x53;elect Curve V1 2/3/4 Assets adapter depending on the number of different tokens in target pool:_

    <figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>
*   _**If the pool is Stable NG:**_\
    &#xNAN;_&#x53;elect Curve StableNG adapter:_

    <figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
If the pool operates with non-erc20 ETH balance, deploy a ETH Gateway first and then pass it as target address.\
See the list of deployed gateways below and reach out to Gearbox team if the needed is not present.
{% endhint %}

* _**Adapter arguments:**_
  * **Target Address**
    *   The address of the pool

        <figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>
  * **LP token**
    *   The address of the pool's LP token (may be different from pool itself)

        <figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>
  * **Base Pool Address**
    * Applicable only if pool is a metapool.\
      Example: [this](https://www.curve.finance/dex/ethereum/pools/factory-v2-251/deposit/) pool has [FRAX/USDC](https://www.curve.finance/dex/ethereum/pools/fraxusdc/deposit/) as its base pool.
  * **Crypto Swap or PancakeSwap pool**
    * If Type of Pool is Crypto Swap (a.k.a Twocrypto/ Tricrypto) checkout this box.
* ETH Gateway deployments:
  * Mainnet:
    * [ETH/stETH pool](https://etherscan.io/address/0xdc24316b9ae028f1497c275eb9192a3ea0f67022) Gateway: 0x0675cb2066bacae2edfd09633d5b62be3c619a35

</details>

<details>

<summary><strong>PancakeSwap/ IguanaDEX StableSwap</strong></summary>

{% hint style="warning" %}
Before adding adapter, please ensure that tokens from a pool and pool LP token itself are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add USDX/USDT adapter both USDX, USDT and pool's LP token itself must be added before._\
\
_learn how to find pool's token address below._
{% endhint %}

*   **Select Curve V1 2 Assets adapter:**

    <figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

    * **Target Address**
      *   The address of the pool

          <figure><img src="../.gitbook/assets/Screenshot 2025-07-31 at 18.53.41.png" alt=""><figcaption></figcaption></figure>
    * **LP token**
      *   The address of the pool's LP token (can be retreived by calling token() method of pool contract)

          <figure><img src="../.gitbook/assets/Screenshot 2025-07-31 at 18.54.48.png" alt=""><figcaption></figcaption></figure>
    * **Base Pool Address**
      * Not applicable to PancakeSwap. Leave untouched.
    * **Crypto Swap or PancakeSwap pool**
      * Checkout this checkbox.

</details>

<details>

<summary><strong>Pendle</strong></summary>

## Router configuration

For the router on the chain to support swaps, Pendle worker should be configured.

It requires passing the following addresses:

* routerStatic

## Adapter configuration

*   **Add Pendle adapter (requires providing router address):**

    <figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>
* Pendle deployment addresses: [https://github.com/pendle-finance/pendle-core-v2-public/blob/main/deployments](https://github.com/pendle-finance/pendle-core-v2-public/blob/main/deployments)

{% hint style="warning" %}
Before adding pool to adapter, please ensure that pool's input token and PT token are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add Pendle pool for PT-sUSDe, both sUSDe and PT-sUSDe must be added before._
{% endhint %}

*   **Configure adapter to whitelist pools:**\
    &#xNAN;_&#x43;onfiguration requires specifying market address and input/output tokens_

    <figure><img src="../.gitbook/assets/Screenshot 2025-07-31 at 19.05.05.png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
*   _**Market:**_

    <figure><img src="../.gitbook/assets/Screenshot 2025-07-31 at 19.07.10.png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/Screenshot 2025-07-31 at 19.08.20 (1).png" alt=""><figcaption></figcaption></figure>
* _**Input token:**_\
  Select a token that is in the "1 SY Equals To" row on the screenshot above ^
* _**Pendle token:**_\
  Target PT token

</details>

<details>

<summary><strong>Fluid DEX</strong></summary>

## Router configuration

For the router on the chain to support swaps, Fluid worker should be configured.

It requires passing the following addresses:

* fluidDexResolver

{% hint style="warning" %}
Before adding pool to adapter, please ensure that pool's tokens are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add Fluid DEX for wstUSR/USDT, both wstUSR and USDT must be added._
{% endhint %}

*   **Add Fluid DEX adapter (requires providing DEX address)**

    <figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
If the pool includes ETH token, ETH Gateway must be deployed first and then be passed as target address to Fluid DEX adapter.
{% endhint %}

* Fluid deployment addresses: [https://github.com/Instadapp/fluid-contracts-public/blob/main/deployments/deployments.md](https://github.com/Instadapp/fluid-contracts-public/blob/main/deployments/deployments.md)

{% hint style="info" %}
DEX addresses have names in the similar format: **Dex\_wstUSR\_USDT.** \
Search the name based on required tokens above.
{% endhint %}

* ETH Gateway deployments:
  *   Mainnet:

      * #### Dex\_wstETH\_ETH: 0x9f294BF3201533B652aFb6B10c0385972C28a16f
      * #### ezETH\_ETH: 0xa59fc0102b7c2aee66e237ee15cb56ad58a97b2e
      * #### rsETH\_ETH: 0xb219cE3Fa907edCb375B7375F3C50d920e244bba
      *   #### weETH\_ETH:

          0x0A226E0efa6FCF26837441d623210A9464349200



</details>

<details>

<summary><strong>ERC4626</strong></summary>

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Takes ERC4626 **Vault Address** as parameter. Target vault must be added as Asset to Market and as Collateral to Credit Manager.

{% hint style="warning" %}
Before adding adapter, please ensure that token being underlying asset of a ERC4626 vault is added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add sDAI ERC4626 adapter DAI itself must be added before._
{% endhint %}

Operates using deposit, withdraw, mint and redeem functions of ERC4626 standard. Allows performing swaps from the vault’s **asset**  token into ERC4626 vault **share** token.

{% hint style="info" %}
Sometimes tokens look very much like ERC4626 but with overwritten methods, like those implementing timelocked deposits and withdrawals. \
Note that this adapter works with vanilla standard methods only. \
\
e.g. sUSDe can be minted from USDe using ERC4626 deposit interface, but has timelocked withdrawals.
{% endhint %}

</details>

<details>

<summary><strong>Kodiak Island</strong></summary>

## Router configuration

For the router on the chain to support swaps, Kodiak Island worker should be configured.

It requires passing:

* \_kodiakIslandRouter - 0x679a7C63FC83b6A4D9C1F931891d705483d4791F
* \_kodiakSwapRouter - 0xEd158C4b336A6FCb5B193A5570e3a571f6cbe690
* \_kodiakQuoter - 0x644C8D6E501f7C994B74F5ceA96abe65d0BA662B



Takes Gateway Address as parameter. On Berachain it's 0x8d41361d340515d1cdd8c369ca7b5c79f6b2e9c9.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

After adding adapter, click configure to whitelist particular Islands.

{% hint style="warning" %}
Before adding Island to adapter, please ensure that Island's tokens and Island itself are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add WBERA/iBERA Island, WBERA, iBERA and Island must be added._
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2025-08-06 at 23.21.42.png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><strong>Convex-staked Curve LP</strong></summary>

{% hint style="warning" %}
Before adding and configuring Convex pool adapters, ensure that **Curve LP token**, **Convex Deposit Token**, **Staked Phantom Token**, **CRV** and **CVX** are added as collaterals to Market and Credit Manager (everything except **Staked Phantom Token** can have zero limit, LT and feed).\
\
\
**Convex Deposit Token** can be found by its symbol. If the Curve LP token has symbol frxUSDUSDf, then Convex deposit token will have symbol cvxfrxUSDUSDf.



**Staked Phantom Token** can be found by its symbol. If the Curve LP token has symbol frxUSDUSDf, then Convex deposit token will have symbol stkcvxfrxUSDUSDf.
{% endhint %}

**Add Convex Base Reward Pool adapter.**&#x20;

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

* _**Base Reward Pool Address:**_
  *   Rewards contract address from Convex pool Info.

      <figure><img src="../.gitbook/assets/Screenshot 2025-08-11 at 18.25.08.png" alt=""><figcaption></figcaption></figure>
* _**Staked phantom token:**_
  * **Staked Phantom Token** can be found by its symbol. If the Curve LP token has symbol frxUSDUSDf, then Convex deposit token will have symbol stkcvxfrxUSDUSDf.

**Add Convex Booster adapter**

{% hint style="success" %}
If the Credit Manager already includes the Convex Booster adapter, skip it and proceed to the next step (Update Convex booster Pool IDs).
{% endhint %}

{% hint style="info" %}
Booster address is single across all chains and is suggested as default option.
{% endhint %}

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

**Update Convex booster Pool IDs**

{% hint style="info" %}
After each new Convex pool is added, Booster pool ids should be updated.
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2025-08-11 at 18.49.58.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2025-08-11 at 18.51.39.png" alt=""><figcaption></figcaption></figure>

\


</details>

<details>

<summary><strong>Balancer V2</strong></summary>

## Router configuration

For the router on the chain to support swaps, Balancer V2 worker should be configured.

Configuration requires passing:

* BalancerQueries&#x20;

Balancer deployment addresses can be found [here](https://docs-v2.balancer.fi/reference/contracts/deployment-addresses/mainnet.html).

## Adapter configuration

*   **Add BalancerV2 adapter (requires providing Vault address):**

    <figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

    * Deployment addresses: \
      [https://docs-v2.balancer.fi/reference/contracts/deployment-addresses/mainnet.html](https://docs-v2.balancer.fi/reference/contracts/deployment-addresses/mainnet.html)

{% hint style="warning" %}
Before adding adapter, please ensure that tokens from a pool and pool LP token itself are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add WETH/osETH pool to adapter both WETH, osETH and WETH/osETH token itself must be added before._\
\
_learn how to find pool's token address below._
{% endhint %}

* **Finding Pool LP Token Address:**

<figure><img src="../.gitbook/assets/Screenshot 2025-09-08 at 13.58.46.png" alt=""><figcaption></figcaption></figure>

* **Configure adapter to whitelist pools:**

<figure><img src="../.gitbook/assets/Screenshot 2025-09-08 at 13.55.44 (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

*   Configuration requires specifying PoolID which can be found on Balancer UI\


    <figure><img src="../.gitbook/assets/Screenshot 2025-09-08 at 13.53.56.png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><strong>Balancer V3</strong></summary>

## Router configuration

For the router on the chain to support swaps, Balancer V3 worker should be configured.

Configuration requires passing:

* [BalancerV3MultiActionQueries](https://github.com/Van0k/balancer-queries/blob/master/src/BalancerV3MultiActionQueries.sol) (needs to be deployed manually, reach out to contributors for support)

Balancer deployment addresses can be found [here](https://docs.balancer.fi/developer-reference/contracts/deployment-addresses/plasma.html#core-contracts).

BalancerV3MultiActionQueries deployments:

* Plasma
  * 0x1a9B1bfD35fA3932493b5f4F20Cb16b2B88Cc0C8
* Mainnet
  * 0x0BA8417d19D87b7b5C9dA8762ba505d61D1bF1E7
* Optimism
  * 0x1b8a4BA520C7789D7bE7476960B8Cdd42e57d928

## Adapter configuration

* **Add BalancerV3 adapter (requires providing Gateway address):**

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

* Gateway deployment addresses:
  * Ethereum:&#x20;
    * v3.10 (outdated) 0x21f55223de449224e8bdf4f59452e072bdf7af57
    * v3.11 (up to date) 0x8A57c21234ddc225499843F6A073dd374c952560
  * Plasma:&#x20;
    * v3.10 (outdated) 0xd5c89297ad23e12d7f0ff24112418dbe9ebeae56
    * v3.11 (up to date) 0x55109bA88c396008cfBe9F27Ad97A7e1e4394f6F
  * Optimism:
    * v3.11 (up to date) 0x77b2dfc344072fa242f2d03893ccbdbb0ef47b7c

{% hint style="warning" %}
Before adding adapter, please ensure that tokens from a pool are added as _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
&#xNAN;_&#x65;.g. to add_ waEthLidowstET&#x48;_/rstETH pool to adapter both_ waEthLidowstET&#x48;_, rstETH and_ waEthLidowstET&#x48;_/rstETH token itself must be added before._\
\
_learn how to find pool's token address below._
{% endhint %}

{% hint style="info" %}
What are _wa_-tokens?\
It's erc4626 vaults representing positions staked in Aave pools. \
To support swaps from wstETH through waEthLidowstET&#x48;_/rstETH_ boosted Balancer pool, you need to include wa-token as collateral and add erc4626 adapter with wa-token address as vault which will process swaps from wstETH to waEthLidowstETH.
{% endhint %}

* **Finding Pool LP Token Address:**

<figure><img src="../.gitbook/assets/Screenshot 2025-09-08 at 15.27.47 (1).png" alt=""><figcaption></figcaption></figure>

* **Configure adapter to whitelist pools:**

<figure><img src="../.gitbook/assets/Screenshot 2025-09-08 at 13.55.44 (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

* Configuration requires specifying Pool Address which can be found on Balancer UI

<figure><img src="../.gitbook/assets/Screenshot 2025-09-08 at 15.27.47 (2).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary><strong>Mellow ERC4626</strong></summary>

## Router configuration

For the router on the chain to support swaps, Mellow worker should be configured. Reach out to contributors for support.

{% hint style="warning" %}
Before adding adapter, please ensure that mellow vault (LRT itself) and its Withdrawal Phantom Token are added _**Assets to Market**_ and as _**Collaterals to Credit Manager**_.\
\
If the phantom token is not present in PFS, ask Gearbox contributors to help you deploy a new one.
{% endhint %}

### **Add Mellow ERC4626 adapter:**

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

* Vault address
  * Select a corresponding Mellow vault (LRT itself) that was previously added as collateral.
* Phantom Token
  * A token that tracks user's position in withdrawal queue and allows unstaking LRT right from the Credit Account.

### **Add Mellow claimer adapter:**

This adapter allows claiming unstaked tokens after the redemption request was processed.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Mellow Claimer is a contract deployed by Mellow. Deployment addresses can be found here: [https://docs.mellow.finance/multi-deployments#navigation](https://docs.mellow.finance/multi-deployments#navigation)

**Configure Mellow Claimer Adapter**

<figure><img src="../.gitbook/assets/Screenshot 2025-09-08 at 17.13.56.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

* Multi vault
  * Mellow LRT itself
* Phantom token
  * A token that tracks user's position in withdrawal queue and allows unstaking LRT right from the Credit Account.

</details>

<details>

<summary><strong>Midas (direct deposits &#x26; redemptions)</strong></summary>

Midas risks:

\- If Midas rejects a withdrawal request, a credit account that has the request rejected will have its phantom token balance locked and non-claimable. This means that de-facto the account has bad debt (that cannot be liquidated) until the situation is resolved manually

\- A gateway has a function to manually process a cancelled request by paying an amount of at least pendingTokenOutAmount for the respective credit account (the function can be called by anyone). This will allow the credit account to claim a withdrawal as if it was normally processed

\- It's best to forbid the withdrawal phantom token if there is a rejected request to Gearbox CA, since Midas might accidentally refund the withdrawal to the CA itself, leading to double counting. Forbidding the token will prevent the user to borrow and withdraw more against their collateral in this case.

{% hint style="warning" %}
For safety, each curator on each chain must have its own gateway and phantom token for each vault.
{% endhint %}

Gateway addresses:

* Plasma
  * Hyperithm Curator: 0xB375DF6a1D7a1c172e65D4FBDA2d3caa144Bf8e7

Phantom token addresses:&#x20;

* Plasma
  * Hyperithm Curator: 0x0835e60e9A56734cEE76e3953c3BE0635Fcb71d5

</details>

<details>

<summary><strong>Velodrome, Aerodrome V1 &#x26; V2 (Basic volatile and Basic stable)</strong></summary>

For the router on the chain to support swaps, Velodrome worker should be configured.

It requires passing the following addresses:

* Router



* **Add Velodrome V2 adapter (requires providing Router address):**

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

* Velodrome v2  optimism deployment addresses: [https://github.com/velodrome-finance/contracts/tree/main/deployment-addresses](https://github.com/velodrome-finance/contracts/tree/main/deployment-addresses)
*   **Configure adapter to whitelist pools:**\
    &#xNAN;_&#x43;onfiguration requires specifying tokens and fee from a pair_\
    _Look for Pool Factory in deployment addresses_

    <figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>
* Is Stable?\
  Basic stable ⇒ Stable\
  Basic volatile ⇒ not Stable

</details>
