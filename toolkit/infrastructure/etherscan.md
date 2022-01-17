# 🔎 Etherscan

`hardhat-deploy` lets you easily verify contracts on Etherscan, and we have added a helper script to `/packages/hardhat` to let you do that and we have abstracted the actual command away from the user. Please see the packages/hardhat/package.json and look for the 'verify' command, you will see the hardhat command in there (hardhat etherscan-verify --api-key \<your\_key>).

Simply run:

```
cd packages/hardhat
yarn verify --network <network_of_choice>
```

{% hint style="warning" %}
Make sure to change the script so it uses your own Etherscan API key for the `"verify"` command in `packages/hardhat/package.json`&#x20;

"hardhat etherscan-verify --api-key \<your\_key>"
{% endhint %}

And all hardhat's deployed contracts with matching ABIs for that network will be automatically verified.&#x20;



