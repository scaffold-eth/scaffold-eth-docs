---
description: All of the commands you can run from the root of your scaffold-eth project
---

# 🏗 Scaffold-eth commands

## Scaffold-eth Super Powers

yarn install

`yarn chain` starts a local Hardhat chain at `localhost:8545`

`yarn start` starts a react frontend server at `localhost:3000`

`yarn compile` compiles any smart contracts located at `packages/hardhat/contracts/`

`yarn deploy` deploys any smart contracts that have been specified in `00_deploy_your_contract.js` located at `packages/hardhat/deploy/`

`--------------------`

`yarn build ` builds the react-app frontend

`yarn fork` starts a local Hardhat chain with the state of the last `mainnet` block

`yarn test` runs any tests located at `packages/hardhat/test/`

`yarn verify`:upside_down: local 

`yarn watch` watches for changes in `./contracts` . Upon a detected change `yarn deploy` is automatically run and contracts are re-deployed. 

`yarn accounts` provides a list of accounts that were generated and pre-funded on `yarn chain`

`yarn balance` provides a balance for a given address. Requires an address argument. ex. `yarn balance 0x0000000000000000000000000000000000000000`. 

`yarn send` :upside_down: local  - requires a bit more documentation, likely not super useful, does it need to be in repo/docs? code located at bottom of `hardhat.config.js`

`yarn ipfs`:upside_down: publishes a document or file structure to IPFS. Make sure to have your own IPFS INFURA keys implemented at .... where is the IPFS INFURA key? 

`yarn surge`:upside_down: publishes your frontend app to Surge. - ADDITIONAL documentation needed

`yarn balance`provides a balance for a given address. Requires an address argument. ex. `yarn balance 0x0000000000000000000000000000000000000000`

`yarn s3` publishes your frontend app to an AWS s3 bucket. Requires an `aws.json` credentials file at `packages/react-app/` with `{ "accessKeyId": "xxx", "secretAccessKey": "xxx", "region": "xxx" }` . You will also want to set you bucket name at `packages/react-app/scripts/s3.js`

 :ship:` yarn ship` runs yarn surge, but with a :ship: emoji.

`yarn generate` :upside_down: displays - generates a new Ethereum address, sets that address as the 'deployer' address in WHERE DOES IT SET AT GENERATOR?, and stores the nemonic at `packages/hardhat/*newAddressValue*.txt`

`yarn account`displays a QR code of the most recently generated account using `yarn generate` and displays the addresses balance on the most common networks. 

`yarn mineContractAddress `:upside_down: - requires more documentation. There are arguments required that are not clear. 

`yarn wallet` generates a new Ethereum address and provides a localhost URL with the private key appended. This allows you to navigate to your Scaffold-eth build and have a new address as the signer in the top right corner. 

`yarn fundedwallet`

`yarn flatten`

`yarn clean`

`yarn run-graph-node`

`yarn remove-graph-node`

`yarn clean-graph-node`

`yarn graph-prepare`

`yarn graph-codegen`

`yarn graph-build`

`yarn graph-create-local`

`yarn graph-remove-local`

`yarn graph-deploy-local`

`yarn graph-ship-local`

`yarn deploy-and-graph`

`yarn mint`

`yarn theme`

`yarn watch-theme`
