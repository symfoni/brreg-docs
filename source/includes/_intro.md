# Brreg Cap Table (BrregCapTable) Developer Documentation

## Introduction
Welcome to the "Brønnøysund Business Cap Table" (beta) developer documentation, BrregCapTable in short. 

There are some 321 000 limited liability companies in Norway - less than 1000 have their shareholding listed in a securities register. While every company is obliged to keep an updated cap table, the large majority of companies report shareholding only for tax purposes once a year.

A lot of people believe in a local business or a start-up, but few have the energy and insights to actually make an investment. What energy might be released if more people were able to take part in financing ideas they believe in. By providing an infrastructure, we hope to establish a platform that make ownership transparent and lower the risks of engaging with small and mediums sized enterprises. Doing so is part of a broad effort to make capital more efficient, for example by making shares liquid, allowing their use as collateral and link loans, mortgages and payments direct to shares and share transactions. In the process, it is quite possible to imagine a greatly simplified public reporting where regulators may themselves access the required data - and a greatly simplified corporate governance involving share loyalty programs, the payment of dividends and voting. In short, the platform may serve to open and democratizing the unlisted markets for new groups of investors.

Norwegian limited liability companies must have a share capital of at least NOK 30,000 assigned to one or more shares, each of identical nominal value. The total share capital, the number of shares and their nominal value are stated in the company's articles of association.

All limited liability companies shall have a register of shareholders unless the company's shares are registered in a securities register. The cap table shall at all times contain an overview of the company’s shareholders, and it will normally determine who may exercise shareholder rights including the right to vote at the general meeting and the right to receive dividends. The cap table is in principle public - insight may not be denied.

### What is a cap table?
Upon listing a shareholder in the shareholders' register the company shall notify the shareholder thereof. The shareholders’ register shall be updated in accordance with established rules in the Companies Act (§ 4-7) to reflect changes of ownership or pledging of shares.
Shares can be sold or given away without payment unless otherwise stated by law, articles of association or agreement between the shareholders. In the case of a sale, the price is normally calculated based on market value. Transfers of ownership below market value are referred to as “gift sale” and may trigger a tax liability.
When shareholders sell or otherwise realize shares, gains will be taxable and losses deductible.
The Companies Act contains rules on the consent of acquiring shares, and rules on pre-emption rights for the other shareholders. An agreement to transfer shares shall be reported to the board of the limited company by the person acquiring the shares. The agreement should as a minimum list the parties, the number of shares to be transferred, and at what price.
Transfers in BrregCapTable will be reported automatically. The new shareholder must be notified by the company that she has been included in the shareholders' register and what is listed.

<aside class = "success">Companies and shareholders that rely on BrregCapTable may need not keep a separate cap table nor report its details to the government as everything is automated.</aside>

#### Shareholder agreements
Shareholder agreements are normally entered into between shareholders of a company and regulate the relationship between them. Shareholders are not obliged to enter into such an agreement, but it may be useful. A shareholder agreement obliges only the shareholders who have signed the agreement. There are no requirements as to how the agreement should look or what it should contain. Examples of conditions that can be regulated in a shareholder agreement are rules relating to ownership, demands for dividends, non-compete clauses, impartiality and work/employment requirements.

#### Conflict between shareholders
It is not uncommon for conflicts between shareholders to arise regarding the organization and running of a company. Since the causes of conflict may be difficult to spot in advance, it may make sense to

* Avoid a setup where two owners hold 50% of the shares each and hence become incapable of making majority decisions in cases of conflict
* Enter into shareholder agreements that clarify how the relationship between shareholders in the event of disagreement.

In cases where the shareholders no longer manage to cooperate with each other, the district court may, in response to a lawsuit from a shareholder or from the company, decide on the redemption or release of a shareholder's shares. Such lawsuits must be regarded as last resort, and there must be weighty reasons.

# Integrate your application
A project that is looking to integrate with BrregCapTable has 5 different avenues to interact with the protocol implementation. The integration types are as follows:

* [SDK](https://www.npmjs.com/package/@brreg/sdk)
* [Smart Contracts](https://gitlab.com/blockchangers/brreg/tree/master/packages/contracts/src/contracts)
* [Web3](https://docs.ethers.io/ethers.js/html/)
* [GraphQL](http://52.158.44.155:4000/graphiql)
* [REST](http://52.158.44.155:4000/api_docs)

The SDK makes it easy to make read and makes changes to company cap tables. A smart contract integration allows you to extend the register itself. For new smart contract developers we recommend this <a href="https://karl.tech/learning-solidity-part-1-deploy-a-contract/" target="_blank">Learning Solidity tutorial series by Karl Floersch</a>. The common methods existing applications use to integrate with our protocol implementation are through our SDK. Explore the SDK guides to learn more!

## Demo data

We have extracted data from our registries for about 130 companies respectively. It is stored in two excel files.

[Download here](https://drive.google.com/drive/folders/1c2c54U8-klVijtEUrP_yhdLHFnw0CkFB?usp=sharing)

# Main Concepts

## Common Terms
This is a list of terms you might encounter when developing on BrregCapTable.

### Cap table

* A ledger showing the shareholders of a company and their shareholding
* The Norwegian term is “aksjeeierbok”, literally a “book” of shareholders 

### Registry of cap tables

* Registry of all cap tables on BrregCapTable
* This is where you can get a list of all cap tables for companies.

### Entity registry

* Information about people and companies
* "Enhetsregisteret", in Norwegian

### Chairman of the board

* The legal entity responsible for the cap table

### Share class 

* Share classes are called _partitions_ in the SDK

### Block explorer

* Service that allows a view into what is happening on the blockchain
* Link in the menu to the left

### Blockchain

* A peer to peer ledger, like a database. “Writes” to the blockchain is done by the user in question directly instead of a server authenticating the user and storing the data for her. 
* BrregCapTable is built on Ethereum whose underlying technology is blockchain. 
* Any reference to blockchain, Ethereum or smart contract is a reference to this underlying technology.

### Smart Contracts

*   A piece of code (or program) that is stored on the blockchain. Conditions of the contract are predefined by the users; if all conditions are met, certain actions are executed by the contract (program).

### Wallet

*   The interface/client / wrapper / holder that allows users to manage their account(s) and interactions with the blockchain.
*   Examples: MetaMask.io, your Ledger Hardware Wallet, a Multisig Wallet Contract.

### Account

*   A pair consisting of a public & private key that identifies an entity on the platform.
*   The user's stock and operations are actually stored on the blockchain, not in the wallet or account.
*   Just like your Facebook account has a `Name (public)` and `password (private)`, so does your Ethereum account.

### Address _("Public Key")_

*   You use this as a reference to another user or smart contract.
*   Sometimes referred to as the "public key"
*   A string made up of `0x` + `40 hexadecimal characters`.
*   In Ethereum, the addresses begin with `0x`.
*   Example: `0x06A85356DCb5b307096726FB86A78c59D38e08ee`

### Public Key

*   A central concept of cryptography is the pairing of a public and a private key.
*   You can derive a public key from a private key, but cannot derive a private key from a public key.
*   (Advanced) In Ethereum, the address "acts" like the public key, but it's not actually the public key.
*   (Advanced) In Ethereum, the public key is derived from the private key and is 128 hex characters. You then take the `"SHA3" (Keccak-256)` hash of this (64 characters), take the last 40 characters, and prefix with `0x`, give you your 42-character address.

### Private Key

*   You use this to send stock or issue commands **from** an account.
*   The secret half of your Address / public key.
*   A string of 64 hexadecimal characters.
*   Every string of 64 hexadecimal characters is a private key.
*   If you hand-type a private key differently today than yesterday, you will access a different wallet. Never hand type your private key.
*   This is the string you need to send from your account. Without the private key you cannot access your account. Although, you don't need to save this raw, unencrypted private key in this format. You can save the fancy versions of it (e.g. the Keystore File / Mnemonic Phrase).
*   Example: `afdfd9c3d2095ef696594f6cedcae59e72dcd697e2a7521b1578140422a4f890`

### Mnemonic Phrase / Seed Phrase / Seed Words

*   Another fancy version of your private key, that is actually used to derive multiple private keys.
*   A (typically) phrase consisting of 12 or 24 words that allow you to access an infinite number of accounts.
*   Used by Ledger, TREZOR, MetaMask, Jaxx, and others.
*   Originates from [BIP 39 Spec](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki).
*   The accounts you can access with this phrase are determined by the "path".
*   Example 12-words: `brain surround have swap horror body response double fire dumb bring hazard`
*   Example 24-words: `card enrich gesture connect kick topple fan body blind engine lemon swarm venue praise addict agent unaware equal bean sing govern income link leg`

### Hardware Wallet:

*   Typically, a single-purpose device that "holds" your private key(s), ensuring your private keys are safe.
*   Typically, they use a 24-word phrase. This phrase you should write down (not on your computer) and store separately from your hardware wallet.
*   If you lose your hardware wallet, you can still gain access to your accounts via the word-phrase you wrote down.
*   Never type the word-phrase on your computer. It defeats the purpose of your hardware wallet.

### Hexadecimal

*   Used all over Ethereum for a variety of things, a hexadecimal string is comprised of the numbers `0 1 2 3 4 5 6 7 8 9` and `A B C D E F`

### Seed

*   The input that is used to derive a private key from a public key. This should always be generated in a truly random way.

### Encryption

*   Encryption is the act of taking a string of letters/numbers such as your private key and turning them into another string of letters/numbers through a method of private translation.
*   There are various encryption methods.
*   Encryption offers protection against information theft!

### Encrypted vs Unencrypted Keys

*   An unencrypted private key is 64 characters long, and it is used to unlock or restore wallets.
*   An encrypted key is also 64 letters long and is a regular private key that has gone through the process of encryption, as defined above.
*   For example, if the word ‘Apple’ was your shortened private key, then it was encrypted three letters down the alphabet, your new shortened encrypted key would be ‘Dssoh’. Since you know the way to encrypt this key, you could derive the original private key from it by reversing the method of encryption.
*   Encrypted private keys are usually kept within the extension or device they are encrypted by, and they remain out of sight from the user. This is meant to add another layer of security to keep a user’s wallet information safe.

All feedback, rewrites, clarification, typo-fixing, and requests for additions are more than welcome.

Thanks to [MetaMask](https://metamask.github.io/metamask-docs/Main_Concepts/Common_Terms) for this Glossary starting point.

## Users

A user is a shareholder and/or CEO and/or chairman of the board. A user is either active or passive.

An active user is authenticated and can write changed directly into the shareholder register, like transferring shares or changing their address.

A passive user is a shareholder who is not registered on the platform. A passive user cannot make changes in the shareholder register, and any transfers have to be input by the chairman of the board, on behalf of the shareholder.

<aside class=“notice”>
All changes in the shareholder register have to be approved by the chairman of the board. In future versions, this approval can be granted automatically if the articles of association and shareholder agreements are automated (i.e. programmed as code).
</aside>

## Networks and endpoints

### Localhost
You can run the whole blockchain locally. This part is undocumented at this stage, but [all of the source code is available on Gitlab](https://gitlab.com/blockchangers/brreg).

### Staging 
The staging blockchain is named _Toyen_ and is open to everyone. This is the recommended way to get started with integration with the platform. 

Relevant details

* RPC endpoint URL: `http://ethjygmk4-dns-reg1.northeurope.cloudapp.azure.com:8540`
* Websocket endpoint: `ws://ethjygmk4-dns-reg1-0.northeurope.cloudapp.azure.com:8547`
* [Block explorer](http://52.158.44.155:4000/)
* [Example application](https://blockchangers.gitlab.io/brreg/)
* [GraphQL query generator](http://52.158.44.155:4000/graphiql)
* Network ID: `53387025`


<aside note="warning">Please be advised that there currently is not implemented any throttling or DDOS prevention. Please use the blockchain accordingly. </aside>

### Production
The production version of the platform is not live yet. 



