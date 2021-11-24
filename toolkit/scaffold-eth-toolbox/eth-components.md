# 🏺 Eth-components

## Components & Helpers

[useEthersProvider](https://github.com/scaffold-eth/eth-components#useEthersProvider) ⇒

A wrapper around useWeb3React that we can extend as required

[renderTestHook](https://github.com/scaffold-eth/eth-components#renderTestHook) ⇒

Created a test hook with a Web3Wrapper

[Account](https://github.com/scaffold-eth/eth-components#Account) ⇒

Displays an Address, Balance, and Wallet as one Account component, also allows users to log in to existing accounts and log out

```
~ Features ~
```

* Provide address={address} and get balance corresponding to the given address
* Provide localProvider={localProvider} to access balance on local network
* Provide userProvider={userProvider} to display a wallet
*   Provide mainnetProvider={mainnetProvider} and your address will be replaced by ENS name

    ```
          (ex. "0xa870" => "user.eth")
    ```
* Provide price={price} of ether and get your balance converted to dollars
*   Provide web3Modal={web3Modal}, loadWeb3Modal={loadWeb3Modal}, logoutOfWeb3Modal={logoutOfWeb3Modal}

    ```
          to be able to log in/log out to/from existing accounts
    ```
*   Provide blockExplorer={blockExplorer}, click on address and get the link

    ```
          (ex. by default "https://etherscan.io/" or for xdai "https://blockscout.com/poa/xdai/")
    ```

[Address](https://github.com/scaffold-eth/eth-components#Address) ⇒

Displays an address with a blockie image and option to copy address

\~ Features \~

*   Provide ensProvider={mainnetProvider} and your address will be replaced by ENS name

    ```
          (ex. "0xa870" => "user.eth")
    ```
*   Provide blockExplorer={blockExplorer}, click on address and get the link

    ```
          (ex. by default "https://etherscan.io/" or for xdai "https://blockscout.com/poa/xdai/")
    ```
* Provide fontSize={fontSize} to change the size of address text

[AddressInput](https://github.com/scaffold-eth/eth-components#AddressInput) ⇒

Displays an address input with QR scan option \~ Features \~

*   Provide ensProvider={mainnetProvider} and your address will be replaced by ENS name

    ```
          (ex. "0xa870" => "user.eth") or you can enter directly ENS name instead of address
    ```
* Provide placeholder="Enter address" value for the input
* Value of the address input is stored in value={toAddress}
*   Control input change by onChange={setToAddress}

    ```
                      or onChange={address => { setToAddress(address);}}
    ```

[Balance](https://github.com/scaffold-eth/eth-components#Balance) ⇒

Displays a balance of given address in ether & dollar

\~ Features \~

* Provide address={address} and get balance corresponding to given address
* Provide provider={mainnetProvider} to access balance on mainnet or any other network (ex. localProvider)
* Provide price={price} of ether and get your balance converted to dollars

[Blockie](https://github.com/scaffold-eth/eth-components#Blockie) ⇒

Show a blockie (bar code profile icon) component for an public address

[EtherInput](https://github.com/scaffold-eth/eth-components#EtherInput) ⇒

Displays input field for ETH/USD amount, with an option to convert between ETH and USD \~ Features \~

* Provide price={price} of ether and easily convert between USD and ETH
* Provide value={value} to specify initial amount of ether
* Provide placeholder="Enter amount" value for the input
* Control input change by onChange={value => { setAmount(value);}}

[Faucet](https://github.com/scaffold-eth/eth-components#Faucet) ⇒

Displays a local faucet to send ETH to given address, also wallet is provided

\~ Features \~

* Provide price={price} of ether and convert between USD and ETH in a wallet
* Provide localProvider={localProvider} to be able to send ETH to given address
*   Provide ensProvider={mainnetProvider} and your address will be replaced by ENS name

    ```
          (ex. "0xa870" => "user.eth") or you can enter directly ENS name instead of address
          works both in input field & wallet
    ```
* Provide placeholder="Send local faucet" value for the input

[GasGauge](https://github.com/scaffold-eth/eth-components#GasGauge) ⇒

Displays gas gauge

\~ Features \~

* Provide gasPrice={gasPrice} and get current gas gauge

NetworkDisplay =>



[PunkBlockie](https://github.com/scaffold-eth/eth-components#PunkBlockie) ⇒

Show a punk blockie (crypto punk profile icon) component for an public address

[Wallet](https://github.com/scaffold-eth/eth-components#Wallet) ⇒

Displays a wallet where you can specify address and send USD/ETH, with options to scan address, to convert between USD and ETH, to see and generate private keys, to send, receive and extract the burner wallet \~ Features \~

* Provide provider={userProvider} to display a wallet
*   Provide address={address} if you want to specify address, otherwise

    ```
                                                your default address will be used
    ```
*   Provide ensProvider={mainnetProvider} and your address will be replaced by ENS name

    ```
          (ex. "0xa870" => "user.eth") or you can enter directly ENS name instead of address
    ```
* Provide price={price} of ether and easily convert between USD and ETH
* Provide color to specify the color of wallet icon

[transactor](https://github.com/scaffold-eth/eth-components#transactor) ⇒

this should probably just be renamed to "notifier" it is basically just a wrapper around BlockNative's wonderful Notify.js [https://docs.blocknative.com/notify](https://docs.blocknative.com/notify)

### useEthersProvider ⇒

A wrapper around useWeb3React that we can extend as required

**Kind**: global constant\
**Returns**: TEthersManager\


### renderTestHook ⇒

Created a test hook with a Web3Wrapper

**Kind**: global constant\
**Returns**: (TTestHookResult)\
**See**: renderHook from @link testing-library/react-hooks

| Param    | Description           |
| -------- | --------------------- |
| callback | callback to init hook |

### Account ⇒

Displays an Address, Balance, and Wallet as one Account component, also allows users to log in to existing accounts and log out

```
~ Features ~
```

* Provide address={address} and get balance corresponding to the given address
* Provide localProvider={localProvider} to access balance on local network
* Provide userProvider={userProvider} to display a wallet
* Provide mainnetProvider={mainnetProvider} and your address will be replaced by ENS name (ex. "0xa870" => "user.eth")
* Provide price={price} of ether and get your balance converted to dollars
* Provide web3Modal={web3Modal}, loadWeb3Modal={loadWeb3Modal}, logoutOfWeb3Modal={logoutOfWeb3Modal} to be able to log in/log out to/from existing accounts
* Provide blockExplorer={blockExplorer}, click on address and get the link (ex. by default "[https://etherscan.io/](https://etherscan.io)" or for xdai "[https://blockscout.com/poa/xdai/](https://blockscout.com/poa/xdai/)")

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### Address ⇒

Displays an address with a blockie image and option to copy address

\~ Features \~

* Provide ensProvider={mainnetProvider} and your address will be replaced by ENS name (ex. "0xa870" => "user.eth")
* Provide blockExplorer={blockExplorer}, click on address and get the link (ex. by default "[https://etherscan.io/](https://etherscan.io)" or for xdai "[https://blockscout.com/poa/xdai/](https://blockscout.com/poa/xdai/)")
* Provide fontSize={fontSize} to change the size of address text

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### AddressInput ⇒

Displays an address input with QR scan option \~ Features \~

* Provide ensProvider={mainnetProvider} and your address will be replaced by ENS name (ex. "0xa870" => "user.eth") or you can enter directly ENS name instead of address
* Provide placeholder="Enter address" value for the input
* Value of the address input is stored in value={toAddress}
* Control input change by onChange={setToAddress} or onChange={address => { setToAddress(address);}}

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### Balance ⇒

Displays a balance of given address in ether & dollar

\~ Features \~

* Provide address={address} and get balance corresponding to given address
* Provide provider={mainnetProvider} to access balance on mainnet or any other network (ex. localProvider)
* Provide price={price} of ether and get your balance converted to dollars

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### Blockie ⇒

Show a blockie (bar code profile icon) component for an public address

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### EtherInput ⇒

Displays input field for ETH/USD amount, with an option to convert between ETH and USD \~ Features \~

* Provide price={price} of ether and easily convert between USD and ETH
* Provide value={value} to specify initial amount of ether
* Provide placeholder="Enter amount" value for the input
* Control input change by onChange={value => { setAmount(value);}}

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### Faucet ⇒

Displays a local faucet to send ETH to given address, also wallet is provided

\~ Features \~

* Provide price={price} of ether and convert between USD and ETH in a wallet
* Provide localProvider={localProvider} to be able to send ETH to given address
* Provide ensProvider={mainnetProvider} and your address will be replaced by ENS name (ex. "0xa870" => "user.eth") or you can enter directly ENS name instead of address works both in input field & wallet
* Provide placeholder="Send local faucet" value for the input

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### GasGauge ⇒

Displays gas gauge

\~ Features \~

* Provide gasPrice={gasPrice} and get current gas gauge

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### PunkBlockie ⇒

Show a punk blockie (crypto punk profile icon) component for an public address

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### Wallet ⇒

Displays a wallet where you can specify address and send USD/ETH, with options to scan address, to convert between USD and ETH, to see and generate private keys, to send, receive and extract the burner wallet \~ Features \~

* Provide provider={userProvider} to display a wallet
* Provide address={address} if you want to specify address, otherwise your default address will be used
* Provide ensProvider={mainnetProvider} and your address will be replaced by ENS name (ex. "0xa870" => "user.eth") or you can enter directly ENS name instead of address
* Provide price={price} of ether and easily convert between USD and ETH
* Provide color to specify the color of wallet icon

**Kind**: global constant\
**Returns**: (FC)

| Param |
| ----- |
| props |

### transactor ⇒

this should probably just be renamed to "notifier" it is basically just a wrapper around BlockNative's wonderful Notify.js [https://docs.blocknative.com/notify](https://docs.blocknative.com/notify)

**Kind**: global constant\
**Returns**: (transactor) a function to transact which calls a callback method parameter on completion

| Param     |
| --------- |
| provider  |
| gasPrice  |
| etherscan |

