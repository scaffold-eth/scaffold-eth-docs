---
description: Start using Chainlink data feeds, VRF and more ⛓
---

# 🔮 Implementing an Oracle

### How Do Smart Contracts Use Oracles?

Oracles are most popularly used with Data Feeds. DeFi platforms like AAVE and Synthetix use Chainlink data feed oracles to obtain accurate real-time asset prices in their smart contracts.

Chainlink data feeds are sources of data aggregated from many independent Chainlink node operators. Each data feed has an on-chain address and functions that enable contracts to read from that address. For example, the ETH / USD feed.

![An Aggregator Page for ETH / USD](https://docs.chain.link/images/contract-devs/price-aggr.png)

### Using Chainlink Data Feeds

The following code is from the [Get the Latest Price](https://docs.chain.link/docs/get-the-latest-price/) page. It describes a contract which obtains the latest ETH / USD price using the Kovan testnet.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract PriceConsumerV3 {

    AggregatorV3Interface internal priceFeed;

    /**
     * Network: Kovan
     * Aggregator: ETH/USD
     * Address: 0x9326BFA02ADD2366b30bacB125260Af641031331
     */
    constructor() {
        priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);
    }

    /**
     * Returns the latest price
     */
    function getLatestPrice() public view returns (int) {
        (
            uint80 roundID, 
            int price,
            uint startedAt,
            uint timeStamp,
            uint80 answeredInRound
        ) = priceFeed.latestRoundData();
        return price;
    }
}
```

Notice how the code imports an interface called `AggregatorV3Interface`. In this case, `AggregatorV3Interface` defines that all V3 Aggregators will have the function `latestRoundData`. You can see all of the functions that a V3 Aggregator exposes in the[`AggregatorV3Interface` file on Github](https://github.com/smartcontractkit/chainlink/blob/master/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol/).

Our contract is initialized with the hard-coded address of the Kovan data feed for ETH / USD prices. Then, `getLatestPrice` uses `latestRoundData` to obtain the most recent round of price data. We're interested in the price, so the function returns that.

### &#x20;How To Deploy To Testnet

There are a few things that are needed to deploy a contract to a testnet:



*
