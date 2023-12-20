# Ставка Финансирования Бессрочных Фьючерсов

Ставки финансирования - это периодические платежи, которые осуществляются между трейдерами в длинных и коротких позициях по типу peer-to-peer (одноранговой сети)

Выплаты ставки финансирования производятся каждый час

The funding payments are made every 1 hour.

***

### Расчет Ставки Финансирования <a href="#h_0041d9bda9" id="h_0041d9bda9"></a>

Ставка финансирования для каждого периода финансирования может быть рассчитана следующим образом:

```
FundingRateForPeriod = (MarkPriceTWAP - IndexPriceTWAP) / IndexPriceTWAP / 24 hours
```

Средневзвешенная по времени цена для цены отметки и индексной цены берутся за 30 минут до начала периода финансирования