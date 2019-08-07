## Registry Of Cap Tables Que API

Note that while anyone can add any company with the Stock Factory API, only validated companies are displayed to users and other developers. You get the company validated by adding it to this validation queue. 

### init(externalSignerProvider: Signer | any, proxyAddress?: string)

> The Class always has to be initalized before using

```javascript
const RegistryOfCapTablesQue = require("@brreg/sdk").RegistryOfCapTablesQue
const RegistryOfCapTablesQueContract = await RegistryOfCapTablesQue.init(ethereum);
```

Parameter | Default | Description
--------- | ------- | -----------
externalSignerProvider|undefined|Should be set to the user's wallet i.e. `ethereum` from the section [Accessing the user's wallet](#accessing-the-user-39-s-wallet) from above.
proxyAddress|optional|If you want to point the SDK at another blockchain than the [Stagning server](#networks-and-endpoints)

### addQue(address: string)

Add company to the queue.

### isQued(address: string)

Returns true of the given company is in the queue.

### queNumber(address: string)

Returns the number in the queue for the given company.

### que()

Returns the complete queue.














## Stock API
Used fo cap table management 

### Include SDK

```javascript
const StockFactory = require("@brreg/sdk").StockFactory;
const Stock = require("@brreg/sdk").Stock;
const RegistryOfCapTablesQue = require("@brreg/sdk").RegistryOfCapTablesQue;
```

First you need the address of the company in question. 


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









## Get information about company
> To get metadata of a company, use this code:

```javascript
const ctReg = require('ctReg');

let company = ctReg.getCompany(NO123456789);
```

```javascript
{
  name: "COMPANY AS",
  address: "M\u00f8llergata 6",
  postNumber: "0179",
  municipality: "OSLO",
  country: "NO",
  siteLink: "www.blockchangers.com",
  isVerified: true
}
```

> Make sure to replace `NO123456789` with the company you are requesting data for.

This command returns a object with information about the given company from the Enteties Registry.

<aside class="notice">
This method should also used to check if a company is onboarded to the platform. 
</aside>

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
org_number |   | The unique identifier for the company in for format COUNTRYCODE + UUID i.e. `NO123456789`

### Return values

Parameter | Description
--------- | -----------
name | The name of the company
Address | The postal address of the company
postNumber | Continuing the postal address with postal number
municipality | Continuing the postal address with the address' municipality
country |  Continuing the postal address with the address' country
siteLink | URL for the company website
isVerified | Anyone can claim a company, but it is only a verified company by Brønnøysundregistrene if this value is true
error_msg | Descriptive error if the query was unsuccessful

<aside class="warning">
You should only display companies where `isVerified` is `true` to the end-user.
</aside>


## Get company cap table
> To get the cap table of a company, use this code:

```javascript
const ctReg = require('ctReg');

// Returns current cap table
let captable = ctReg.getCapTable("NO123456789");

// TODO Returns cap table at the given time
//let captable = ctReg.getCapTable(NO123456789, 1560437308);
```

```javascript
{
  shareholders: [
    {
      name: "Kari Nordmann",
      dob_orgnum: "240786",
      address: "Borettsgata 3, 0187 Oslo",
      roles: ["Shareholder", "Chairman"],
      uuid: "0x123456789abcdef"
      sharesAmount: [
        {class: "Klasse A", num: 1000},
        {class: "Klasse B", num: 500}
      ]
    },
    {
      name: "Karianne Nordmann",
      dob_orgnum: "240760",
      address: "Nistuguvegen 207, 2860 Hov",
      roles: ["Shareholder"],
      uuid: "0xabcdef123456789"
      sharesAmount: [
        {class: "Klasse A", num: 0},
        {class: "Klasse B", num: 500}
      ]
    },
  ]
}
```

> Make sure to replace `NO123456789` with the company you are requesting data for.

This command returns an object with a list of shareholders and holdings in the given company.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
org_number |   | The unique identifier for the company in for format COUNTRYCODE + UUID i.e. `NO123456789`

### Return values

Parameter | Description
--------- | -----------
name | The name of the company or person (Entity)
dob_orgnum | For a person, the date of birth, or the organization number if the Entity is a company
address | The postal address of the Entity
roles | The roles the Entity has with the company
uuid | The Entity's identifier which should be used for referencing this Entity
sharesAmount | List of share classes and the amount of shares the Entity holds for each class
error_msg | Descriptive error if the query was unsuccessful

<aside class="warning">
You should only display cap tables where `isVerified` from `getCompany` is `true` to the end-user.
</aside>



## Onboarging a new company to the platform

```javascript
const ctReg = require('ctReg');

let obj = {
name: "COMPANY AS",
address: "M\u00f8llergata 6",
postNumber: "0179",
municipality: "OSLO",
country: "NO",
org_number: 123456789,
siteLink: "www.blockchangers.com",
shareholders: [
    {
      name: "Kari Nordmann",
      dob_orgnum: "240786",
      address: "Borettsgata 3, 0187 Oslo",
      roles: ["Shareholder", "Chairman"],
      uuid: "0x123456789abcdef"
      sharesAmount: [
        {class: "Klasse A", num: 1000},
        {class: "Klasse B", num: 500}
      ]
    },
    {
      name: "Karianne Nordmann",
      dob_orgnum: "240760",
      address: "Nistuguvegen 207, 2860 Hov",
      roles: ["Shareholder"],
      uuid: "0xabcdef123456789"
      sharesAmount: [
        {class: "Klasse A", num: 0},
        {class: "Klasse B", num: 500}
      ]
    },
  ]
}
let success = ctReg.onboardCompany(obj);
```

The first time 

<aside class="notice">
This method is not for founding a new company. It is only for onboarding already founded companies to the platform.
</aside>

<aside class="notice">
This method will overwrite earlier executions of `onboardCompany` for the given company, if it is unverified by the Brønnøysundregistrene. If it is verified, it `onboardCompany` can not be run again for the company.
</aside>

<aside class="warning">
Method should only be allowed to run by the company's Chairman.
</aside>

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
ssn |   | The unique identifier for the person e.g. Norwegian "Fødselsnummer" or Dnumber

### Return values

Parameter | Description
--------- | -----------
success | True or false 
error_msg | Descriptive error if 'success' is false

## Send to validation
After onboarding it should be verified







## Get shareholders

```javascript
const ctReg = require('ctReg');

let shareholders = ctReg.getShareholders(orgnur);
```

> The above command returns JSON structured like this:

```json
{
  "company": {
    "orgNumber": "NO915772137",
    "slug": "blockchangers-as",
    "name": "BLOCKCHANGERS AS",
    "address": "M\u00f8llergata 6",
    "postNumber": "0179",
    "city": "OSLO",
    "municipality": "",
    "country": "NO",
    "currency": "NOK",
    "correspondenceAddress": "",
    "correspondencePostNumber": "",
    "correspondenceCity": "",
    "correspondenceMunicipality": "",
    "correspondenceCountry": "NO",
    "siteLink": "www.blockchangers.com",
    "bankAccountNumber": "",
    "bankName": "",
    "bankAddress": "",
    "iban": "",
    "hasMva": false,
    "inactive": false,
    "isVerified": true,
    "documentsGroup": "company-NO915772137-company",
    "documentsBatch": "company-NO915772137",
    "stockOptions": [
      
    ],
    "convertibleLoans": [
      
    ]
  },
  "states": [
    {
      "id": 39998,
      "roles": [
        {
          "roleId": 351196,
          "roles": [
            "Shareholding company"
          ],
          "company": {
            "orgNumber": "NO920142346",
            "name": "FOYN AS",
            "slug": "foyn-as",
            "email": "",
            "address": "",
            "postNumber": "0479",
            "city": "OSLO",
            "country": "NO",
            "currency": "NOK",
            "logo": {
              
            }
          },
          "sharesAmount": {
            "A": 4231,
            "B": 0
          },
          "name": null
        },
        {
          "roleId": 351195,
          "userId": 34160,
          "userFullName": "Oskar Erik \u00c5slund",
          "userEmail": null,
          "userAvatar": {
            
          },
          "roles": [
            "Shareholder"
          ],
          "sharesAmount": {
            "ordinary": 4231
          },
          "name": null
        },
        {
          "roleId": 351194,
          "userId": 57736,
          "userFullName": "Jon Dahl Ramvi",
          "userEmail": "jon@blockchangers.com",
          "userAvatar": {
            
          },
          "roles": [
            "Chairman",
            "CEO",
            "Shareholder"
          ],
          "sharesAmount": {
            "ordinary": 30000
          },
          "name": null
        }
      ],
      "createdAt": "2019-06-12T14:32:56.121719Z",
      "updatedAt": "2019-06-12T14:33:22.018562Z",
      "title": "",
      "date": null,
      "sharesClasses": {
        "ordinary": null
      },
      "status": "step 2"
    },
    {
      "id": 38407,
      "roles": [
        {
          "roleId": 320416,
          "roles": [
            "Shareholding company"
          ],
          "company": {
            "orgNumber": "NO920142346",
            "name": "FOYN AS",
            "slug": "foyn-as",
            "email": "",
            "address": "",
            "postNumber": "0479",
            "city": "OSLO",
            "country": "NO",
            "currency": "NOK",
            "logo": {
              
            }
          },
          "sharesAmount": {
            "ordinary": 4231
          },
          "name": null
        },
        {
          "roleId": 320415,
          "userId": 34160,
          "userFullName": "Oskar Erik \u00c5slund",
          "userEmail": null,
          "userAvatar": {
            
          },
          "roles": [
            "Shareholder"
          ],
          "sharesAmount": {
            "ordinary": 4231
          },
          "name": null
        },
        {
          "roleId": 320414,
          "userId": 57736,
          "userFullName": "Jon Dahl Ramvi",
          "userEmail": "jon@blockchangers.com",
          "userAvatar": {
            
          },
          "roles": [
            "CEO",
            "Shareholder",
            "Chairman"
          ],
          "sharesAmount": {
            "ordinary": 30000
          },
          "name": null
        }
      ],
      "createdAt": "2018-10-31T08:35:03.794055Z",
      "updatedAt": "2018-10-31T08:35:03.794081Z",
      "title": "Last updated 2018-10-31",
      "date": null,
      "sharesClasses": {
        "ordinary": null
      },
      "status": "history"
    }
  ],
  "holdings": [
    
  ],
  "stockOptions": [
    
  ],
  "convertibleLoans": [
    
  ],
  "claims": [
    
  ]
}
```

This method retrieves all shareholders for a given company.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
orgnum |  | The unique identifier for the company called organization number

## Get spesific shareholder ID

```javascript
const ctReg = require('ctReg');

let shareholder = ctReg.getShareholderUUID(ssn);
```

> The above command returns a string witht the user's blockchain universal unique ID:

```javascript
0x1234567890abcdf
```

This method retrieves an ID for a given social security number.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
ssn |   | The unique identifier for the person e.g. Norwegian "Fødselsnummer" or Dnumber


## Onboard company

```javascript
const ctReg = require('ctReg');

const company = {
  name: 'COMPANY AS',
  uuid: '123456789',
  typeOfStock: 'A',
}

const factory = new ethers.ContractFactory(StockQueJSON.abi, StockQueJSON.bytecode, this.DEVELOPER_SIGNER)
const StockQueContractAsDeveloper = await factory.deploy([this.CONTROLLER1])
const address2StockQueContract = StockQueContractAsDeveloper.address
await StockQueContractAsDeveloper.deployed()

const StockFactory = new brregSdk.StockFactory(provider)

StockFactory.setDefaultValues([company.typeOfStock], [this.CONTROLLER1], this.BOARD_DIRECTOR, address2StockQueContract)

const acmeStock = await StockFactory.createNew(company.name, company.symbol, company.uuid, this.BOARD_DIRECTOR_SIGNER)
```

> The above command returns a string witht the user's blockchain universal unique ID:

```javascript
0x1234567890abcdf
```

This method retrieves an ID for a given social security number.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
ssn |   | The unique identifier for the person e.g. Norwegian "Fødselsnummer" or Dnumber
