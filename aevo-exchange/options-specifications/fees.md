# Fees

### Trading Fees

Taker fees: 0.05% of the notional

Maker fees: 0.03% of the notional

Options fees can never be higher than 12.5% of the options price. For example, if an option is traded at $1 (ETH at $1k), the fee will be $0.125 (instead of $0.3)

Hence, trading fees can be defined as:\
`min((taker or maker * qty * index_price), (0.125 * option_price))`

#### Example Scenario

Symbol: ETH-30DEC22-1500-C\
Type: ETH Call Option\
Underlying: ETH\
Current Price: $1000\
Strike Price: $1500\
Quantity: 1 contracts\
Expiration Date: December 30, 2022\
Premium: 20 USDC

User A sets a **limit sell order** for 1 ETH-30DEC22-1500-C contract, with price 20 USDC. User B places a **market buy order** for 1 of the same contract, and pays the 20 USDC premium.

Trading fees paid by User A (Maker):\
`min((0.03% * 1 * $1000), (0.125 * $20)) = min($0.45, $2.5) = $0.45`

Trading fees paid by User B (Taker):\
`min((0.05% * 1 * $1000), (0.125 * $20)) = min($0.75, $2.5) = $0.75`

### Settlement Fees

When options expire in the money, there is an exchange of cash between buyers of the option and sellers of the option. Aevo charges a **0.015%** settlement fee on the **notional** of the option that expired in the money. This fee is charged to the holders of the option at expiry.

Settlement fees can never be higher than 12.5% of the option's value.

**Settlement fees are also not charged for Daily Options.**

#### Example Scenario

Symbol: ETH-30DEC22-1500-C\
Type: ETH Call Option\
Underlying: ETH\
Current Price: $2000\
Strike Price: $1500\
Quantity: 1 contracts\
Expiration Date: December 30, 2022

User A holds 1 contract of ETH-30DEC22-1500-C, which is in-the-money at expiry.

Settlement Fees paid by User A:\
`min(0.015% * 1 * $2000, (0.125 * ($2000-$1500)) = min($0.3, $62.5) = $0.3`

User B holds 1 contract of ETH-30DEC22-2500-C, which is out-of-the-money at expiry. User B pays no settlement fee.

### Liquidation Fees

When positions get liquidated, a liquidation fee is charged to the user that gets liquidated. The liquidation fee is **0.2% of the notional**.

#### Example Scenario

Symbol: ETH-30DEC22-1500-C\
Type: ETH Call Option\
Underlying: ETH\
Current Price: $2000\
Strike Price: $1500\
Quantity: 1 contracts\
Expiration Date: December 30, 2022

User A is short 1 contract of ETH-30DEC22-1500-C, which is currently in-the-money. Because User A runs out of maintenance margin, he gets liquidated.

Liquidation Fees paid by User A:\
`0.2% * 2000 = $4`
