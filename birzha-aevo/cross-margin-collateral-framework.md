# Cross-Margin Collateral Framework

**IMPORTANT: Aevo will be introducing cross-margin collateral liquidations in order to bring more flexibility to its cross margin system. Please read the cross-margin trading rules section for more details.**



**Aevo's crypto options and perpetual futures are settled in USDC**. On top of USDC collateral, we support a few types of collateral asset, each with their own collateral value ratio.

<table><thead><tr><th>Asset</th><th data-type="number">Liquidation Order</th><th>Collateral Ratio</th><th>Convert fee</th></tr></thead><tbody><tr><td>USDC</td><td>1</td><td>100%</td><td>0.00%</td></tr><tr><td>USDT</td><td>2</td><td>99%</td><td>0.01%</td></tr><tr><td>aeUSD</td><td>3</td><td>100%</td><td>0.00%</td></tr><tr><td>ETH</td><td>4</td><td>90%</td><td>0.10%</td></tr><tr><td>WBTC</td><td>5</td><td>90%</td><td>0.10%</td></tr></tbody></table>

The value of a collateral asset in a portfolio is:

```
Balance * Price of asset in USDC * Collateral Ratio
```

Based on liquidity and market conditions, Aevo will update the collateral value ratio over time.

***

## Cross-margin Trading Rules

When a negative USDC balance is incurred AND the negative balance threshold of 100 USDC is met, the account's collateral would be auto-converted to top up the USDC balance. The auto-conversion process goes through the list of assets based on their liquidation order to convert into USDC.

There are 3 scenarios where a negative USDC balance could occur:

1. Buying an option.
2. Selling an option and it expires in-the-money (paying for settlement).
3. Realizing negative perpetual futures PNL.

### Example

1. Alice deposits 1 ETH. 1 ETH = $1000. Alice's equity is $1000.
2. Alice uses $500 to buy options. This would bring Alice's USDC balance to -$500.
3. Aevo will convert $500 of ETH into USDC. Alice's equity will still remain as $1000, but it will be composed of $500 of ETH, $0 of USDC, and $500 of ETH options.

Note: This example does not account for trading and conversion fees incurred.
