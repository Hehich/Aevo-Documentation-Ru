# Transfer a vault position

When you enter the strategy, you do not gain the vault position tokens by default. However, we expose the functionality of redeeming vault tokens for power users that need to transfer across different accounts.&#x20;

First, navigate to the Vault page on the webapp. On the right hand side, you can see the Contract Address. Click on it and go to Etherscan.

Now that you are on the contract's Etherscan/Snowscan page, you need to go to Contract > Write as Proxy.

Connect your Metamask or web wallet you want to redeem for your account.

Ctrl-F for the `maxRedeem` function. This function redeems your vault tokens from the vault itself. Click "Write" and proceed with the transaction.

Once the redeem transaction confirms, you should be able to see the vault ERC20 tokens in your wallet. You can freely transfer this ERC20 token around using your wallet.
