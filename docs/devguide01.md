---
id: devguide01
title: Introduction
sidebar_label: Introduction
---
*Dƒusion* is a decentralized token exchange based on discrete batch auctions with multi-dimensional order books and uniform clearing prices. 

Unlike traditional exchanges with a separate order book or liquidity pool for each token pair, *dƒusion* builds a single multi-token order book, aggregating all orders between different token pairs into one holistic view.

The settlement of trades happens in discrete intervals (batches) of roughly 5 minutes. A settlement consists of:

1. *A Price Vector:* A vector with a single clearing price for each token that was exchanged in the batch. Given the vector representation, exchange rates are arbitrage-free within a settlement (e.g. <span style="color:#DB3A3D">`p(t_1,t_2) * p(t_2, t_3) == p(t_1, t_3)`</span>)
2. *Trade Execution Information:* Provided as the executed buy amounts of the orders in the batch. 

This suffices to compute the resulting allocation after all trades. A smart contract verifies that a solution is valid and adapts the resulting allocation. Anyone can submit settlements to the smart contract, as long as they are “better” than the previous solution with regards to a metric that captures “cumulative trader’s utility” of a given solution. The best solution submitted within four minutes will be the final settlement.

We believe that *dƒusion*  will be able to provide better prices than traditional exchanges, especially in highly fragmented markets. Today, those markets provide liquidity via rent-seeking agents (e.g. arbitrageurs and market makers).

Our first use case, the stablecoin market, is a great example: The US-Dollar is tokenized in many different forms (e.g. DAI, USDC, TUSD, Gemini, etc) leading to a fragmentation of liquidity on decentralized exchanges. Existing order books between each of these tokens (e.g. Gemini <=> TUSD) tend to be thin and have a high slippage. *dƒusion*  re-aggregates order books into a global multi-token liquidity pool where any token can be traded against any other.