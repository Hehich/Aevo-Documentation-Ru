# Mark Pricing

The methodology consists in fitting a SABR model for BTC and ETH to model implied volatility using quotes data from Deribit.

Once the model is fitted, we adjust the model parameters to reflect the relationship between the realised volatility of the reference asset (ETH in our case) and the altcoin.

We also model the forward of the altcoin using perpetual futures data.

Our volatility model is refreshed every 15 minutes, while spot prices data is continuously updated.

To read more about our pricing methodology, you can download our short paper here:&#x20;

{% file src="../../.gitbook/assets/Aevo_Altcoin_Pricing.pdf" %}
