> **_NOTE_**<br>
> PLEASE KEEP IN MIND THAT ALL VALUES (AMOUNTS, ADDRESSES, ETC..) ARE JUST FOR EXAMPLE. WHEN INTERACTING WITH THE SMART CONTRACTS USERS SHOULD USE THEIR OWN WALLET ADDRESSES, CORRESPONDING CONTRACT ADDRESSES AND AMOUNT VALUES !!!

# Removing liquidity from V2 pools through UniswapV2Router02 contract
Example is on Ethereum mainnet

Before removing the liquidity through the UniswapV2Router02 contract, the users have to approve the router address as a spender for their LP (UNI-V2) tokens:

1. Go to the pool address on the block explorer and select “Write contract” ([https://arbiscan.io/address/0x176542be47040929a34591367f243f83c1ee13de#writeContract](https://etherscan.io/address/0xa478c2975ab1ea89e8196811f51a7b7ade33eb11#writeContract))

2. Connect your wallet (Connect to Web3)

3. Click on “approve”

4. In the first filed enter the UniswapV2Router02 contract address - 0x7a250d5630B4cF539739dF2C5dAcb4c659F2488D

5. In the second put the amount of LP owned by the user (or put even higher one), in this example - 205145344937454235 (unit256)

6. Click “write”



### Interacting with the V2 Router 
With the Uniswap V2 router, there are different functions for the different types of pools. 
- removeLiquidity (for pools where neither token is the chain's native coin), 
- removeLiquidityEth (for pools where one of the tokens is the chain's native coin) 
- removeLiquidtyEthSupportingFeeOnTransferTokens. The example (on Arbitrum chain) will use removeLiquidity function, but the principle is the same and for the rest.

1. Go to the V2 router address on the block explorer and select “Write contract” ([https://etherscan.io/address/0x7a250d5630b4cf539739df2c5dacb4c659f2488d#writeContract](https://etherscan.io/address/0x7a250d5630b4cf539739df2c5dacb4c659f2488d#writeContract))

2. Connect your wallet (Connect to Web3) 

3. Scroll to 3.removeLiquidity

4. For “tokenA” put the token0 address - *0x6B175474E89094C44Da98b954EedeAC495271d0F*

5. For “tokenB” put token1 address - *0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2*
*Tokens positions can be seen on the pool contract - Read Contract->token0/token1

6. Under “liquidity” put the amount of SLP owned by the user - *205145344937454235* (unit256)

7. In “amountAMin” put the minimum amount of token0 the user agrees to receive - *21500000000000000000* (that’s 21.5 in uint256, as the token - DAI -  is with 18 decimal) *

8. In “amountBMin” put the minimum amount of token1 the user agrees to receive - *6500000000000000* (that’s 0.0065 in uint256, as the token - WETH - is with 18 decimals) *

9. For “to (address)” put **YOUR ADDRESS** - *e.g. 0x123abc456def789.....*

10. Under “deadline” put the end time (in unix timestamp) after which the transaction should be rejected if not executed within the set time period, can set timestamp like 5-10 mins in the future - *1678787791*

11. Click “write”
![image](https://user-images.githubusercontent.com/12489182/228181967-93da3b63-6477-415a-b434-ac15ca3bbd16.png)
