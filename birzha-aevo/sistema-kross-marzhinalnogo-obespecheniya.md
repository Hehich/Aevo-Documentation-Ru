# Система кросс-маржинального обеспечения

**ВАЖНО: Aevo вводит ликвидацию залогов по кросс-марже с целью повышения гибкости системы кросс-маржи. Пожалуйста, ознакомьтесь с правилами кросс-маржинальной торговли для получения более подробной информации.**



**Расчеты по криптоопционам и бессрочным фьючерсам Aevo производятся в USDC.** Помимо залога USDC, мы поддерживаем несколько видов залоговых активов, каждый из которых имеет свой коэффициент стоимости залога.

<table><thead><tr><th>Актив</th><th data-type="number">Ордер на ликвидацию</th><th>Коэффициент обеспечения</th><th>Комиссия за конвертацию</th></tr></thead><tbody><tr><td>USDC</td><td>1</td><td>100%</td><td>0.00%</td></tr><tr><td>USDT</td><td>2</td><td>99%</td><td>0.01%</td></tr><tr><td>aeUSD</td><td>3</td><td>100%</td><td>0.00%</td></tr><tr><td>ETH</td><td>4</td><td>90%</td><td>0.10%</td></tr><tr><td>WBTC</td><td>5</td><td>90%</td><td>0.10%</td></tr></tbody></table>

Стоимость залогового актива в портфеле равна:

```
Баланс * Стоимость актива в USDC * Коэффициент обеспечения
```

Исходя из ликвидности и рыночных условий, Aevo со временем будет обновлять коэффициент обеспечения.

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
