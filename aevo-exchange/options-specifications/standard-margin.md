# Standard Margin

By default, all accounts use Standard Margin. Standard Margin evaluates the margin for every position on a user's portfolio individually, not holistically. For example, it does not take into consideration offsetting or correlated positions.

### Initial Margin

Long call/put:\
`Quantity * Limit`

Short call:\
`Maximum (0.15 - OTM Amount/Spot, 0.1) * Spot + Mark Price of the Option`

Short put:\
`Maximum(Maximum (0.15 - OTM Amount/Spot, 0.1) * Spot + Mark Price of the Option, Maintenance Margin)`

### Maintenance Margin

Long call/put:\
`None`

Short call:\
`0.1 * Spot + Mark Price of the Option`

Short put:\
`Maximum (0.1 * spot, 0.1 * Mark Price of the Option) + Mark Price of the Option`
