# Introduction
Welcome to the Brønnøysund Register Center's cap table Developer Portal (beta).
Norwegian limited companies must have a share capital of at least NOK 30,000 distributed among one or more shares, all of which have the same nominal value in NOK. The size of the share capital, the number of shares and the nominal value are determined in the company's articles of association when the company is formed.
All limited companies shall have a cap table unless the company's shares are registered in the public security register. The cap table shall contain an overview of who is shareholders at all times, and it will normally be decisive for who can exercise shareholder rights such as voting rights at the general meeting and the right to dividend. The cap table is public - so everyone has the right to see it.

## What is a cap table
When a shareholder is entered in the shareholder's register the company shall notify the shareholder thereof. The share register shall be updated when a change of ownership or pledging of shares happens, in accordance with established rules in the Companies Act (§ 4-7).
Shares can be freely sold or given away without payment unless otherwise stated by law, articles of association or agreement between the shareholders. For sale, the price is normally calculated on the basis of market value. Sales below market value can also occur, called a gift sale. In the same way as when shares are given away, this could trigger a tax liability.
When shareholders sell or otherwise realize shares, gains will be taxable and losses deductible.
The Companies Act contains rules on the consent of acquiring shares, and rules on pre-emption rights for the other shareholders. An agreement on the transfer of shares shall be reported to the board of the limited company by the person taking over the shares. The agreement should at a minimum contain who the agreement applies to, how many shares are transferred, and at what price.
Transfers made in the Brønnøysund Register's shareholder book have been reported immediately. The new shareholder must be notified by the company that she has been included in the shareholder's register and what is listed.

<aside class = "success">This this platform is live, the company does not need to keep its own cap table nor report its details to the government, as everything is automated.</aside>

<aside class = "success">
The actual transfer of shares is not necessary to report to the cap table when using the Brønnøysund Register's Shareholder Book, as it is automatically reported.
</aside>

### Agreements between the company and the company's management, shareholders or related parties
The company and the shareholders of the company can enter into agreements with each other, but there are then stricter requirements for the procedure. The starting point is that any agreement that has a value more than one-tenth of the share capital, must be approved in the general assembly. From this point of view, some exceptions are listed in the Companies Act. The rules also apply to shareholders' close associates, such as close relatives.

### Shareholder agreements
Shareholder agreements are normally entered into between shareholders of a company and regulates the relationship between them. The shareholders are not obliged to enter into such an agreement, but it may be useful. The shareholder agreement obliges the shareholders who sign the agreement. There are no requirements as to how the agreement should look or what it should contain. Examples of conditions that can be regulated in a shareholder agreement are special rules relating to ownership, demands for dividends, non-compete clauses, impartiality and requirements for work effort.

### Conflict between shareholders
It is not uncommon for conflicts between shareholders to arise regarding the organization and running of a company. What the basis of the conflicts is difficult to say beforehand, but it may make sense to have a conscious relationship with this. It may make sense to
* Avoid being two owners who own 50% each of the shares, because this makes majority decisions difficult
* Enter into shareholder agreements that clarify how the relationship between shareholders should be in the event of disagreement.
In cases where the shareholders no longer manage to cooperate with each other, the district court may, by a lawsuit from a shareholder or from the company, decide on the redemption or release of a shareholder's shares. Such lawsuits must be regarded as last resort, and there must be weighty reasons.

## Definitions
- Cap table: shareholder book for a company (“aksjeeierbok”)
- Registry of cap tables: registry of all cap tables on the platform
- Entity registry: information about people and companies ("Enhetsregisteret")
- (Board) Director: Chairman. The legal entity responsible for the cap table
- Share class is called partition in the SDK
- Block explorer: service for a view into what’s happening on the blockchain. Link in menu to the left

## Functions in the Brønnøysund Register's Shareholders' Registry
As a service provider, one can either use the share register SDK (Javascript) to make read / writes against cap tables, or one can extend the register of data and functionality by writing smart contracts in Solidity and uploading to the service block.

Feel free to give feedback by creating an Issue on Github.

## Users

A user is a shareholder and/or CEO and/or chairman of the board. A user is either active or passive.

An active user is authenticated and can write changed directly into the shareholder register, like transferring shares or changing their address.

A passive user is a shareholder who is not registered on the platform. A passive user cannot make changes in the shareholder register, and any transfers have to be input by the chairman of the board, on behalf of the shareholder.

<aside class=“notice”>
All changes in the shareholder register have to be approved by the chairman of the board. In future versions, this approval can be granted automatically if the articles of association and shareholder agreements are automated (i.e. programmed as code).
</aside>

# Development

You can either the platform with the SDK, or you can extend the platform itself by developing and deploying smart contracts.

## Installation of SDK

To install the SDK to your project just use NPM:

`npm i @brreg-sdk`
 

### Example application
It can be hard getting started. We recommend you take a look at our example application to get a feel of the SDK. The application is written in Vue.js.
<a href="https://gitlab.com/blockchangers/kunder/brreg/brreg" target="_blank">https://gitlab.com/blockchangers/kunder/brreg/brreg</a>






# SDK

## End user interaction and authentication
As Brønnøysundregistrenes Aksjeeierbok (beta) is a service facilitated by leveraging blockchain technology, the flow of how end users interact with your service changes from the regular client-server way of interacting.

Instead of credentials authenticating the user and giving the user the correct access, end users are expected to use a browser with blockchain wallet functionality. This functionality is available in

* Google Chrome and Microsoft Edge when installing the [Metamask plugin](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn)
* The Opera web browser

### Accessing the user's wallet
> To access the user's wallet, use this code:

```javascript
let ethereum
if (typeof window.ethereum !== 'undefined' || (typeof window.web3 !== 'undefined')) {
    ethereum = window.ethereum;
}
```

> Append the `ethereum` variable when writing to the blockchain, and the user will be asked to sign the transaction before it is sent

The first line of code includes the SDK. This needs to be installed before you can use it. See "Installation". 

In a regular client-server architecture, the user's browser works as a thin client, where the business logic is running on the server. In an application utilizing blockchain, the business logic is run in the user's browser and she connects directly to the backend/blockchain. For this to work, you need to use her access keys for every write operation. 

<aside class="warning">
This code snippet is essential for using any of the following methods from the SDK.
</aside>


### Checking that the user has a wallet
```javascript
// Check if found wallet. Stop of no
const foundEthereum = (ethereum !== undefined);
if (!foundEthereum) return;

// Since we have metamask, we can now add listeners
ethereum.on('accountsChanged', function (accounts) {
    console.log("accounts changed => ", accounts)
})
ethereum.on('networkChanged', function (network) {
    console.log("network changed => ", network)
})

// Connect to the wallet
if (state.accounts.length < 1) {
  try {
      const accounts = await ethereum.enable();
      console.log(accounts);
      return true;
  } catch (error) {
      // Handle error. Most likely the user rejected the login:
      console.log("Metamask reject connect error: ", error);
      return false;
  
}
```

When creating a good UX you want to guide the user. You will need a handful of methods to keep track of whether they have a wallet in their browser, whether they are connected to the right blockchain and so on. Use these functions to create that user experience.

## Platform wide methods (RegistryOfCapTables)

init(externalSignerProvider: Signer | any, proxyAddress?: string)
list()

### List all companies on the platform

```javascript
const RegistryOfCapTables = require("@brreg/sdk").RegistryOfCapTables

const RegistryOfCapTablesContract = await RegistryOfCapTables.init(ethereum);
const list = await RegistryOfCapTablesContract.list();

console.log(list);
```

Only already onboarded companies are on the platform. Use this code to list them all. Remember to getting the `ethereum` variable. Read more above titled "Accessing the user's wallet"

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



## Regular flows

Here is a list of some common solutions for covering often used user flows.

### Onboard a new company

```javascript
const EntityRegistry = require("@brreg/sdk").EntityRegistry

// TODO
```

An important distinction is that a company can exist while not being on this platform. If a chairman wants to onboard her company, it is your responsibility as the application developer to complete this. Note that only the chairman of the company is allowed to onboard the company. 

This platform is empty from the start. The Brønnøysund Register Centre will not offer any application or service for chairmen to adopt this cap table service. It is all done by third parties delivering services to the public, like yourself. This means that all the data needed to get the cap table onto the platform is your responsibility to get and populate with. This can either be something you have already, something you get from other Brønnøysund Register Center APIs or just asking the user. 

<aside class=”notice”>You are responsible for validating that the user is the chairman of the company. This will be done by the platform in later version.</a>

### Onboard a new person

TODO

### Show cap table

TODO





# Extending the registry with smart contracts

TODO


