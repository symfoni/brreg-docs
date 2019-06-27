# SDK

## End user interaction and authentication
As Brønnøysundregistrenes Aksjeeierbok (beta) is a service facilitated by leveraging blockchain technology, the flow of how end users interact with your service changes from the regular client-server way of interacting.

Instead of credentials authenticating the user and giving the user the correct access, end users are expected use a browser with blockchain wallet functionality. This functionality is available in

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

In a regular client-server architechture, the user's browser works as a thin client, where the business logic is running on the server. In an application utalizing blockchain the business logic is run in the user's browser and she connects directly to the backend/blockchain. For this to work you need to use her access keys for every write operation. 

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
}
```

When creating a good UX you want to guide the user. You will need a handful of methods to keep track of whether they have a wallet in their browser, whether they are connected to the right blockchain and so on. Use these functions to create that user experience.

## Platform wide methods

### List all companies on the platform

```javascript
const RegistryOfCapTables = require("@brreg/sdk").RegistryOfCapTables

const RegistryOfCapTablesContract = await RegistryOfCapTables.init(ethereum);
const list = await RegistryOfCapTablesContract.list();

console.log(list);
```

Only already onboarded companies are on the platform. Use this code to list them all. Remember to getting the `ethereum` variable. Read more above titled "Accessing the user's wallet"


## Cap table management

### Include SDK

```javascript
const StockFactory = require("@brreg/sdk").StockFactory;
const Stock = require("@brreg/sdk").Stock;
const RegistryOfCapTablesQue = require("@brreg/sdk").RegistryOfCapTablesQue;
```


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


### setCurrentEntity

```javascript
try {
    const data = await dispatch('getEntityByAddress', { address })
    commit('address', data.address)
    commit('uuid', data.uuid)
    commit('type', data.type)
    commit('name', data.name)
    commit('country', data.country)
    commit('city', data.city)
    commit('postalcode', data.postalcode)
    commit('streetAddress', data.streetAddress)
    commit('exist', EXIST.TRUE)
    return data
} catch (error) {
    console.log("Could not find any entity for you so please create one")
    commit('exist', EXIST.FALSE)
}
```

TODO


### create

```javascript
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

Input person's Norwegian sosial security number (Personnummer) for the `uuid` and all of her transactions are returned.


### generateAddress

```javascript
const entityRegistry = await EntityRegistry.init(ethereum);
const address = await entityRegistry.generateAddress();
console.log(address);
```

TODO

