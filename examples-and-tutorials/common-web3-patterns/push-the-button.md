# π² Push The Button - Multi-player Turn Based Game

## Branch Info

**Author: **[Amogh Jahagirdar](https://github.com/0xamogh)****\
**Source code:** [https://github.com/austintgriffith/scaffold-eth/tree/push-the-button-dev](https://github.com/austintgriffith/scaffold-eth/tree/push-the-button-dev)\
**Intended audience:** Beginners/Intermediate\
**Topics:** Scaffold-eth basics, Gaming

## πββοΈ Quick Start

> A base template for multiplayer turn-based game on Ethereum...

```
git clone https://github.com/austintgriffith/scaffold-eth.git push-the-button-dev

cd push-the-button-dev

git checkout push-the-button-dev
```

```
yarn install
```

```
yarn start
```

> in a second terminal window:

```
cd push-the-button-dev
yarn chain
```

> in a third terminal window:

```
cd push-the-button-dev
yarn deploy
```

π± Open [http://localhost:3000](http://localhost:3000) to see the app

What you are seeing right now is the default βpush the button templateβ from `minesweeper.js`

π Open an incognito window and navigate to [http://localhost:3000](http://localhost:3000) (You'll notice it has a new wallet address).

β½οΈ Grab some gas for each account using the faucet:

![image](https://user-images.githubusercontent.com/31567169/110157380-87012b80-7e01-11eb-88a3-4d6652368c87.png)

π Stake the ETH from each account:

![image](https://user-images.githubusercontent.com/31567169/110157434-98e2ce80-7e01-11eb-8b42-b37af72b7766.png)

You'll see the Pool Value, Player Count and the Participants list update

Start a round by pressing Start Game, you'll see something like this ππ½

![image](https://user-images.githubusercontent.com/31567169/110158029-52da3a80-7e02-11eb-9132-8108d5f5998f.png)

The game here on is pretty straightforward

* The goal is to generate the largest number by sheer luck
* The account whose turn it is to play is allowed to click the "Spin the Roulette wheel" button
* Once he clicks the button, a random number is generated via the commit-reveal scheme
* The winning number is updated if this number is the largest yet.
* There is 30 second deadline before he loses his turn
* If he loses his turn, anybody but him can "Skip Turn" for him
* When everyone is done playing, the winner is declared and everyone can withdraw their winnings

π΅π»ββοΈ Inspect the `Debug Contracts` tab to figure out what address is the `owner` of `YourCollectible`?

πΌ Edit your deployment script `deploy.js` in `packages/hardhat/scripts`

π Edit your game variables and working fro, `YourContract.sol` in `packages/hardhat/contracts`

π Edit your frontend `PushTheButton.jsx` in `packages/react-app/src/views`

### π‘ Deploy the game!

π° Ready to deploy to a testnet?

> Change the `defaultNetwork` in `packages/hardhat/hardhat.config.js`

![image](https://user-images.githubusercontent.com/2653167/109538427-4d38c980-7a7d-11eb-878b-b59b6d316014.png)

π Generate a deploy account with `yarn generate`

![image](https://user-images.githubusercontent.com/2653167/109537873-a2c0a680-7a7c-11eb-95de-729dbf3399a3.png)

π View your deployer address using `yarn account` (You'll need to fund this account. Hint: use an [instant wallet](https://instantwallet.io) to fund your account via QR code)

![image](https://user-images.githubusercontent.com/2653167/109537339-ff6f9180-7a7b-11eb-85b0-46cd72311d12.png)

π¨βπ€ Deploy your game:

```
yarn deploy
```

> βοΈ Edit your frontend `App.jsx` in `packages/react-app/src` to change the `targetNetwork` to wherever you deployed your contract:

![image](https://user-images.githubusercontent.com/2653167/109539175-3e9ee200-7a7e-11eb-8d26-3b107a276461.png)

You should see the correct network in the frontend:

![image](https://user-images.githubusercontent.com/2653167/109539305-655d1880-7a7e-11eb-9385-c169645dc2b5.png)

### βοΈ Side Quests

**π Integrate L2 solutions for ETH**

While playing a game, the ETH network often feels slow, integrate a L2 solution like MATIC (this oneβs already done for you, try others)

**π° Redesign the rewards system**

Currently the user gets heavily penalised if he misses a turn, be more kind to your players or they might not come back π’

**πΆ Infura**

> You will need to get a key from [infura.io](https://infura.io) and paste it into `constants.js` in `packages/react-app/src`:

![image](https://user-images.githubusercontent.com/2653167/109541146-b5d57580-7a80-11eb-9f9e-04ea33f5f45a.png)

### π³ Ship the app!

> βοΈ build and upload your frontend and share the url with your friends...

```
# build it:

yarn build

# upload it:

yarn surge

OR

yarn s3

OR

yarn ipfs
```

![image](https://user-images.githubusercontent.com/2653167/109540985-7575f780-7a80-11eb-9ebd-39079cc2eb55.png)

> π©ββ€οΈβπ¨ Share your public url with a friend and invite them for a game!!
