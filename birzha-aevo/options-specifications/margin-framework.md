# Маржинальная торговля

На бирже использование плеча разрешено ТОЛЬКО для шорта опциона. Это означает, что позиция может быть недостаточно обеспеченной, при условии выполнения требований к начальному и поддерживающему обеспечению.

Система обеспечения является кросс-маржинальной, что означает, что все позиции вносят свой вклад в обеспечение счета и могут быть предоставлены для ликвидации, если баланс счета опускается ниже уровня поддерживающей маржи (о которой речь пойдет ниже). Система обеспечения включает несколько ключевых компонентов:

1. Оценка по маркерам (mark pricing)
2. Риск-менеджемент
3. Процесс ликвидации

### Как это работает

Начальная Маржа - Сумма маржи, зарезервированная для открытия позиции. Поддерживающая Маржа - Сумма маржи, зарезервированная для поддержания открытой позиции. Эта сумма ниже начальной маржи, необходимой для открытия. При 1) открытии нового ордера или 2) входе в позицию мы убеждаемся, что у трейдера достаточно собственного капитала:

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
