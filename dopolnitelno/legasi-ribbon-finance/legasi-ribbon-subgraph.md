# Легаси Ribbon Subgraph

Подграф Ribbon размещен на [The Graph](https://thegraph.com/explorer/subgraphs/7yFpkxbgeWHBcrpW3ACdk1yFSGyotaUHu8mNhmtqZYT9?view=Overview?chain=Arbitrum%20One). Если вам нужны дополнительные данные, не стесняйтесь поднимать проблему в [репозитории ribbon-subgraph](https://github.com/ribbon-finance/ribbon-subgraph) или вносить изменения.

У нас есть два подграфа, размещенных в унаследованном Graph explorer:

1. [Ribbon v2 Subgraph](https://thegraph.com/legacy-explorer/subgraph/ribbon-finance/ribbon-v2)
2. [Ribbon v1 Subgraph](https://thegraph.com/explorer/subgraph/kenchangh/ribbon-finance)

## Запросы к Хранилищам

Этот запрос возвращает первые 5 хранилищ и важную статистику о хранилище.

```
{
  vaults(first: 5) {
    id
    totalPremiumEarned
    underlyingAsset
    underlyingSymbol
  }
}
```

## Запросы о процентной ставке Хранилища

Этот запрос возвращает хронологический список значений `pricePerShare` для хранилища. `pricePerShare` показывает, сколько стоит акция хранилища в залоговом активе. Например, для хранилища ETH Theta, если значение `pricePerShare` больше 1\*10\*\*18, то хранилище является прибыльным.

```
{
  vaultPerformanceUpdates(
    where:{vault:"0x25751853eab4d0eb3652b5eb6ecb102a2789644b"},
    orderBy:timestamp, orderDirection:asc) {
    id
    pricePerShare
    timestamp
  }
}
```

## Запросы о Комиссии Хранилища

Этот запрос возвращает информацию о комиссиях хранилищ.

```
{
  vaults(first: 5) {
    id
    totalFeeCollected
    managementFeeCollected
    performanceFeeCollected
    underlyingAsset
    underlyingSymbol
  }
}
```
