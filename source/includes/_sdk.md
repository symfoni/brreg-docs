# SDK

You can either the platform with the SDK, or you can extend the platform itself by developing and deploying smart contracts. This section is details how to use the SDK.

## Getting started

> To install the SDK to your project just use NPM in your project.

```
npm install @brreg-sdk
```

To develop on BrregCP, you’re first going to want to get the SDK installed on your development machine. 

You should also install MetaMask in Chrome as the middleware between your application the blockchain. [Download here](https://metamask.io/).

### Example application
It can be hard getting started. We recommend you <a href="https://gitlab.com/blockchangers/brreg/tree/master/packages/forvalter" target="_blank">take a look at the source code of our example application</a> to get a feel of the SDK. The application is written in Vue.js. A <a href="https://blockchangers.gitlab.io/brreg/" target="_blanK">live version of the example application is available on Github</a>.

## Basic Considerations

As BrregCP is a service facilitated by leveraging blockchain technology, the flow of how end users interact with your service changes from the regular client-server way of interacting.

Instead of credentials authenticating the user and giving the user the correct access, end users are expected to use a browser with blockchain wallet functionality. This functionality is available in

* Google Chrome and Microsoft Edge when installing the [Metamask plugin](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn)
* The Opera web browser

### Web3 Browser Detection

The first thing your app will want to do is verify whether the user is using MetaMask or not, which is simple using a check like `if (typeof window.ethereum !== 'undefined') { /* deal with it */ }`.

### Connecting to the BrregCP Network

In the top right menu of MetaMask, you can select the network that you are currently connected to. Among several popular defaults, you'll find `Custom RPC`. Use it and set

* Network Name to `Toyen` and
* New RPC URL to `http://ethjygmk4-dns-reg1.northeurope.cloudapp.azure.com:8540`

![How to setup Metamask with the Toyen network](../images/toyenInMetamask.png "How to setup Metamask with the Toyen network")

Since your seed phrase is the power to control all your accounts, it is probably worth keeping at least one seed phrase for development, separate from any that you use for storing real value. One easy way to manage multiple seed phrases with MetaMask is with multiple browser profiles, each of which can have its own clean extension installations.

<aside class="note">Note that users of you application will also have to manually connect Metamask to the Toyen network as long as BrregCP is in active development and in beta.</aside>

### User State

Currently there are a few stateful things you want to consider when interacting with Metamask:

```javascript
ethereum.networkVersion
ethereum.selectedAddress
```

> Both of these are available synchronously. The networkVersion for BrregCP is `53387025`.

- What is the current network?
- What is the current account?

<aside class="note">If the networkVersion is not `53387025`, the user is not connected to the BrregCP. Guide the user to correcting this. See the "Connecting to the BrregCP Network" chapter above.</aside>

### Logging In

> When you're ready to request the user logs in, you can call this simple method.

```javascript
ethereum.enable();
```

> Since it returns a promise, if you're in an `async` function, you may log in like this.

```javascript
const accounts = await ethereum.enable()
const account = accounts[0] // We currently only ever provide a single account,
                            // but the array gives us some room to grow.
```

This promise-returning function resolves with an array of hex-prefixed ethereum addresses, which can be used as general account references when sending transactions.

Over time, this method is intended to grow to include various additional parameters to help your site request all the setup it needs from the user during setup.

## Accessing the user's wallet
> To access the user's wallet, use this code:

```javascript
let ethereum
if (typeof window.ethereum !== 'undefined' || (typeof window.web3 !== 'undefined')) {
    ethereum = window.ethereum;
}
```

The first line of code includes the SDK. This needs to be installed before you can use it. See [Getting started](#getting-started). 

In a regular client-server architecture, the user's browser works as a thin client, where the business logic is running on the server. In an application utilizing blockchain, the business logic is run in the user's browser and she connects directly to the backend/blockchain. For this to work, you need to use her access keys for every write operation. 

<aside class="warning">
This code snippet is essential for using any of the following methods from the SDK.
</aside>

MetaMask injects a global API into websites visited by its users at `window.ethereum` (Also available at `window.web3.currentProvider` for legacy reasons). This API allows websites to request user login, load data from blockchains the user has a connection to, and suggest the user sign messages and transactions. You can use this API to detect the user of a web3 browser.

If you want to deep dive into the Metmask API and their best practieces, check our the [Metamask documentation](https://metamask.github.io/metamask-docs/API_Reference/Ethereum_Provider).

## Registry Of Cap Tables

While most functions are spesific to a given company, the functions in this chapter are platform wide.

### init(externalSignerProvider: Signer | any, proxyAddress?: string);

> The Class always has to be initalized before using

```javascript
init(ethereum);
```

Parameter | Default | Description
--------- | ------- | -----------
externalSignerProvider|undefined|Should be set to the user's wallet i.e. `ethereum` from the section [Accessing the user's wallet](#accessing-the-user-39-s-wallet) from above.
proxyAddress|undefined|optional. If you want to point the SDK at another blockchain than the [Stagning server](#networks-and-endpoints)

### list()

```javascript
const RegistryOfCapTables = require("@brreg/sdk").RegistryOfCapTables
const RegistryOfCapTablesContract = await RegistryOfCapTables.init(ethereum);
const list = await RegistryOfCapTablesContract.list();
console.log(list);
```

List all companies on the platform

Only already onboarded companies are on the platform. Use this code to list them all. Remember to getting the `ethereum` variable. See [Accessing the user's wallet](#accessing-the-user-39-s-wallet)

## Onboard new company (StockFactory)

init(signer, [proxy])
createNew(name: string, uuid: string, options: { partitions: string[], symbol: string } = { partitions: [DEFAULT_PARTITION], symbol: "" })

## Cap table management (Stock)

### Include SDK

```javascript
const StockFactory = require("@brreg/sdk").StockFactory;
const Stock = require("@brreg/sdk").Stock;
const RegistryOfCapTablesQue = require("@brreg/sdk").RegistryOfCapTablesQue;
```

First you need the address of the company in question. Then you can do all of these 
Read:
init(account, address, [proxy])
info()
transactions([filter])
shareholders()
getDefaultPartitions([asBytes])
balanceOf(address)
balanceOfByPartition(partition, address)
partitionsOf(address, [asBytes])
name() 
uuid()
totalSupply()
getTotalSupplyByPartition(partition)
denominationPerShare()
isController(address)
director()
getAddress()



Write:
setDenomination(number)
transferDirector(address)
issue(to fnr, number shares, [options: {data:, partition}])
transfer(to fnr, number shares, [options: {data:, partition}])
redeem(number of shares, [options: {data:, partition}])








### createNew

```javascript
const stockFactory = await StockFactory.init(ethereum);
stockFactory.createNew(name, uuid);
```

TODO


### capTable

```javascript
let companyCapTable = await Stock.init(ethereum, id);
console.log(companyCapTable);
```

Input the Norwegian organization number for the `id` and get the full cap table in return.


### getInfo

```javascript
const capTable = await Stock.init(ethereum, id);
let info = capTable.info();
console.log(info);
```

Input the Norwegian organization number for the `id` and get the full cap table in return.


### getShareholders

```javascript
const capTable = await Stock.init(ethereum, id);
const shareholders = await capTable.transactionsByShareHolder();
console.log(shareholders);
```

Input the Norwegian organization number for the `id` and get the full cap table in return.


## Interacting with the Entity Registry

### Include SDK

```javascript
const EntityRegistry = require("@brreg/sdk").EntityRegistry
```


TODO generateAddress() for putting shares not where no user exists

init(externalSignerProvider: Signer | any, proxyAddress?: string)
allTransactionsAllCapTables(uuid: string)
getEntityByUuid(uuid: string)
getEntityByAddress(address: string)
addEntity(data: EntityData)
updateEntity(data: EntityData)


### create

```javascript
const accounts = await ethereum.enable();
     let stockFactory = await StockFactory.init(ethereum);
     stockFactory.createNew("Blockchangers AS", "915772137")
// TODO Note that it will have to be acceptet by brreg. in que

const entityRegistry = await EntityRegistry.init(ethereum)
const res = await entityRegistry.addEntity({
    address: data.address,
    uuid: data.uuid,
    type: data.type,
    name: data.name,
    country: data.country,
    city: data.city,
    postalcode: data.postalcode,
    streetAddress: data.streetAddress
})
await dispatch('setCurrentEntity', { address: data.address })
```

TODO

TODO 2: disse kode eksemplene er feil


### getEntityByUuid

```javascript
const entityRegistry = await EntityRegistry.init(ethereum);
const data = await entityRegistry.getEntityByUuid(uuid);
console.log(data);
```

TODO


### getEntityByAddress

```javascript
const entityRegistry = await EntityRegistry.init(ethereum);
const data = await entityRegistry.getEntityByAddress(address);
console.log(data);
```

TODO


### getTransactions

```javascript
const entityRegistry = await EntityRegistry.init(ethereum);
const data = await entityRegistry.allTransactionsAllCapTables(uuid);
console.log(data);
```

Input person's Norwegian social security number (personnummer) for the `uuid` and all of her transactions are returned.


### generateAddress

```javascript
const entityRegistry = await EntityRegistry.init(ethereum);
const address = await entityRegistry.generateAddress();
console.log(address);
```

TODO

