# Perpetual Futures Funding Rate

Funding rates are periodic payments that are transacted between the long or short traders peer-to-peer. Aevo exchange does not charge a fee on the funding.

The funding payments are made every 1 hour.

***

### Funding Rate Calculation <a href="#h_0041d9bda9" id="h_0041d9bda9"></a>

The funding rate for every funding period can be calculated as below:

```
FundingRateForPeriod = (MarkPriceTWAP - IndexPriceTWAP) / IndexPriceTWAP / 24 hours
```

The TWAP for mark price and index price is taken 30 minutes before the funding period begins.
