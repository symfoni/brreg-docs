# SDK

## End user interaction and authentication
As Brønnøysundregistrenes Aksjeeierbok (beta) is a service facilitated by leveraging blockchain technology, the flow of how end users interact with your service changes from the regular client-server way of interacting.

Instead of credentials authenticating the user and giving the user the correct access, end users are expected use a browser with blockchain wallet functionality. This functionality is available in

* The Opera browser
* Google Chrome and Microsoft Edge when installing the [Metamask plugin](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn)

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
let captable = ctReg.getCapTable(NO123456789);

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
