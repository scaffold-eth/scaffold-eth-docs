---
description: Build you own decentralized token exchange!!
---

# 📉 Minimum Viable DEX

[Medium Article](https://medium.com/@austin\_48503/%EF%B8%8F-minimum-viable-exchange-d84f30bd0c90)

## 💡Introduction <a href="27e8" id="27e8"></a>

This first killer app to be built on Ethereum was the token. A standard called ERC20 emerged and now anyone can deploy a token on Ethereum in seconds.

Often, a token needs to be exchanged for value or another token and traditionally this has been facilitated by insecure centralized entities.

In 2017,&#x20;

[Vitalik Buterin](https://medium.com/u/587a00dbce51?source=post\_page-----d84f30bd0c90-----------------------------------) [proposed](https://vitalik.ca/general/2017/06/22/marketmakers.html) a method that would allow a smart contract to perform swaps between two assets using a liquidity ratio based on reserves. Eventually this became 🦄[Uniswap](https://uniswap.org) and now anyone can use uniswap.exchange to swap tokens on Ethereum.

The Uniswap contracts have moved over $1.2 BILLION USD collectively. 🤯

> Over the course of 2019, Uniswap liquidity providers earned more than $1.2 million in fees. — [Year in Eth 2019](https://medium.com/@jjmstark/the-year-in-ethereum-2019-242012e4276d)

In this tutorial, we will attempt to boil down a decentralized exchange to a few simple Solidity functions in an easy to digest smart contract. Thankfully, my buddy&#x20;

[Philippe Castonguay](https://medium.com/u/62c1161d949c?source=post\_page-----d84f30bd0c90-----------------------------------) created [uniswap-solidity](https://github.com/PhABC/uniswap-solidity) and this tutorial will use a slimmed down version of this code.

We will build a decentralized exchange to swap an arbitrary token for ETH using a liquidity pool anyone can participate in. This build will demonstrate how smart contracts can create 🤖 automatic decentralized systems using crypto-economic incentives.

## 👩‍💻 Prerequisites <a href="95ea" id="95ea"></a>

You will need [NodeJS>=10](https://nodejs.org/en/download/), [Yarn](https://classic.yarnpkg.com/en/docs/install/), and [Git](https://git-scm.com/downloads) installed.

This tutorial will assume that you have a basic understanding of [web app development](https://reactjs.org/tutorial/tutorial.html) and some exposure to [core Ethereum concepts](http://eth.build).

## 🙇‍♀️ Getting Started <a href="c0ac" id="c0ac"></a>

In 🛠 [Programming Decentralized Money](https://medium.com/@austin\_48503/programming-decentralized-money-300bacec3a4f) we introduced 🏗 [scaffold-eth](https://github.com/austintgriffith/scaffold-eth). This tutorial will use the `dex` branch of the Ethereum development scaffolding:

```
git clone https://github.com/scaffold-eth/scaffold-eth.git app
cd app
git checkout challenge-3-dex
yarn install
```

We will also want to bring up our local blockchain and deploy our contracts. In a new terminal window, run:

```
yarn chain
```

In a third terminal window, we can compile and deploy with:

```
yarn deploy
```

The app should come up at [http://localhost:3000](http://localhost:3000) and you should see:

![](https://miro.medium.com/max/30/1\*bbtUmV6xesAQkc\_WykLnvQ.png?q=20)![](https://miro.medium.com/max/700/1\*bbtUmV6xesAQkc\_WykLnvQ.png)

> ☢️. If this isn’t the header you see, you are probably on the wrong git branch.

We will also see two smart contracts displayed called `DEX` and `Balloons`.

![](https://miro.medium.com/max/21/1\*iSQ7oJDJmHuC5YCzCfXdKw.png?q=20)![](https://miro.medium.com/max/511/1\*iSQ7oJDJmHuC5YCzCfXdKw.png)

We can find these smart contracts in `packages/hardhat/contracts`:

`Balloons.sol` just an example ERC20 contract that mints 1000 to whatever address deploys it.

`DEX.sol` is what we will build in this tutorial and you can see it starts with a `SafeMath` library to help us prevent overflows and underflows and also tracks a `token` (ERC20 interface) that we set in the constructor (on deploy):

![](https://miro.medium.com/max/30/1\*oibxeIJjrhCEQEB6H-Oazw.png?q=20)![](https://miro.medium.com/max/700/1\*oibxeIJjrhCEQEB6H-Oazw.png)

> ☢️ You will find the smart contracts in `packages/hardhat/contracts`. There are other `contracts` folders so make sure you find the right one with `DEX.sol`.

## 💰Reserves <a href="b690" id="b690"></a>

As mentioned in the introduction, we want to create an automatic market where our contract will hold _**reserves**_ of both `ETH` and `🎈Balloons`. These reserves will provide `liquidity` that allows anyone to swap between the assets. Let’s add a couple new variables to `DEX.sol`:

```
uint256 public totalLiquidity;mapping (address => uint256) public liquidity;
```

These variables track the _total_ liquidity, but also by individual addresses too.

Then, let’s create an `init()` function in `DEX.sol` that is `payable` and then we can define an amount of `tokens` that it will transfer to itself:

```
function init(uint256 tokens) public payable returns (uint256) {  require(totalLiquidity==0,"DEX:init - already has liquidity");  totalLiquidity = address(this).balance;  liquidity[msg.sender] = totalLiquidity;  require(token.transferFrom(msg.sender, address(this), tokens));  return totalLiquidity;}
```

Calling `init()` will load our contract up with both `ETH` and `🎈Balloons`.

You can compile your contracts with the command `yarn run compile` and for now, just ignore any warnings. When you are ready, deploy your contracts:

```
yarn deploy
```

Your app should hot reload and the DEX contract should be at a new address. Plus, our new liquidity variables are automatically loaded into the frontend:

![](https://miro.medium.com/max/30/1\*IVqwdF1WJAEcb8qUbRN6Lw.png?q=20)![](https://miro.medium.com/max/530/1\*IVqwdF1WJAEcb8qUbRN6Lw.png)

We can see that the DEX starts empty. We want to be able to call `init()` to start it off with liquidity, but we don’t have any funds or tokens yet.

🏗 Scaffold-eth starts every user off with a temporary account on page load. Let’s copy our address in the top right:

![](https://miro.medium.com/max/30/1\*89AlwKVNUT4qqKcwx8xdUw.png?q=20)![](https://miro.medium.com/max/557/1\*89AlwKVNUT4qqKcwx8xdUw.png)

And send our account some test ETH from the faucet in the bottom left:

![](https://miro.medium.com/max/30/1\*\_vtqcaM9RcLh4n7CxuexJA.png?q=20)![](https://miro.medium.com/max/261/1\*\_vtqcaM9RcLh4n7CxuexJA.png)

Now we need some 🎈Balloon tokens! Find the `deploy.js` file in `packages/hardhat/scripts` and let’s add a line that sends our account 10 tokens (10 times 10¹⁸ because no decimals) when the contract is deployed:

![](https://miro.medium.com/max/30/1\*pft7wjyuzL\_e0C5Uyq8gaw.png?q=20)![](https://miro.medium.com/max/700/1\*pft7wjyuzL\_e0C5Uyq8gaw.png)

Now redeploy everything and we’ll see new addresses contracts, but more importantly, we should have 10 tokens sent to us on deploy:

```
yarn run deploy
```

To see our 🎈balloons in the frontend you’ll see we are using a `<TokenBalance>` component just below the `<Account>` component in `App.js`. (You can find `App.js` in the `packages/react-app/src` directory.)

![](https://miro.medium.com/max/30/1\*rV820XM\_brQnn8RJxrGnfg.png?q=20)![](https://miro.medium.com/max/663/1\*rV820XM\_brQnn8RJxrGnfg.png)

We can’t just call `init()` yet because the DEX contract isn’t allowed to transfer tokens from our account. We need to `approve()` the `DEX` contract with the Balloons UI. Copy and paste the `DEX` address and then set the _amount_ to `5000000000000000000` (5 \* 10¹⁸):

![](https://miro.medium.com/max/30/1\*BIlmUgUqi8jeUuuCaq\_0bw.png?q=20)![](https://miro.medium.com/max/450/1\*BIlmUgUqi8jeUuuCaq\_0bw.png)

If you hit the `💸` icon, it should fire off a transaction that approves the `DEX` to take 5 of your tokens. You can test this with the `allowance` form:

![](https://miro.medium.com/max/30/1\*WCki6mOPbjJcVi6LJeeSSA.png?q=20)![](https://miro.medium.com/max/473/1\*WCki6mOPbjJcVi6LJeeSSA.png)

Now we are ready to call `init()` on the `DEX`. We will tell it to take 5 (\*10¹⁸) of our tokens and we will also send 0.01 ETH with the transaction. You can do this by typing `0.01` as the _transaction value_, then hit ✳️ to do \*10¹⁸, then hit #️⃣ to convert it to hex:

![](https://miro.medium.com/max/30/1\*xy8kNk3OinTMaCAicXhQQA.png?q=20)![](https://miro.medium.com/max/404/1\*xy8kNk3OinTMaCAicXhQQA.png)

Once you hit the `💸` button your transaction will send in the ETH and the contract will grab 5 of your tokens:

![](https://miro.medium.com/max/30/1\*nhqvMnFIvsZJPkYRLXzqSA.png?q=20)![](https://miro.medium.com/max/512/1\*nhqvMnFIvsZJPkYRLXzqSA.png)

You can check how many 🎈balloons the DEX has using the UI:

![](https://miro.medium.com/max/30/1\*LaOJDdhNTK7PXme74jBgTg.png?q=20)![](https://miro.medium.com/max/479/1\*LaOJDdhNTK7PXme74jBgTg.png)

This works pretty well, but it will be a lot easier if we just call the `init()` function as we deploy the contract. In the `deploy.js` script try uncommenting the init section so our `DEX` will start with 5 `ETH` and 5 `Balloons` of liquidity:

![](https://miro.medium.com/max/30/1\*DqwSimqI5qSyBxQYyo-KNw.png?q=20)![](https://miro.medium.com/max/700/1\*DqwSimqI5qSyBxQYyo-KNw.png)

Now when we `yarn run deploy` our contract should be initialized as soon as it deploys and we should have equal reserves of ETH and tokens.

![](https://miro.medium.com/max/30/1\*K7Itfsw6S5ZwXKp7whoXGQ.png?q=20)![](https://miro.medium.com/max/557/1\*K7Itfsw6S5ZwXKp7whoXGQ.png)

## 📉 Price <a href="b20c" id="b20c"></a>

Now that our contract holds _reserves_ of both ETH and tokens, we want to use a simple formula to determine the exchange rate between the two.

Let’s start with the formula `x * y = k` where `x` and `y` are the reserves:

```
( amount of ETH in DEX ) * ( amount of tokens in DEX ) = k
```

The `k` is called an invariant because it doesn’t change _during trades_. (The `k` only changes as _liquidity_ is added.) If we plot this formula, we’ll get a curve that looks something like:

![](https://miro.medium.com/max/30/1\*xR7bcYQu9yma\_GY0g7ZnYg.png?q=20)![](https://miro.medium.com/max/700/1\*xR7bcYQu9yma\_GY0g7ZnYg.png)

💡 We are just swapping one asset for another, the “price” is basically how much of the resulting _output_ asset you will get if you put in a certain amount of the _input_ asset.

🤔 OH! A market based on a curve like this will always have liquidity, but as the ratio becomes more and more unbalanced, you will get less and less of the weaker asset from the same trade amount. Again, if the smart contract has too much ETH and not enough tokens, the price to swap tokens to ETH should be more desirable.

When we call `init()` we passed in ETH and tokens at a _ratio _of 1:1 and that ratio must remain constant. As the reserves of one asset changes, the other asset must also change inversely.

Let’s edit our `DEX.sol` smart contract and bring in a this price function:

```
function price(uint256 input_amount, uint256 input_reserve, uint256 output_reserve) public view returns (uint256) {  uint256 input_amount_with_fee = input_amount.mul(997);  uint256 numerator = input_amount_with_fee.mul(output_reserve);  uint256 denominator = input_reserve.mul(1000).add(input_amount_with_fee);  return numerator / denominator;}
```

We use the ratio of the input vs output reserve to calculate the price to swap either asset for the other. Let’s deploy this and poke around:

```
yarn run deploy
```

Let’s say we have 1 million ETH and 1 million tokens, if we put this into our price formula and ask it the price of 1000 ETH it will be an almost 1:1 ratio:

![](https://miro.medium.com/max/30/1\*4pFRMiyG-TcQBn\_nV6ZGNA.png?q=20)![](https://miro.medium.com/max/409/1\*4pFRMiyG-TcQBn\_nV6ZGNA.png)

If we put in 1000 ETH we will receive 996 tokens. If we’re paying a 0.3% fee it should be 997 if everything was perfect. BUT, there is a tiny bit of _slippage_ as our contract moves away from the original ratio. Let’s dig in more to really understand what is going on here.

Let’s say there is 5 million ETH and only 1 million tokens. Then, we want to put 1000 tokens in. That means we should receive about 5000 ETH:

![](https://miro.medium.com/max/30/1\*TNYnszjlNJiGl7rf\_YTYyw.png?q=20)![](https://miro.medium.com/max/434/1\*TNYnszjlNJiGl7rf\_YTYyw.png)

Finally, let’s say the ratio is the same but we want to swap 100,000 tokens instead of just 1000. We’ll notice that the amount of _slippage_ is much bigger. Instead of 498,000 back we will only get 453,305 because we are making such a big dent in the reserves.

![](https://miro.medium.com/max/30/1\*f9qCqv\_cy\_KY0HdwsraklA.png?q=20)![](https://miro.medium.com/max/416/1\*f9qCqv\_cy\_KY0HdwsraklA.png)

💡 The contract automatically adjusts the price as the ratio of reserves shifts away from the equilibrium. It’s called an 🤖 _Automated Market Maker_.

## ⚖️ Trading <a href="f668" id="f668"></a>

Let’s edit the `DEX.sol` smart contract and add two new functions for swapping from each asset to the other:

```
function ethToToken() public payable returns (uint256) {  uint256 token_reserve = token.balanceOf(address(this));  uint256 tokens_bought = price(msg.value, address(this).balance.sub(msg.value), token_reserve);  require(token.transfer(msg.sender, tokens_bought));  return tokens_bought;}function tokenToEth(uint256 tokens) public returns (uint256) {  uint256 token_reserve = token.balanceOf(address(this));  uint256 eth_bought = price(tokens, token_reserve, address(this).balance);  msg.sender.transfer(eth_bought);  require(token.transferFrom(msg.sender, address(this), tokens));  return eth_bought;}
```

Each of these functions calculate the resulting amount of output asset using our price function that looks at the ratio of the reserves vs the input asset.

We can call `tokenToEth` and it will take our tokens and send us ETH or we can call `ethToToken` with some ETH in the transaction and it will send us tokens.

Let’s compile and deploy our contract then move over to the frontend:

```
yarn run deploy
```

Your app UI should hot reload and show the two new functions:

![](https://miro.medium.com/max/30/1\*vtfi4XEiORt8qksyRyMyGQ.png?q=20)![](https://miro.medium.com/max/534/1\*vtfi4XEiORt8qksyRyMyGQ.png)![](https://miro.medium.com/max/30/1\*880G8iOhoGIVrDUp\_558aA.png?q=20)![](https://miro.medium.com/max/531/1\*880G8iOhoGIVrDUp\_558aA.png)

After sending our account some ETH with the faucet, we can try swapping some ETH for tokens. Let’s start with `0.001` and then hit ✳️ and then #️⃣ . Then, if we hit `💸` it will make the transaction to call `ethToToken()`:

![](https://miro.medium.com/max/30/1\*Vema3c7XWRcK0Zd1nkaZyA.png?q=20)![](https://miro.medium.com/max/481/1\*Vema3c7XWRcK0Zd1nkaZyA.png)

And our account should receive 0.001 tokens back:

![](https://miro.medium.com/max/30/1\*JboFfVjMhWi2PurMcgsW6A.png?q=20)![](https://miro.medium.com/max/148/1\*JboFfVjMhWi2PurMcgsW6A.png)

Swapping tokens for ETH is a little trickier because we have to make a transaction to `approve()` the `DEX` to take our tokens first. Let’s approve the DEX address to take 1 (\* 10¹⁸) tokens (1000000000000000000):

![](https://miro.medium.com/max/30/1\*8-s\_qcwkq8X457GWaEq9lw.png?q=20)![](https://miro.medium.com/max/482/1\*8-s\_qcwkq8X457GWaEq9lw.png)

Then let’s try to swap that amount of tokens for ETH:

![](https://miro.medium.com/max/30/1\*TtnuaEy0kmsk1oFXHf4Y1Q.png?q=20)![](https://miro.medium.com/max/489/1\*TtnuaEy0kmsk1oFXHf4Y1Q.png)

Then our ETH balance should go up by 0.85 or so:

![](https://miro.medium.com/max/30/1\*rouThK8A4LwyL6HS1TSizg.png?q=20)![](https://miro.medium.com/max/133/1\*rouThK8A4LwyL6HS1TSizg.png)

(It shows your balance in USD, but you can click it to see the exact amount:)

![](https://miro.medium.com/max/30/1\*l4aYRPWdAHG-mpb241fIHg.png?q=20)![](https://miro.medium.com/max/112/1\*l4aYRPWdAHG-mpb241fIHg.png)

🎉 We are exchanging assets! 🎊 Celebrate with some emojis! 🥳 🍾 🥂

## 💦 Liquidity <a href="a55e" id="a55e"></a>

So far, only the `init()` function controls liquidity. To make this more decentralized, it would be better if _anyone_ could add to the liquidity pool by sending the `DEX` both ETH and tokens at the correct ratio.

Let’s create two new functions that let us deposit and withdraw liquidity:

```
function deposit() public payable returns (uint256) {  uint256 eth_reserve = address(this).balance.sub(msg.value);  uint256 token_reserve = token.balanceOf(address(this));  uint256 token_amount = (msg.value.mul(token_reserve) / eth_reserve).add(1);  uint256 liquidity_minted = msg.value.mul(totalLiquidity) / eth_reserve;  liquidity[msg.sender] = liquidity[msg.sender].add(liquidity_minted);  totalLiquidity = totalLiquidity.add(liquidity_minted);  require(token.transferFrom(msg.sender, address(this), token_amount));  return liquidity_minted;}function withdraw(uint256 amount) public returns (uint256, uint256) {  uint256 token_reserve = token.balanceOf(address(this));  uint256 eth_amount = amount.mul(address(this).balance) / totalLiquidity;  uint256 token_amount = amount.mul(token_reserve) / totalLiquidity;  liquidity[msg.sender] = liquidity[msg.sender].sub(eth_amount);  totalLiquidity = totalLiquidity.sub(eth_amount);  msg.sender.transfer(eth_amount);  require(token.transfer(msg.sender, token_amount));  return (eth_amount, token_amount);}
```

Take a second to understand what these functions are doing after you paste them into `DEX.sol` in `packages/hardhat/contracts`:

The `deposit()` function receives ETH and also transfers `tokens` from the caller to the contract at the right ratio. The contract also tracks the amount of `liquidity` the depositing address owns vs the `totalLiquidity`.

The `withdraw()` function lets a user take both ETH and tokens out at the correct ratio. The actual amount of ETH and tokens a liquidity provider withdraws will be higher than what they deposited because of the 0.3% fees collected from each trade. This incentivizes third parties to provide liquidity.

Compile and deploy your contracts to the frontend:

```
yarn run deploy
```

## 📲 Interface <a href="ada2" id="ada2"></a>

The UX is pretty bad/ugly and it’s still kind of hard to visualize this whole slippage thing. Let’s do some frontend work to clean up the interface and make it easier to understand.

Let’s edit `App.js` in `packages/react-app/src`:

There is a custom `<DEX>` component included in this code branch. Delete the generic `<Contract>` component for the `DEX` and bring in the `<DEX>` like:

```
<DEX  address={address}  injectedProvider={injectedProvider}  localProvider={localProvider}  mainnetProvider={mainnetProvider}  readContracts={readContracts}  price={price}/>
```

Let’s clean up the Balloon’s `<Contract>` component by giving it a title and choosing to only show the `balanceOf` and `approve()` actions:

```
<Contract  title={"🎈 Balloons"}  name={"Balloons"}  show={["balanceOf","approve"]}  provider={localProvider}  address={address}/>
```

Rad, our frontend is looking 🔥 AF:

![](https://miro.medium.com/max/30/1\*FdVFZuogP5PVH5DcJKu6hg.png?q=20)![](https://miro.medium.com/max/700/1\*FdVFZuogP5PVH5DcJKu6hg.png)

## 🔬Explore <a href="bcd2" id="bcd2"></a>

Now, a user can just enter the amount of ETH or tokens they want to swap and the chart will display how the price is calculated. The user can also visualize how larger swaps result in more slippage and less output asset:

![](https://miro.medium.com/max/700/1\*22dvXI1Y5uhMywl1Ez-NOg.gif)

A user can also deposit and withdraw from the liquidity pool, earning fees:

![](https://miro.medium.com/freeze/max/30/1\*87GGK6926SNFoK2HT-Xl3w.gif?q=20)![](https://miro.medium.com/max/700/1\*87GGK6926SNFoK2HT-Xl3w.gif)

## 🎉 Congratulations! <a href="5ff0" id="5ff0"></a>

We’ve patched together a minimum viable decentralized exchange. We can provide liquidity for anyone to swap assets and liquidity providers will earn fees. It all happens on-chain and can’t be censored or tampered with.

It’s an 🤖 **unstoppable market **⚖️!!!

Hit me up on the Twitter DMs: @austingriffith

Here is our final exchange contract in all its glory:

![](https://miro.medium.com/max/19/1\*1gqv-VIlH6BoSa\_HEG31Aw.png?q=20)![](https://miro.medium.com/max/662/1\*1gqv-VIlH6BoSa\_HEG31Aw.png)
