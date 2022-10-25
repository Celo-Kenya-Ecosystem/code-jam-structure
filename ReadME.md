# Code Jam Structure

## ✨Code Jam: Getting Started with Celo✨

## Objectives

- Learn more about Celo
- Be able to explain how Celo is similar to and different from Ethereum
- Send Celo Dollars on the Alfajores Testnet
  - Create an account
  - Connect to the testnet
  - Fund the account
  - Send funds
- Run a Celo Node
- Learn how to make a simple web page that connects to Celo
- Learn how to make a simple mobile dapp that connects to Celo

## Requirements

- A computer with an internet connection
- Node.js (version 10+) and yarn installed on your computer
- Git installed on your computer
- Familiarity with Javascript and basic web development concepts
- Celo extension wallet (requires a Chrome-based web browser, like Chrome or Brave)

## Modules

### Jam 0: Learn about Celo

To learn more about the background of Celo, the technology stack, and the fundamental protocol, see the Celo Overview page of the Celo documentation. Here are some examples of video tutorials you can use if you prefer:

- [https://www.youtube.com/watch?v=LN7p6mB1t4k] - How to Build a DApp on Celo
- [https://www.youtube.com/watch?v=kO6Wm8pgKXU] - Developing & deploying your first DApp on Celo
- [https://www.youtube.com/watch?v=bp2loYXPhbM&t=16s] - Celo Tech Talks Building a mobile first blockchain platform.

## Jam 1. Sending Transactions

### Step up

1. Clone this GitHub repo: [https://github.com/critesjosh/celo-transactions-lesson]

```sh
 git clone https://github.com/critesjosh/celo-transactions-lesson.git
```

2. Go into the cloned project and install the dependencies

```sh
 cd celo-transactions-lesson && yarn install
```

3. Once the dependencies are installed, create a new file in the project root called .env. Then run

```sh
 node createAccount.js
```

This will print new Celo account details. Copy the private key for your new account into a _PRIVATE_KEY_ variable in .env. It should look something like this

```sh
PRIVATE_KEY="0x7b756cc34cdd08dfc96bea50101fdd62abb8a7ba9c083881dc6f6bd3bda35408"
```

Congratulations! You just created a new account on Celo! This private key controls access to the associated account, so this is highly sensitive data. Anyone with this key can send transactions on behalf of the account. You can see how this account is created in the

```sh
createAccount.js file
```

4. Copy the address that is printed. Fund the account address on the Alfajores test net here: [https://celo.org/developers/faucet]

5. Create an account on Figment Data Hub [https://figment.io/datahub/celo/] and get your API key and add it to the FIGMENT_API_KEY in .env. This will allow you to connect to the Celo networks. Your .env file should now look something like this.

6. Now you are ready to go through lesson.js, following the provided details and uncommenting the function calls to run the associated code.

#### Lesson.js

The lesson.js file contains example code with commentary on how to create transactions on the Celo network using a variety of tools. It starts by creating simple transactions manually, so you can see what is involved, then goes over how ContractKit and Celo Ethers.js do the same thing, but make it easier for you as a developer. ContractKit uses web3.js under the hood, so you will see many references to web3.js when using ContractKit.

As you go through the sections of the file, some of them will have functions that show you how to create transactions and send them to the network. To run the function, uncomment the function call and then run the script by entering node lesson.js in the terminal from the project root directory. The functions will print output to the terminal so you can see what is going on.
Once you are done running that function, comment it out again with two slashes (//).

## Jam 2. Run a Celo Node

Running a node helps support the core infrastructure of a blockchain network. Go through this page of the Celo Docs that shows you how to run a full node. In the near future, Celo will support incentives for running full nodes to help maintain a robust network that can serve millions of mobile users.

#### Sending transactions

Try sending transactions through your local node, rather than using the remote node. You can find some more info about running an "ultralight" node that will sync in seconds on this page (so you don't have to wait for the full node to sync).

#### Connect with CeloCLI

Celo has a command line interface that makes it easy for relatively technical users to read and write to the Celo blockchain without having to rely on a web interface.

- Once you have a node up and running, install celocli via npm. Instructions here.
- Connect celocli to your locally running node.
- Try looking up the token price of cUSD from the price of oracle contracts.
- Try transferring some CELO from your node account.
- You can find more info about the Celo CLI commands on the docs page here. Scroll down the page tree on the left to see the page list.

## Jam  3.  Build a Desktop Webpage

For this section, you will be building off of the repo that we started working on earlier.

You can paste the private key from your .env file into the Celo Extension Wallet to import your funded Alfajores testnet account into the browser extension.

1. Start in the celo-transactions-lesson project root. Move into the webpage directory.
  
  ```sh  
  cd webpage && yarn install 
  ```

 2. Install the Celo Extension Wallet from the chrome web store [https://chrome.google.com/webstore/detail/celoextensionwallet/kkilomkmpmkbdnfelcpgckmpcaemjcdh]. Once it is installed, select the "Alfajores Test Network" from the "Networks" dropdown.

   ```sh
   { meta mask wallet or celo extension } 
   ```

3. Run yarn dev to start watchify and the lite-server to serve the page at localhost:3000. Watchify will watch for any updates to index.js and automatically bundle the new file for the browser.

4. Review the code in index.js.

 There are 3 basic functions that make up this dapp.

 1. connectCeloWallet

 This function sets you up to send transactions on the connected network by doing a few things.

- Connects to the Celo Extension wallet (with window.celo.enable())
- Sets up an instance of ContractKit with

     ```sh
      const web3 = new Web3(window.celo)
      kit = ContractKit.newKitFromWeb3(web3)
    ```

- Sets the default account for contract kit

     ```sh
      const accounts = await kit.web3.eth.getAccounts()
      kit.defaultAccount = accounts[0]
      ```

- Initialized the cUSD token contract

  ```sh
   cUSDcontract = new kit.web3.eth.Contract(erc20Abi, cUSDContractAddress)
   ```

- Get and display account balance by calling getBalance()

2. send
 This function sends a hardcoded amount of cUSD to a hardcoded address (source), using the cUSDcontract object that was set up in connectCeloWallet.

 The methods available on the cUSDcontract are defined by the contract ABI that is imported at the top of the file.

 Try updating the code so that a user can specify how much cUSD and to which address to send.

 After the transaction is sent, the function reads the balance again and displays the transaction hash to the user.

3. getBalance

This function uses the instance of contractkit initialized in connectCeloWallet to get the account balance.

 const totalBalance = await kit.getTotalBalance(kit.defaultAccount)
getTotalBalance returns more balances than just the cUSD balance (CELO), so you need to get the cUSD balance and shift it by the appropriate number of decimal points. cUSD has 18 decimal points. You can read more about why [https://docs.openzeppelin.com/contracts/4.x/erc20#a-note-on-decimals]


## Jam 4: Building Mobile Applications
There is a Celo truffle box for getting started with building mobile applications using React Native. You can find the Truffle box and instructions for getting started [https://github.com/critesjosh/celo-dappkit].
Download the truffle box and start running the application. The repo assumes you have expo and a Celo testnet wallet. You can get the Celo testnet wallets [https://celo.org/developers/wallet].

## Jam 5: Learn more about Smart Contracts

To learn more about developing smart contracts, you can take up the first 3 courses in the awesome Crypto Zombies course.
[#1 Solidity Tutorial & Ethereum Blockchain Programming Course | CryptoZombies] [https://cryptozombies.io/].
Remember that Celo is running the Ethereum Virtual Machine (EVM), so any tools that you may use for writing smart contracts for Ethereum will work for Celo as well.

## Jam 6: Deploy contracts via your local node

Go through this page of the docs that cover how to deploy a Solidity smart contract from a local node connected to the Alfajores testnet.

## Plugins

Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantaneously see your updates!

Open your favorite Terminal and run these commands.

First Tab:

```sh
node app
```

Second Tab:

```sh
gulp watch
```

(optional) Third:

```sh
karma test
```

#### Building for source

For production release:

```sh
gulp build --prod
```

Generating pre-built zip archives for distribution:

```sh
gulp build dist --prod
```

## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
