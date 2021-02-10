# Headers
| UMIP-#     |                                                                                                                                          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------|
| UMIP Title | Add UNI V2 WBTC/ETH LP as a whitelisted collateral currency              |
| Authors    | Dev-1 (dev-1-lp-dollar), Dev-2 (dev-2-lp-dollar) |
| Status     | Draft                                                                                                                                    |
| Created    | February 09, 2021                                                                                                                        |
 
## Summary (2-5 sentences)
This UMIP will add UNI V2 WBTC/ETH tokens as an approved collateral currency. This will involve adding the currency to the whitelist and adding a flat final fee to charge per-request. The proposed final fee is 0.00000025 UNI V2 WBTC/ETH LP per request, as the USD price of UNI V2 WBTC/ETH is ~$2009388526, this roughly translates to a little over $%00 USD.

## Motivation
UNI V2 WBTC/ETH LP is a product of one of the most popular decentralized finance protocol's - Uniswap, which currently locks up and handles billions of dollars worth of assets. This currency is one of the largest by market capitalization for a CFMM (constant function market maker) with $345 million in liquidity. The underlying assets of this currency are ETH and WBTC, a currency pegged to Bitcoin. Both are widely used across the cryptocurrency space, and the crypto-pairs account for a large share of trading volume.
 
UNI V2 WBTC/ETH LP as collateral types are expected to have a variety of deployments. They will open the door for the creation of synthetic assets with CFMM positions. This is a progressive step for UMA as it is a much more capital efficient version of already existing whitelisted collateral currencies (ETH and [W]BTC). Enabling this collateral type will be enabling the use of productive assets, one of the better qualities of the decentralized finance markets.

## Technical Specification
To accomplish this upgrade, two changes need to be made:

- The UNI V2 WBTC/ETH LP address, 0xBb2b8038a1640196FbE3e38816F3e67Cba72D940, needs to be added to the collateral currency whitelist introduced in UMIP-usd-uni-v2-wbtc-eth.md.
- A final fee of 0.00000025 needs to be added for UNI V2 WBTC/ETH LP in the Store contract.


## Rationale
The rationale behind this change is giving deployers more useful collateral currency options. This is an advancement into a better type of collateral.

~$500 USD equivalent was chosen as the final because this is equivaelnt with breathing room above the mimimum equivalent to the final fee of already approved coins, to account for potential volatility.

## Implementation

This change has no implementation other than proposing the two aforementioned governor transactions that will be proposed.

## Security considerations
Since the underlying tokens ETH and WBTC are persistently valuable tokens, including the packaged version from the Uniswap product as supported collateral currencies should impose no additional risk to the protocol.

The main implication is for contract deployers and users who are considering using contracts with this asset as the collateral currency. They should recognize and accept the volatility risk of using this, and ensure appropriate required collateralization rations (120%+), as well as a network of liquidator and support bots to ensure solvency.

As mentioned above, the asset is packaged from Uniswap, a decentralized protocol on the Ethereum blockchain. Uniswap is one of the most popular, proven, and secure smart contract protocols to exist in decentralized finance and beyond. They've succesfully locked up and handled billions of dollars over the course of multiple years, with multiple extensive auditing from top names in the industry. There is the theoretical risk that the WBTC/ETH pool on Uniswap could be exploited and lead to a rapid loss of value in the currency proposed here which would require fast response to ensure solvency for any financial products built using this as a collateral type. However, due to the nature of Uniswap's long-proven track record around quality and security this is extremely unlikely. 

The new price identifier, that is intended to be used with this collateral currency, will need to be specified to 18 decimals of precision in order to comply with UNI V2 WBTC/ETH LP's precision.
