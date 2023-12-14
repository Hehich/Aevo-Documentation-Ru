# User Flow

Users can go to [otc.aevo.xyz/trade](https://otc.aevo.xyz/trade) to select their desired parameters and submit an RFQ (request for quote).

Once the parameters are selected, the indicative price that users will see on the screen is the worst possible price at which the trade will be executed.

Market makers on the other side will have 10 minutes to submit their prices, after which the best price will be selected. Once done, the market maker will have another 10 minutes to execute the trade.

Upon execution, the contract will mint oTokens representing the options on-chain, send the premium from the user to the market maker and the initial margin to the margin pool, all atomically.
