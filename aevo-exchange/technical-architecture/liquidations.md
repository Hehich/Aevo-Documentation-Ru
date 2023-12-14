# Liquidations

### Liquidation Criteria <a href="#h_bb393f5de3" id="h_bb393f5de3"></a>

Since the exchange runs on cross-margin, the trader’s entire portfolio is considered when evaluating liquidation. The liquidation process is kicked off when the risk engine evaluates an account and identifies that it has breached the requirements below:

```
AB - OO - MM > 0
```

* AB = Account Balance
* OO = Total value of Open Orders
* MM = Maintenance Margin of existing positions

### Liquidation Process <a href="#h_ba0f5795eb" id="h_ba0f5795eb"></a>

During the Liquidation Process, the trader’s account is taken over by the Liquidation Engine and they are unable to open new orders.

After each step of the process, the liquidation engine re-evaluates the account’s health. If the account’s equity is still below the maintenance margin, the liquidation engine proceeds to the next step.

1. The account goes into liquidation mode. The account is under the liquidation engine’s control and new positions cannot be entered or closed by the user. The account’s open orders are forcefully cancelled by the trading system in order to free up collateral.
2. The liquidation engine performs incremental liquidation of short positions on the orderbook. Limit orders to reduce the position are created every 2 seconds, for a maximum duration of 30 seconds. Every matched quantity will incur a liquidation fee.
3. If the position cannot be liquidated with the orderbook, the liquidation engine will perform a trade with the insurance fund at a markup. The liquidation fee is also charged on this trade.
4. If there is a scenario where the insurance fund is not sufficient to payout the long option positions on settlement, the exchange has to conduct an auto-deleveraging of the most profitable traders. Existing long positions are closed at the mark price.
5. In the event that there is not enough collateral to pay the long option positions on settlement, the insurance fund pays out the difference in USDC.
