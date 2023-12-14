# On-chain Settlement

Users’ funds and positions remain on-chain at all time, within the Aevo smart contracts. This means that all flow of funds happen within smart contracts, including option settlements, funding payments, and exchanging of option premium.

Let us walk through an example. Alice and Bob are trading an ETH call with strike price $2500. Price of ETH-03062022-2500-C is $2 per contract, and Alice buys 100 contracts from Bob.

<table><thead><tr><th width="201">Alice</th><th width="165">1000</th><th>0</th></tr></thead><tbody><tr><td>Bob</td><td>1000</td><td>100</td></tr></tbody></table>

<table><thead><tr><th width="201">Alice</th><th width="165">800</th><th>100</th></tr></thead><tbody><tr><td>Bob</td><td>1200</td><td>0</td></tr></tbody></table>

