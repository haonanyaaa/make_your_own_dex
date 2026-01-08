# Replica of a Dex

Follow the uniswapV3 development [book](https://uniswapv3book.com/milestone_0/introduction-to-markets.html) to recreate a dex.

## how centralized exchanges works?

All centralized exchanges have an **order book** at their core. An order book is just a journal that stores all the sell and buy orders that traders want to make. Each order in the order book contains a **price** the order must be executed at and the **amount** that must be bought or sold.

For trading to happen, there must exist **liquidity**, which is the availability of the assets on a market. In another words, liquidity is how easily you can buy/sell an assert without significantly moving the price.

On centralized exchanges, the order book is where liquidity is accumulated. if somenone places a sell order, they provide liquidity to the market. If someone places a buy order, they expect the market to have liqudiity, otherwise, no trade is possible.

when there's no liquidity, but markets are stll interested in trades, **market makers** come into play. A market maker is a firm or an individual who provides liquidity to markets, this is someone who has a lot of money and who buys different assets to sell them on exchanges. For this job market makers are paid by exchanges. **Market makers make money by providing liquidity to exchanges.**

## How Decentralized Exchanges Work

### Automated Market Makers

An AMM is a set of smart contracts that define how liquidity is managed. Each trading pair is a separate contract that stores both ETH and USDC and that's programmed to mediate trades: exchanging ETH for USDC and vice versa.

The core idea is **pooling**: each contract is a pool that stores liquidity and lets different users trade in a permissionless way. There are two roles, **liquidity providers** and **traders**, and these roles interact with each other through pools of liquidity, and the way they can interact with pools is programmed and immutable.

The smart contracts are fully automated and not managed by anyone.

## Constant Function Market Makers

$$ x * y = k $$
where x and y are pool contract reservese - the amounts of tokens it currently holds. k is just their product.

The constant function formula says: **after each trade, k must remain unchanged**. When traders make trades, they put some amount of one token into a pool and remove some amount of other token from the pool.

## The Trade Function

The formula for repersenting trading in the pool.
$$ (x + r\Delta x)(y - \Delta y) = k $$

1. There's a pool with some amount of token 0 (x) and some amount of token 1 (y).
2. When we buy token 1 for token 0, we give some amount of token 0 to the pool ($\Delta x$).
3. The pool gives us some amount of token 1 in exchange ($\Delta y$)
4. The pool also takes a small fee ($ r = 1 - swap\ fee $) from the amount of token 0 we gave.
5. The reserve of token 0 changes ($ x + r \Delta x$), and the reserve of token 1 changes as well ($ y - \Delta y$).
6. The product of updated reserves must still equal k.

The job of the pool is to give us a correct amount of token 1 calculated at a fair price. **Pools decide what trade prices are.**

## Pricing

How do we calculate the prices of tokens in a pool?
the law of supply and demand. The price of of tokens in a pool are determined by the supply (**the amounts of reserves of the token**) that the pool is holding. Token prices are relations of reserves:
$$ P_x = \frac{y}{x}, \ \ P_y = \frac{x}{y} $$
where $P_x$ and $P_y$ are prices of tokens in terms of the other token.

Such prices are called **spot prices** and they only reflect current market prices. **High demand increases the price**, and we use pool reserves to measure the demand: the more tokens you want to remove from a pool, the higher the impact of demand is.
$$ (x + r\Delta x)(y - \Delta y) = k  \\ \Delta y = \frac{y r \Delta x}{x + r \Delta x} \ \  \Delta x = \frac{x \Delta y}{r (y - \Delta y)}$$

In conclusion:

1. Before a trade, there's a spot price, its equal to the relation of reserves, the price is the slope of the tangent line at the starting point.
2. After a trade, there's a new spot price where the price is the slop of the tangent line.
3. The actual price of the trade is the slopes of the line connecting the two points.
