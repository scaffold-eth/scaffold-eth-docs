---
description: >-
  A component for swapping erc20s on Uniswap (plus tokenlists + local forks of
  mainnet!)
---

# 🦄 Uniswapper

## Branch Info

**Author: **[Austin Griffith](https://github.com/austintgriffith)****\
**Source code:** [https://github.com/austintgriffith/scaffold-eth/tree/uniswapper](https://github.com/austintgriffith/scaffold-eth/tree/uniswapper)\
**Intended audience:** Intermediate\
**Topics:** Scaffold-eth basics, DEX

## 🏃‍♀️ Quick Start

```
git clone -b uniswapper https://github.com/austintgriffith/scaffold-eth.git uniswapper-scaffold

cd uniswapper-scaffold
```

```
yarn install
```

```
yarn start
```

* In a second terminal window run:

```
yarn fork
```

This branch uses a local fork of mainnet, which is easy to do with Hardhat ([see here to learn more](https://hardhat.org/guides/mainnet-forking.html)). The template configuration uses an Infura node, however this is not a full archive node, so it will only work for an hour or so. To get a long-lasting fork...

* Go to alchemyapi.io and get an API key for mainnet
* Replace the Infura URL with an Alchemy URL with your API key (i.e. [https://eth-mainnet.alchemyapi.io/v2/](https://eth-mainnet.alchemyapi.io/v2/)\<API\_KEY\_HERE>) into the `fork` script on line 28 of /packages/hardhat/package.json

📱 Open [http://localhost:3000](http://localhost:3000) to see the app

Notes:

* This widget uses [tokenlists](https://tokenlists.org) to import the erc20s of your choice
