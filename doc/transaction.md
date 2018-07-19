Transaction related API.

### Create new transaction
Create a transaction object. This is the `Transaction` class constructor.

#### Arguments:
* chainID: Integer. The chainId of network you want to use. It's configured in the `config` file. For mainnet, chainId is 1, for testnet chainId is 1001.
* from: an account object. It's the sender account of this transaction.
* to: an address string. It's the receiver account of this transaction, or the contract address if this is a call type transaction.
* value: string. The transfer value of this transaction, it's unit is wei.
* nonce: Integer. 
* gasPrice: string. The gasPrice of this transaction.
* gasLimit: String.
* contract: object. An object that contains parameters for deploy/call smart contract.

#### returns

SDK API:

* js
```js
var acc = Account.NewAccount();

var tx = new Transaction({
   chainID: 1,
   from: acc,
   to: "n1SAeQRVn33bamxN4ehWUT7JGdxipwn8b17",
   value: "1000000000000000000", //1nas
   nonce: 12,
   gasPrice: 1000000,
   gasLimit: 2000000,
   contract: {
       function: "save",
       args: "[0]"
   }
});
```
* java
```java
// binary tx
int chainID = 100; //1 mainet,1001 testnet, 100 default private
Address to = manager.newAccount("topassphrase".getBytes());
Address to = Address.ParseFromString("n1g6JZsQS1uRUySdwvuFJ7FYT4dFoyoSN5q");
BigInteger value = new BigInteger("0");
long nonce = 1; // nonce = from.nonce + 1
Transaction.PayloadType payloadType = Transaction.PayloadType.BINARY;
byte[] payload = new TransactionBinaryPayload(null).toBytes();
BigInteger gasPrice = new BigInteger("1000000"); // 0 < gasPrice < 10^12
BigInteger gasLimit = new BigInteger("20000"); // 20000 < gasPrice < 50*10^9
Transaction tx = new Transaction(chainID, from, to, value, nonce, payloadType, payload, gasPrice, gasLimit);        
```


### Calculate transaction hash
Calculate the hash of this transaction, the hash algorithm is SHA3-256.

SDK API:

* js

Definition 
```javascript
transaction.hashTransaction();
```
Example
```js
var txHash = tx.hashTransaction();
```
* java
```java
byte[] hash = tx.calculateHash();
```

### Sign the transaction
Sign the transaction with the private key of sender account, the signature algrithom is secp256k1.

SDK API:

* js
```js
var txHash = tx.signTransaction();
```
* java
```java
manager.signTransaction(tx, passphrase);  //todo...
```

### Get transaction string
Get a string that contains all the detailed infomation of this trasaction.  It's is mainly used to print out the transaction information.

SDK API:

* js

Definition
```javascript
transaction.toString()
```
Example
```js
var txHash = tx.toString();
```
* java

Definition
```java 
```
Example
```java
//unimplenmented
```

### Get raw transaction
To generate a raw data of this transaction, it's a serialized data of this transaction in the format of ProtoBuff.

SDK API:

* js
```js
var acc = Account.NewAccount();
var tx = new Transaction({
   chainID: 1,
   from: acc,
   to: "n1SAeQRVn33bamxN4ehWUT7JGdxipwn8b17",
   value: 10,
   nonce: 12,
   gasPrice: 1000000,
   gasLimit: 2000000
});
tx.signTransaction();
var txRawData = tx.toProto();
```
* java
```java
tx = new Transaction(chainID, from, to, value, nonce, payloadType, payload, gasPrice, gasLimit);
manager.signTransaction(tx,passphrase);
rawData = tx.toProto();
```
