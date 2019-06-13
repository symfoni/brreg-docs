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
            "ordinary": 4231
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
