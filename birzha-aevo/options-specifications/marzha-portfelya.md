# Маржа портфеля

Маржа портфеля Aevo обеспечитвает более низкие маржинальные требования и повышенное кредитное плечо для трейдеров, которые поддерживают сбалансированный портфель хеджированных позиций. Она рассчитывается на основе модели риска, которая оценивает маржу на основе совокупных позиций счета, а не на уровне отдельных контрактов.

Маржа портфеля состоит из двух компонентов: сценарной маржи и предельной маржи.

### Сценарная маржа&#x20;

Она отражает основной риск портфеля счета, моделируя его потенциальную прибыль и убытки при различных гипотетических рыночных условиях. Aevo оценивает эту маржу на основе 15 сценариев. Каждый сценарий предполагает движение вверх/вниз цены базового актива и/или волатильности опциона. Сценарии приведены ниже.

| Сценарий | % от максимального движения спота | % от максимального IV сдвига |
| -------- | --------------------------------- | ---------------------------- |
| 1        | Up 100%                           | Up 100%                      |
| 2        | Up 100%                           | Unchanged                    |
| 3        | Up 100%                           | Down 100%                    |
| 4        | Up 50%                            | Up 100%                      |
| 5        | Up 50%                            | Unchanged                    |
| 6        | Up 50%                            | Down 100%                    |
| 7        | Unchanged                         | Up 100%                      |
| 8        | Unchanged                         | Unchanged                    |
| 9        | Unchanged                         | Down 100%                    |
| 10       | Down 50%                          | Up 100%                      |
| 11       | Down 50%                          | Unchanged                    |
| 12       | Down 50%                          | Down 100%                    |
| 13       | Down 100%                         | Up 100%                      |
| 14       | Down 100%                         | Unchanged                    |
| 15       | Down 100%                         | Down 100%                    |

| Scenario | % of Max. Spot Movement | % of Max. IV Shift |
| -------- | ----------------------- | ------------------ |
| 1        | Up 100%                 | Up 100%            |
| 2        | Up 100%                 | Unchanged          |
| 3        | Up 100%                 | Down 100%          |
| 4        | Up 50%                  | Up 100%            |
| 5        | Up 50%                  | Unchanged          |
| 6        | Up 50%                  | Down 100%          |
| 7        | Unchanged               | Up 100%            |
| 8        | Unchanged               | Unchanged          |
| 9        | Unchanged               | Down 100%          |
| 10       | Down 50%                | Up 100%            |
| 11       | Down 50%                | Unchanged          |
| 12       | Down 50%                | Down 100%          |
| 13       | Down 100%               | Up 100%            |
| 14       | Down 100%               | Unchanged          |
| 15       | Down 100%               | Down 100%          |

The Max. Spot Movement and Max. Volatility Shift are risk parameters which will be set by Aevo’s team. These parameters will be set to the following numbers during the initial phase for ETH.

<table data-header-hidden><thead><tr><th width="366"></th><th></th></tr></thead><tbody><tr><td>Parameter</td><td>Max. Move</td></tr><tr><td>Max. Spot Movement Up</td><td>20%</td></tr><tr><td>Max. Spot Movement Down</td><td>20%</td></tr><tr><td>Max. IV Shift Up</td><td>50%</td></tr><tr><td>Max. IV Shift Down</td><td>25%</td></tr></tbody></table>

Spot movements are percent movements where we increase or decrease the current observed spot price by the given magnitude. For example, if spot price currently sits at $1,400, we will run scenarios where spot price increases by 20% to $1,680 and spot price decreases by 20% to $1,120, among other scenarios.

On the other hand, IV shifts are parallel shifts where we add or subtract the current observed IV with the shift magnitude. For example, for an option which has a current IV of 60%, we will run scenarios where the IV for this option shifts up by 50% (the Max. IV Shift Up) to 110% and shifts down by 25% (the Max.IV Shift Down) to 35%. The parameters above will be assessed periodically by Aevo’s team and can be changed in the future.&#x20;

### FLOOR MARGIN&#x20;

It ensures a minimum coverage for the account’s portfolio. It’s calculated using the following formula.&#x20;

`Floor Margin = Net Short Exposure(Option) x Unit Floor Margin`

The floor margin is equal to the sum of net exposure for a given option strike in the account’s portfolio times the Unit Floor Margin. The Unit Floor Margin is a risk parameter set by Aevo’s team. This parameter will be set to 0.01 ETH. This will be assessed periodically by Aevo’s team and can be changed in the future. To provide a better understanding of how net short exposure is calculated, an example is given below.

#### Example 1.1 (Short Strangle):&#x20;

*   Account holds the following positions:

    1x ETH-26AUG22-1500-C Short (IV: 50%, Mark Price: $17.04)

    1x ETH-26AUG22-1100-P Short (IV: 50%, Mark Price: $10.54)
*   Market condition:

    Current date: 29 July 2022 (Days to Expiry: 1 month)

    Current spot price: $1,300
* Portfolio Margin:

| Scenario | Spot Movement %      | IV Shift %            | Call Option P\&L | Put Option P\&L | Total P\&L |
| -------- | -------------------- | --------------------- | ---------------- | --------------- | ---------- |
| 1        | +20% (= 100% \* 20%) | +50% (= 100% \* 50%)  | -$182.79         | -$7.26          | -$190.06   |
| 2        | +20%                 | Unchanged             | -$100.42         | $10.20          | -$90.22    |
| 3        | +20%                 | -25% (= 100% \* -25%) | -$61.46          | $10.54          | -$50.92    |
| 4        | +10% (= 50% \* 20%)  | +50%                  | -$111.34         | -$21.24         | -$132.58   |
| 5        | +10%                 | Unchanged             | -$33.23          | $8.60           | -$24.64    |
| 6        | +10%                 | -25%                  | $2.67            | $10.54          | $13.21     |
| 7        | Unchanged            | +50%                  | -$56.76          | -$44.75         | -$101.52   |
| 8        | Unchanged            | Unchanged             | $2.31            | $1.38           | $3.69      |
| 9        | Unchanged            | -25%                  | $16.71           | $10.32          | $27.04     |
| 10       | -10%                 | +50%                  | -$19.43          | -$82.54         | -$101.97   |
| 11       | -10%                 | Unchanged             | $14.75           | -$23.22         | -$8.47     |
| 12       | -10%                 | -25%                  | $17.40           | $2.52           | $19.92     |
| 13       | -20%                 | +50%                  | $2.48            | -$139.71        | -$137.22   |
| 14       | -20%                 | Unchanged             | $17.18           | -$83.30         | -$66.12    |
| 15       | -20%                 | -25%                  | $17.40           | -$58.20         | -$40.80    |

* Scenario Margin = $190.06
* Floor Margin = 2 x 0.01 ETH = 2 x (0.01 x $1,300) =$26
* Maintenance Portfolio Margin = $216.06
* Initial Portfolio Margin = $216.06 x 1.25 = $270.07
*   Margin requirement under a regular margin account:

    Initial Normal Margin = $287.08 x 1.25 = $358.85

    Maintenance Normal Margin =



    <figure><img src="broken-reference" alt=""><figcaption></figcaption></figure>

#### Example 1.2 (Bull Spread)

*   Account holds the following positions:

    1x ETH-26AUG22-1500-C Long (IV: 50%, Mark Price: $15.09)

    1x ETH-26AUG22-1700-C Short (IV: 70%, Mark Price: $10.92)
*   Market condition:

    Current date: 29 July 2022 (Days to Expiry: 1 month)

    Current spot price: $1,300
* Portfolio Margin:

| Scenario | Spot Movement %      | IV Shift %            | 1500 Call P\&L | 1700 Call P\&L | Total P\&L |
| -------- | -------------------- | --------------------- | -------------- | -------------- | ---------- |
| 1        | +20% (= 100% \* 20%) | +50% (= 100% \* 50%)  | $185.10        | -$141.30       | $43.80     |
| 2        | +20%                 | Unchanged             | $102.73        | -$57.08        | $45.65     |
| 3        | +20%                 | -25% (= 100% \* -25%) | $63.76         | -$18.57        | $45.20     |
| 4        | +10% (= 50% \* 20%)  | +50%                  | $113.65        | -$87.66        | $25.99     |
| 5        | +10%                 | Unchanged             | $35.54         | -$19.80        | $15.74     |
| 6        | +10%                 | -25%                  | -$0.36         | $3.61          | $3.24      |
| 7        | Unchanged            | +50%                  | $59.07         | -$47.25        | $11.82     |
| 8        | Unchanged            | Unchanged             | $0.00          | $0.00          | $0.00      |
| 9        | Unchanged            | -25%                  | -$14.41        | $9.88          | -$4.52     |
| 10       | -10%                 | +50%                  | $21.74         | -$19.46        | $2.28      |
| 11       | -10%                 | Unchanged             | -$12.44        | $8.11          | -$4.33     |
| 12       | -10%                 | -25%                  | -$15.09        | $10.85         | -$4.24     |
| 13       | -20%                 | +50%                  | -$0.17         | -$2.55         | -$2.72     |
| 14       | -20%                 | Unchanged             | -$14.87        | $10.46         | -$4.42     |
| 15       | -20%                 | -25%                  | -$15.09        | $10.92         | -$4.17     |

* Scenario Margin = $4.52
* Floor Margin = 1 x 0.01 ETH = 1(0.01 x $1,300) = $13
* Maintenance Portfolio Margin = $17.52
* Initial Portfolio Margin = $17.52 x 1.25 = $21.90
*   Margin requirement under a regular margin account:

    Initial Normal Margin = $140.92 x 1.25 = $176.15

    Maintenance Normal Margin =

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
