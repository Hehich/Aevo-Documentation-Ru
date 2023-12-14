# Composition

aeUSD maintains a 5% liquidity target _(subject to change)_. This means that aeUSD keeps 5% in aevo USDC and 95% in aevo sDAI. This allows us to facilitate 5% of redemptions atomically without having to withdraw sDAI on L1. Rebalances are performed on a daily basis by a bot, to maintain the liquidity target. sDAI is a soft-wrapper, meaning it can be redeemed for DAI and subsequently swapped for USDC atomically.

**What happens if the current liquidity ratio > liquidity target (ex: 7% in USDC)?**

Whenever there is an excess of USDC in the vault we:

1. Bridge (current % - target %) amount of aevo USDC to the mainnet L1 [swap vault](https://etherscan.io/address/0x426d1F3866BfcDF4d0efEfeD1Ba3c5E06CaECbE6) via the [L2 bridge](https://explorer.aevo.xyz/address/0x4200000000000000000000000000000000000010)
2. Swap from USDC to sDAI through 1Inch via the `execute` function
3. Bridge the sDAI back to Aevo L1 via the [L1 bridge](https://etherscan.io/address/0x4082C9647c098a6493fb499EaE63b5ce3259c574), marking aeUSD vault as the recipient
4. Mint aevo sDAI to the aeUSD vault&#x20;

This increases aeUSD exposure to sDAI and increases the APY for aeUSD holders.

**What happens if the current liquidity ratio < liquidity target (ex: 3% in USDC)?**

Whenever there is an excess of sDAI in the vault we:

1. Bridge (target % - current %) amount of aevo sDAI to the mainnet L1 [swap vault](https://etherscan.io/address/0x426d1F3866BfcDF4d0efEfeD1Ba3c5E06CaECbE6) via the [L2 bridge](https://explorer.aevo.xyz/address/0x4200000000000000000000000000000000000010)
2. Swap from sDAI to USDC through 1Inch via the `execute` function
3. Bridge the USDC back to Aevo L2 via the [L1 bridge](https://etherscan.io/address/0x4082C9647c098a6493fb499EaE63b5ce3259c574), marking aeUSD vault as the recipient
4. Mint aevo USDC to the aeUSD vault&#x20;

This increases aeUSD exposure to USDC in order to facilitate withdrawals.



All of the above steps are performed within the confines of smart contracts on L1 and L2.
