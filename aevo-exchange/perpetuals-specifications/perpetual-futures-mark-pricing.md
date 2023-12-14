# Perpetual Futures Mark Pricing

The mark price of a Perpetual Future contract can be calculated with the below formula:

Mark Price = Median(Fair Price, Price 1, Price 2)

For example, if Price 1 < Price 2 < Fair Price, then take Price 2 as the Mark Price.

The definitions for Price 1, Price 2 and Fair Price are defined below.

***

### Fair Price <a href="#h_65603626e2" id="h_65603626e2"></a>

```
Fair Price = (Fair Impact Bid + Fair Impact Ask) / 2
```

The Fair Impact Bid is the average price of a $10,000 notional market sell order or [the best bid price - 0.1%](#user-content-fn-1)[^1]\*, whichever has a greater value.

The Fair Impact Ask is the average price of a $10,000 notional market buy order or [the best ask price + 0.1%](#user-content-fn-2)[^2]\*, whichever has a lower value.

***

### Price 1 <a href="#h_65603626e2" id="h_65603626e2"></a>

```
Price 1 = Index Price * (1 + Last Funding Rate * Time Until Next Funding)
```

Time Until Next Funding is the time left in hours until the next funding period. For example, if we measure Price 1, 30 minutes before the next funding period, it would be 0.5.

Below is an example, of how this works out:

```
Index Price = 2000
Last Funding Rate = 0.005
Time Until Next Funding = 0.5

Price 1 = 2000 * (1 + 0.005 * 0.5) = 2005
```

***

### Price 2 <a href="#h_867d10a2c1" id="h_867d10a2c1"></a>

```
Price 2 = Price Index + Moving Average (5-minute Basis)
```

Moving Average (5-minute Basis) = Moving Average (FairPrice - Price Index), which is continuously calculated in a 5-minute interval.

[^1]: \*Only applies to majors: ETH and BTC. Other pairs will always use the average price of a $10,000 notional market sell order.

[^2]: \*Only applies to majors: ETH and BTC. Other pairs will always use the average price of a $10,000 notional market buy order.
