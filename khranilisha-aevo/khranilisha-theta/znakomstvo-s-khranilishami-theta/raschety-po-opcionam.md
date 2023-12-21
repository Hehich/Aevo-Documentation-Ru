# Расчеты по Опционам

## Цена расчетов

В настоящее время мы полагаемся на инфраструктуру Opyn для расчетов по опционам. Opyn использует спотовые цены Chainlink в качестве источника данных для расчетов по опционам.

После нескольких доработок и обучения мы решили использовать оракул [Pyth ](https://pyth.network/)для расчета цены, когда опционы истекают в деньгах. Причины следующие:



* Источник данных Chainlink не предназначен для определения истечения срока действия, поскольку он использует такие источники данных, как агрегаторы (CoinGecko или CoinMarketCap), которые часто работают с задержкой.
* Pyth обеспечивает более точное представление ценовых данных благодаря тому, что он получает данные о ценах с бирж в режиме реального времени.

## Опционы wstETH и rETH&#x20;

В хранилищах Ribbon выписываются опционы, обеспеченные ликвидными производными токенами стабфонда, такими как wstETH (Wrapped Staked ETH) и rETH (Rocket Pool ETH).

Существуют некоторые основные различия в том, как рассчитывается расчетная цена для этих опционов. Как рассчитывается расчетная цена, показано ниже:

1. Мы выясняем, за сколько stETH можно развернуть каждый wstETH.
2. С точки зрения цены мы рассматриваем 1 stETH как 1 ETH.
3. Мы устанавливаем цену истечения срока действия на цену ETH.

#### Пример

У нас есть опцион колл на ETH стоимостью 2000 долларов. В этом примере мы обеспечим колл-опцион с помощью wstETH и предположим, что 1 wstETH = 1 stETH. Если ETH окажется в деньгах по цене $2500, держатель опциона сможет потребовать $500 за обычный опцион колл на ETH, или 0,2 ETH.



In the case of wstETH, 0.2 wstETH can be claimed at expiry. However, 0.2 wstETH can only be traded for 0.19 ETH on liquidity pools like Curve, which means the option holder would have 5% less profits if they swapped back to ETH after claiming.

The implications for this are:

* wstETH options have the same payoff calculation as a regular ETH option, except the collateral received is wstETH, which is unwrapped for stETH.
* This means if stETH is trading 5% below the value of ETH, the amount returned from exercising the option is 5% less.
