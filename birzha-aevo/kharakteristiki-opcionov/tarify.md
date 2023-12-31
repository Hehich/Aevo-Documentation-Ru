# Тарифы

### Торговые сборы

Комиссионные тейкера: 0,05% от условной суммы

Комиссионные мейкера: 0,03% от условной суммы

Комиссия за опционы никогда не может быть выше чем 12,5% от цены опциона. Например, если опцион торгуется по цене $1 (при цене ETH равной $1k), сумма комиссии составит $0.125 (вместо $0.3)



Таким образом, торговые сборы можно определить как:\
`min((taker or maker * qty * index_price), (0.125 * option_price))`

#### Примерный сценарий

Символ: ETH-30DEC22-1500-C\
Тип опциона: ETH колл-опцион\
Базовый актив: ETH\
Текущая цена: $1000\
Цель по цене: $1500\
Количество: 1 контракт\
Дата истечения срока действия: 30 декабря 2022\
Опционная премия: 20 USDC

Пользователь А устанавливает **лимитный ордер на продажу** для одного ETH-30DEC22-1500-C контракта, с ценой в 20 USDC. Пользователь Б выставляет **рыночный ордер на покупку** одного из тех же контрактов, и выплачивает опционную премию в размере 20 USDC.

Торговая комиссия, уплачиваемая пользователем А (мейкером):\
`min((0.03% * 1 * $1000), (0.125 * $20)) = min($0.45, $2.5) = $0.45`

Торговая комиссия, уплачиваемая пользователем Б (тейкером):\
`min((0.05% * 1 * $1000), (0.125 * $20)) = min($0.75, $2.5) = $0.75`

### Плата за расчеты

Когда опционы истекают в денежном выражении, происходит обмен денежными средствами между покупателями опциона и продавцами опциона. Aevo взимает комиссию за расчеты в размере **0.015%** от **номинала** опциона, срок действия которого истек.

Комиссия за расчеты никогда не может превышать 12,5% стоимости опциона.

**Комиссия за расчеты ежедневных опционов не взимается.**

#### Примерный сценарий:

Символ: ETH-30DEC22-1500-C\
Тип опциона: ETH колл-опцион\
Базовый актив: ETH\
Текущая цена: $2000\
Цель по цене: $1500\
Количество: 1 контракт\
Дата истечения срока действия: 30 декабря 2022

Пользователь А имеет 1 контракт ETH-30DEC22-1500-C, который находится "в деньгах" по истечении срока действия.

Комиссия за расчеты, оплачиваемая пользователем А:\
`min(0.015% * 1 * $2000, (0.125 * ($2000-$1500)) = min($0.3, $62.5) = $0.3`

Пользователь Б имеет 1 контракт ETH-30DEC22-2500-C, который не находится  "в деньгах" по истечении срока действия. Пользователь Б не оплачивает комиссию за расчеты.

### Комиссия за ликвидацию

Когда происходит ликвидация позиции, с ликвидируемого пользователя взимается комиссия за ликвидацию. Ликвидационная комиссия составляет **0.2%** от **номинала позиции.**

#### Примерный сценарий

Символ ETH-30DEC22-1500-C\
Тип опциона: ETH колл-опцион\
Базовый актив: ETH\
Текущая цена: $2000\
Цель по цене: $1500\
Количество: 1 контракт\
Дата истечения срока действия: 30 декабря  2022

Пользователь А имеет в короткой позиции 1 контракт ETH-30DEC22-1500-C, который в текущий момент находится "в деньгах". Поскольку у пользователя А закончилась поддерживающая маржа, он ликвидируется.

Комиссия за ликвидацию, оплачиваемая пользователем А:\
`0.2% * 2000 = $4`
