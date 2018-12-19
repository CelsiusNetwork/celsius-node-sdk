![Institutional Partner Overview](/assets/images/institutional-partner.svg)

# Use case

The Institutional Partner API offers partners the ability to use Celsius Network features as a legal entity rather then as a user. This means that the benefits and features of Celsius Network can be accessed through the API rather than from a mobile app. 

# Features

- ***Deposits & withdrawals***
> Partner can do deposits and withdrawals of cryptocurrencies to the Celsius account to start earning interest.
- ***Balance & tranaction checking***
> Partner can check their account balances and transaction statuses on different blockchains.

# Getting started

## Security

1. Partner receives a **partner-token** and the **api-key** from Celsius Network that will be used to authenticate that partner on Celsius API.
2. Each request sent to the Celsius API is followed by the partner token and api key to successfully authenticate the partner.
3. Each response sent back from the Celsius API will be signed using Celsius Network's private key, and will be automatically verified on the SDK receiving end with the hardcoded public key. 

## Initializing the SDK

Initialize SDK in the following way:

```javascript
const { Celsius, AUTH_METHODS, ENVIRONMENT } = require('index')
const partnerKey = PARTNER_TOKEN

const celsius = Celsius({
    authMethod: AUTH_METHODS.USER_TOKEN,
    partnerKey: partnerKey,
    environment: ENVIRONMENT.staging // If not present, default is production.
})

```
## Using SDK

After initializing SDK, partner can perform following actions:

#### Get balance for all currencies
```javascript
const userSecret = USER_TOKEN

celsius.getBalanceSummary(userSecret).then((balanceSummary) => {
    console.log(balanceSummary)
})
.catch((error) => {
    console.log(error)
})
```
#### Get balance for a single currency
```javascript
const coin = 'BTC'
const userSecret = USER_TOKEN

celsius.getCoinBalance(coin, userSecret).then((balanceSummary) => {
    console.log(balanceSummary)
})
.catch((error) => {
    console.log(error)
})
```
#### Get paginated list of transactions for all currencies 
```javascript
const pagination = {
  page: 1,
  perPage: 20
}
const userSecret = USER_TOKEN

celsius.getTransctionSummary(pagination, userSecret).then((transactions) => {
    console.log(transactions)
})
.catch((error) => {
    console.log(error)
})
```
#### Get paginated list of transactions for a single currency
```javascript
const coin = 'BTC'
const pagination = {
  page: 1,
  perPage: 20
}
const userSecret = USER_TOKEN

celsius.getCoinTransactions(coin, pagination, userSecret).then((transactions) => {
    console.log(transactions)
})
.catch((error) => {
    console.log(error)
})
```
#### Get address of a wallet for a currency
```javascript
const coin = 'BTC'
const userSecret = USER_TOKEN

celsius.getDeposit(coin, userSecret).then((address) => {
    console.log(address)
})
.catch((error) => {
    console.log(error)
})
```
#### Withdraw funds to an address
```javascript
const coin = 'BTC'
const formFields = {
    address: DESTINATION_ADDRESS,
    amount: AMOUNT
}
const userSecret = USER_TOKEN

celsius.withdraw(coin, formFields, userSecret).then((transactionId) => {
    console.log(transactionId)
})
.catch((error) => {
    console.log(error)
})
```
#### Get status of a transaction
```javascript
const transaction = TRANSACTION_ID
const userSecret = USER_TOKEN

celsius.getTransactionStatus(transaction, userSecret).then((status) => {
    console.log(status)
})
.catch((error) => {
    console.log(error)
})
```
