# Layer 2 Architecture

Aevo’s smart contracts run on the Aevo Rollup, an EVM-based Ethereum optimistic roll-up. Trades are created and settled on the smart contracts which live on the Aevo Rollup. The Aevo Rollup is operated in collaboration with Conduit.

Conduit operates a sequencer for the Aevo Rollup that posts batches of transactions to Ethereum Mainnet every _1 hour._ The dispute period for transactions on the Aevo Rollup is _2 hours_. This means that when after transactions are posted onto Ethereum Mainnet, it takes 2 hours for them to be fully confirmed. In practice, this means that withdrawals from Aevo will take anywhere between 2-3 hours to be fully confirmed.

Deposits into the Aevo Rollup use the [Optimism Standard Bridge.](https://community.optimism.io/docs/developers/bridge/standard-bridge/) The Standard Bridge is composed of two main contracts the [L1StandardBridge](https://github.com/ethereum-optimism/optimism/blob/master/packages/contracts/contracts/L1/messaging/L1StandardBridge.sol) (for Layer 1) and the [L2StandardBridge](https://github.com/ethereum-optimism/optimism/blob/master/packages/contracts/contracts/L2/messaging/L2StandardBridge.sol) (for Layer 2). Deposits into Aevo Rollup take the same confirmation time as a regular Ethereum Mainnet transaction, which is approximately \~10 minutes.

Gas fees for transactions in the Aevo Rollup are paid in Ether. The majority of this cost goes to placing the batch of transactions’ calldata on Ethereum Mainnet. Currently, the gas fees for trading paid for by the Aevo Exchange, whereas the gas fees for depositing and withdrawing will be paid by the user.

#### Below are the actions that incur gas fees:

* Settling trades - fees are borne by the exchange.
* Deposits - fees are borne by the depositor.
* Withdrawals - fees are borne by the withdrawer.

#### What does not incur gas fees:

* Creating an order
* Cancelling an order
