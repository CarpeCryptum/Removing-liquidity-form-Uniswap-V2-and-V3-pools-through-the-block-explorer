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

![image](https://github.com/CarpeCryptum/pics/blob/main/Screenshot%202025-01-08%20at%2013.28.46.png)

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
![image](https://github.com/CarpeCryptum/pics/blob/main/Screenshot%202025-01-08%20at%2014.56.06.png)

# Removing liquidity from V3 pools through NFPM contract
Example on Arbitrum

1. Go to NonfungiblePositionManager contract address on the block explorer (for the desired chain - here we use an Arbitrum example) and select "Read contract"/"Read as proxy"
([https://arbiscan.io/address/0xC36442b4a4522E871399CD717aBDD847Ab11FE88#readProxyContract](https://arbiscan.io/address/0xC36442b4a4522E871399CD717aBDD847Ab11FE88#readProxyContract))
2. Scroll down to 11.positions, click on it and enter the ID of the NFT token that represent your liquidity postion. Then click "query"
3. Copy the liquidity amount ![image](https://github.com/CarpeCryptum/pics/blob/bb87fb890ed366f0bd74b4ccb8b8f8af0a6c7c46/Screenshot%202023-09-16%20at%2015.57.00.png)

4. Select "Write contract"/Write as proxy"
5. Connect to web3
6. Scroll down to 5.decreaseLiquidity and click on it
7. In the first field (decreaseLiquidity) put 0, in the second put the params, which are as follow: your token ID, your liquidty amount (the one you coppied from "Read Contract"), the minimum amopunt of the first token (token0) you would accept, the mininimum amount of second token (token1) you would accept, deadline(the date - in unixtimestamp - after which the transaction should fail if have not been processed yet). Keep in mnind that token amounts should be in unit 256, so check the decimals of each token
![image](https://github.com/CarpeCryptum/pics/blob/f2334cbb80fbbfd28a5eaa4b5e5d00ee5912c83b/Screenshot%202023-09-16%20at%2017.41.52.png)
8. Click "write". If the transaction cost shown on user's wallet is too high it means there is a problem, so should not be confiremed. Have to check all the data and if there are no errors may simulate the transaction on Tennderly to see what the problem may be.
9. After successfull decreaseLiquidity transaction go to 3.collect. In the first field (collect) put 0. In the second field put the following params: your token ID, **YOUR ADDRESS**, max amount of token0 you want to receive, max amount of token1 you want to receieve (max amounts can be any nuber greater than the number of tokens your postions holds).
![image](https://github.com/CarpeCryptum/pics/blob/ad8e46dfd009bc335458fc3cba30f9574629b29b/Screenshot%202023-09-16%20at%2018.00.36.png)
10. Click "write". If the transaction cost shown on user's wallet is too high it means there is a problem, so should not be confiremed. Have to check all the data and if there are no errors may simulate the transaction on Tennderly to see what the problem may be.
