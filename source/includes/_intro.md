# Introduction
Welcome to the Brønnøysund Register Center's cap table Developer Portal (beta).
Norwegian limited companies must have a share capital of at least NOK 30,000 distributed among one or more shares, all of which have the same nominal value in NOK. The size of the share capital, the number of shares and the nominal value are determined in the company's articles of association when the company is formed.
All limited companies shall have a cap table, unless the company's shares are registered in the public security register. The cap table shall contain an overview of who is shareholders at all times, and it will normally be decisive for who can exercise shareholder rights such as voting rights at the general meeting and the right to dividend. The cap table is public - so everyone has the right to see it.

## What is a cap table
When a shareholder is entered in the shareholder's register the company shall notify the shareholder thereof. The share register shall be updated by change of ownership or pledging of shares in accordance with established rules in the Companies Act (§ 4-7).
Shares can be freely sold or given away without payment, unless otherwise stated by law, articles of association or agreement between the shareholders. For sale, the price is normally calculated on the basis of market value. Sales below market value can also occur, called a gift sale. In the same way as when shares are given away, this could trigger a tax liability.
When shareholders sell or otherwise realize shares, gains will be taxable and losses deductible.
The Companies Act contains rules on the consent of acquiring shares, and rules on pre-emption rights for the other shareholders. An agreement on the transfer of shares shall be reported to the board of the limited company by the person taking over the shares. The agreement should at a minimum contain who the agreement applies to, how many shares are transferred, and at what price.
Transfers made in the Brønnøysund Register's shareholder book have been reported immediately. The new shareholder must be notified by the company that he / she has been included in the shareholder's register and what is listed.

<aside class = "success"> The company does not need to carry its own cap table. The solution automatically complies with the mtp stock law. dating, accessibility requirements and requirements for storage. </aside>

<aside class = "success">
The actual transfer of shares is not necessary to report to the cap table when using the Brønnøysund Register's Shareholder Book, as it is automatically reported.
</aside>

### Agreements between the company and the company's management, shareholders or related parties
The company and the shareholders of the company can enter into agreements with each other, but there are then stricter requirements for the procedure. The starting point is that any agreement that has a value more than one tenth of the share capital, must be approved in the general assembly. From this point of view, some exceptions are listed in the Companies Act. The rules also apply to shareholders' close associates, such as close relatives.

### Shareholder agreements
Shareholder agreements are normally entered into between shareholders of a company, and regulates the relationship between them. The shareholders are not obliged to enter into such an agreement, but it may be useful. The shareholder agreement obliges the shareholders who sign the agreement. There are no requirements as to how the agreement should look or what it should contain. Examples of conditions that can be regulated in a shareholder agreement are special rules relating to ownership, demands for dividends, non-compete clauses, impartiality and requirements for work effort.

### Conflict between shareholders
It is not uncommon for conflicts between shareholders to arise regarding the organization and running of a company. What the basis of the conflicts is difficult to say beforehand, but it may make sense to have a conscious relationship with this. It may make sense to
* Avoid being two owners who own 50% each of the shares, because this makes majority decisions difficult
* Enter into shareholder agreements that clarifies how the relationship between shareholders should be in the event of disagreement.
In cases where the shareholders no longer manage to cooperate with each other, the district court may, by lawsuit from a shareholder or from the company, decide on the redemption or release of a shareholder's shares. Such lawsuits must be regarded as last resort, and there must be weighty reasons.

## Functions in the Brønnøysund Register's Shareholders' Registry
As a service provider, one can either use the share register SDK (Javascript) to make read / writes against cap tables, or one can extend the register of data and functionality by writing smart contracts in Solidity and uploading to the service block.

Feel free to give feedback by creating an Issue on Github.

## Users

A user is a shareholder and/or CEO and/or chairman of the board. A user is either active or passive.

An active user is authenticated and can write changed directly into the shareholder register, like transferring shares or changing their address.

A passive user is a shareholder who is not registered on the platform. The user cannot make changes in the shareholder register, and any transfers has to be input by the chairman of the board, on behalf of the shareholder.

<aside class=“notice”>
All changes in the shareholder register has to be approved by the chairman of the board. In future versions, this approval can be granted automatically if the articles of association and shareholder agreements are automated (i.e. programmed as code).
</aside>

# Installation

To install the SDK to your project just use NPM:

`npm i @brreg-sdk`
 

## Example application
It can be hard getting started. We recommend you take a look at our example application to get a feel of the SDK.
<a href="https://github.com/blockchangers/brreg/tree/master/packages/forvalter" target="_blank">https://github.com/blockchangers/brreg/tree/master/packages/forvalter</a>
