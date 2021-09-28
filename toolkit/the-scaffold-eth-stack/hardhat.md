---
description: >-
  Scaffold-eth wraps the Hardhat Ethereum development environment and makes
  deploying and testing smart contracts super easy.
---

# 👷‍♂️ Hardhat

Hardhat is a powerful toolset that includes a local chain, contract compiling, contract deployment, and testing. We highly encourage you to [read the docs](https://hardhat.org/getting-started/) and go through the [Hardhat intro tutorial](https://hardhat.org/tutorial/). Doing so will give you a foundational knowledge of what is happening under the hood with scaffold-eth and will help you debug and troubleshoot.   
  
Hardhat docs: [https://hardhat.org/getting-started/](https://hardhat.org/getting-started/)  
Hardhat intro tutorial: [https://hardhat.org/tutorial/](https://hardhat.org/tutorial/)

Out of the box Scaffold-eth will have the following file structure under `packages/hardhat/`

```text
├── contracts
│   ├── YourContract.sol
├── deploy
│   ├── 00_deploy_your_contract.js
├── scripts
│   ├── deploy.js
│   ├── publish.js
│   └── watch.js
├── test
|   ├── myTest.js
├── hardhat.config.js
└── package.json
```

`contracts` is where you will add and edit your smart contracts. 

`deploy` is where your main deploy script lives. When you create a new smart contract this is where you will reference it in order to deploy it the network specified in `hardhat.config.js`. 

`scripts` is where you might keep your helper scripts, such as `publish.js` which publishes a specified subgraph to The Graph. Or you might have a script to mint a series of NFTs.   
  
`test` is where you will keep your test suite for your smart contracts. 

`hardhat.config.js` is where you will specify the network to deploy your smart contracts to on `yarn deploy`, provide Infura keys for each network, specify your desired solidity compiler versions, etc. 

`package.json` is where your dependencies and `npm` scripts are specified.   
  
Please read the [Hardhat docs](https://hardhat.org/getting-started/) in order to get a full understanding of these directories and their contents. 

