---
description: Aevo Index Computation
---

# Index Price

Aevo uses a custom internal oracle to report the value of the various asset prices to the exchange. Aevo constructs an Index based on the spot price on various centralized exchanges.

From the constituent pairs, we exclude the exchanges that are disconnected, administratively turned off, and with detected invalid data. After that, we find the median of all data sources and remove pairs that have deviated away from the median by 0.5%. The final index price is calculated by performing a mean of the exchange prices.

### Aevo ETH Index <a href="#h_1436cb3762" id="h_1436cb3762"></a>

Exchange Pair Constituents (equally weighted):

* Coinbase: ETH-USD
* Binance: ETHUSDT, ETHBUSD
* Deribit: eth\_usd
* OKX: ETH-USDT
* BitGet: ETHUSDT
* ByBit: ETHUSD
* Huobi: ethusdt
* GateIo: ETH\_USDT
* BitFinex: tETHUSD
* Kraken: ETH/USD
* BitStamp: ethusd

**The Aevo ETH Index tracks the ETH/USDC pair.** As such, amongst the above constituents, the ones tracking ETH/USDT or ETH/USD are converted to ETH/USDC.
