## Headers
| UMIP-uni-v2-wbtc-eth-DRAFT    |                                                                                                                                          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------|
| UMIP Title | Add uni-V2-WBTC-ETH as a price identifier              |
| Authors    | Dev-1 (dev-1-lp-dollar), Dev-2 (dev-2-lp-dollar) |
| Status     | Draft                                                                                                                                    |
| Created    | February 09, 2021   

## SUMMARY

The DVM should support price requests for Uniswap V2 WBTC-ETH LP tokens.

## MOTIVATION

The DVM currently does not support Uniswap V2 WBTC-ETH LP tokens.

By enabling uni-V2-WBTC-ETH as a price identifier, UMA will open the door for the creation of synths with CFMM (constant function market maker) LP positions. The Uniswap V2 WBTC-ETH market is one of the largest CFMM pools with $345 million in liquidity supplied as of February 09, 2021. 

The LP Dollar team will use the uni-V2-WBTC-ETH price identifier to enable fixed borrowing costs for Uniswap V2 WBTC-ETH liquidity providers.

## MARKETS & DATA SOURCES

| Uniswap V2 WBTC-ETH   |                                                                                                 |
|------------|------------------------------------------------------------------------------------------------------------------- |
| Contract Address | [0xBb2b8038a1640196FbE3e38816F3e67Cba72D940](https://etherscan.io/address/0xbb2b8038a1640196fbe3e38816f3e67cba72d940) |
| Decimals | 18 |
| Token0 Symbol  | WBTC  |
| Token0 Address  | 0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599                                                                  |
| Token0 Decimals  | 8                                                                  |
| Token1 Symbol  | WETH  |
| Token1  | 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2                                                                   |
| Token1 Decimals  | 18                                                                  |

1) First, the Uniswap V2 WBTC-ETH contract must be queried to get the total reserve balances in the pool. This query can be constructed with the Uniswap V2 subgraph or an Ethereum archive node.    
  
     Fetching total reserves balances via the [Uniswap V2 subgraph](https://thegraph.com/explorer/subgraph/uniswap/uniswap-v2):  
     
     GraphQL Request
     ``` graphql
     {
      pair(
        id: "0xbb2b8038a1640196fbe3e38816f3e67cba72d940",  
        block: {number: 11824935}
      ) {
          id
          reserve0
          reserve1
        }
     }
     ```
     
     JSON Response
     ``` json
     {
       "data": {
         "pair": {
           "id": "0xbb2b8038a1640196fbe3e38816f3e67cba72d940",
           "reserve0": "3667.03647028",
           "reserve1": "97499.896966146357068372"
         }
       }
     }
     ```
     
     Fetching total reserve balances via an archive node with [web3.js](https://web3js.readthedocs.io/en/v1.3.0/):
     
     web3.js Call
     ``` javascript
     let pair = new web3.eth.Contract(abi, "0xBb2b8038a1640196FbE3e38816F3e67Cba72D940");
     let reserves = await pair.methods.getReserves().call({}, 11824935);
     ```
     
     web3.js Response Object
     ```
     Result {
      '0': '366703647028',
      '1': '97499896966146357068372',
      '2': '1612909138',
      reserve0: '366703647028',
      reserve1: '97499896966146357068372',
      blockTimestampLast: '1612909138' }
    ```
    
2) Second, the total supply of LP tokens must be queried. The total supply is used to calculate the amount of reserves claimable by each LP token.

     Fetching total supply via the [Uniswap V2 subgraph](https://thegraph.com/explorer/subgraph/uniswap/uniswap-v2):  
     
     GraphQL Request
     ``` graphql
     {
      pair(
        id: "0xbb2b8038a1640196fbe3e38816f3e67cba72d940",  
        block: {number: 11824935}
      ) {
          id
          totalSupply
        }
     }
     ```
     
     JSON Response
     ``` json
     {
       "data": {
         "pair": {
           "id": "0xbb2b8038a1640196fbe3e38816f3e67cba72d940",
           "totalSupply": "0.167105037364528719"
         }
       }
     }
     ```
     
     Fetching total supply via an archive node with [web3.js](https://web3js.readthedocs.io/en/v1.3.0/):
     
     web3.js Call
     ``` javascript
     let pair = new web3.eth.Contract(abi, "0xBb2b8038a1640196FbE3e38816F3e67Cba72D940");
     let totalSupply = await pair.methods.totalSupply().call({}, 11824935);
     ```
     
     web3.js Response
     ```
     167105037364529719
    ```

## PRICE FEED IMPLEMENTATION

To-Do.

## TECHNICAL SPECIFICATIONS

To-Do.

## RATIONALE

To-Do.

## IMPLEMENTATION

To-Do.

## Security Considerations

To-Do.
