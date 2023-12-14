# Margin Framework

On the exchange, ONLY the short-side of the option can use leverage. This means that a position can be under-collateralized as long as it fulfils the initial margin and maintenance margin requirements.

The margin system is cross-margin, meaning all positions contribute to the margin for an account, and may be put up for liquidation if an account falls below the maintenance margin (covered below).

The margin system is composed of a few key components:

* Mark pricing
* Risk engine
* Liquidation engine

### Margin Framework

Initial Margin - The amount of margin reserved to open a position.\
Maintenance Margin - The amount of margin reserved to keep a position open. This is lower than the initial margin required.

When 1) opening a new order or 2) getting into a position, we ensure that the trader has sufficient equity:

`AB + UP - OO - IM - MM > 0`

AB = Account Balance\
UP = Unrealized PnL\
OO = Total value of Open Orders\
IM = Initial Margin of new position\
MM = Maintenance Margin of existing positions

The exchange routinely evaluates accounts with existing positions to ensure that they fulfil the maintenance margin requirements:

`AB + UP - OO - MM > 0`

AB = Account Balance\
UP = Unrealized PnL\
OO = Total value of Open Orders\
MM = Maintenance Margin of existing positions

When an account breaches this requirement, the liquidation process begins.

When withdrawing from the exchange, we ensure that the trader has sufficient maintenance margin:

`AB + UP - OO - MM > 0`

AB = Account Balance\
UP = Unrealized PnL\
OO = Total value of Open Orders\
MM = Maintenance Margin of existing positions
