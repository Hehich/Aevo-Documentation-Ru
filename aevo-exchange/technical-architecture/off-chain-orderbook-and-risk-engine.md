# Off-chain Orderbook and Risk Engine

Aevo operates an off-chain order-book where maker and taker orders are posted and matched. Once a maker and taker order gets matched, only then do they get posted on Aevo’s smart contracts, which are deployed on the L2 roll-up.

Before an order is created and posted to the order-book, it is evaluated through the off-chain risk engine. The risk engine checks margin requirements for that account (either Standard Margin or Portfolio Margin) to determine if it has enough margin to create that order.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
