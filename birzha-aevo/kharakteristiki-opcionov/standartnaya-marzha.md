# Стандартная маржа

По умолчанию все счета используют Стандартную Маржу. Стандартная Маржа оценивает маржу для каждой позиции в портфеле пользователя по отдельности, а не комплексно. Например, она не учитывает офсетные или коррелированные позиции.



### Первоначальная маржа

Длинный колл/пут-опцион:\
`Quantity * Limit`

Короткий колл-опцион\
`Maximum (0.15 - OTM Amount/Spot, 0.1) * Spot + Mark Price of the Option`

Короткий пут-опцион\
`Maximum(Maximum (0.15 - OTM Amount/Spot, 0.1) * Spot + Mark Price of the Option, Maintenance Margin)`

### Поддерживающая маржа

Длинный колл/пут-опцион:\
`None`

Короткий колл-опцион\
`0.1 * Spot + Mark Price of the Option`

Короткий пут-опцион:\
`Maximum (0.1 * spot, 0.1 * Mark Price of the Option) + Mark Price of the Option`
