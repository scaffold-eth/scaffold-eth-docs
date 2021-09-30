# 📜 Adding a New Contract

TL;DR ..... \(To be added\)

If we open [http://localhost:3000](http://localhost:3000/) we should see `YourContract.sol` displayed.

[![Screen Shot 2021-08-24 at 12 28 21 PM](https://user-images.githubusercontent.com/22862292/130670337-0222dc8d-9fb5-4772-b1c1-04d79a389b97.png)](https://user-images.githubusercontent.com/22862292/130670337-0222dc8d-9fb5-4772-b1c1-04d79a389b97.png)

`YourContract.sol` lives in `packages/hardhat/contracts`.

Let's add a new contract. Begin by creating a new file `NewContract.sol` in `packages/hardhat/contracts`.

We can easily populate the file by copy and pasting `YourContract.sol`, changing the contract name, and maybe changing the `purpose` variable.

```text
pragma solidity >=0.8.0 <0.9.0;
//SPDX-License-Identifier: MIT

import "hardhat/console.sol";
//import "@openzeppelin/contracts/access/Ownable.sol"; //https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable.sol

contract NewContract {

  //event SetPurpose(address sender, string purpose);

  string public purpose = "Learn Scaffold-eth";

  constructor() {
    // what should we do on deploy?
  }

  function setPurpose(string memory newPurpose) public {
      purpose = newPurpose;
      console.log(msg.sender,"set purpose to",purpose);
      //emit SetPurpose(msg.sender, purpose);
  }
}
```

Once we have saved `NewContract.sol` let's add it to our deployment in `packages/hardhat/deploy/00_deploy_your_contract.js`.

[![Screen Shot 2021-08-24 at 12 39 30 PM](https://user-images.githubusercontent.com/22862292/130671772-ebc29781-05a1-4ce5-b811-b44be4eac696.png)](https://user-images.githubusercontent.com/22862292/130671772-ebc29781-05a1-4ce5-b811-b44be4eac696.png)

Now we can add a new `<Contract />` component to our frontend at the `"/"` path in our `App.jx` located at `packages/react-app/src`.

[![Screen Shot 2021-08-24 at 12 41 01 PM](https://user-images.githubusercontent.com/22862292/130671968-d9636179-e8cf-4d66-aae6-315bbc309b8d.png)](https://user-images.githubusercontent.com/22862292/130671968-d9636179-e8cf-4d66-aae6-315bbc309b8d.png)

Run `yarn deploy` to deploy `NewContract.sol` and we should see our new contract displayed on the frontend!

[![Screen Shot 2021-08-24 at 1 14 54 PM](https://user-images.githubusercontent.com/22862292/130676210-1cb41f08-ddfc-4355-9a2e-0f9024a5d743.png)](https://user-images.githubusercontent.com/22862292/130676210-1cb41f08-ddfc-4355-9a2e-0f9024a5d743.png)

We've just learned how to quickly implement and deploy a new contract in scaffold-eth 🚀 We can start pulling in other contracts and playing with functionality blazing fast 🔥 Boom! Middle rolls!

