Account related API.
With Account related account you can create new account, 

### Create new account
Create a new account.

#### Returns
Returns an nebulas account object.

SDK API:
* js
```js
var account = new Account();
```
* java
```java
AccountManager manager = new AccountManager();
Address address = manager.newAccount("passphrase".getBytes());  //create a new account
```
* python
```
```

### Get account address
Get the address of an account. 

#### Returns
Returns the address string.

SDK API:
* js

Definition
```js
account.getAddressString()
```
Example:
```js
var account = new Account();
var address = account.getAddressString(); // 
```

* java

Definition
```java

```
Example
```java
AccountManager manager = new AccountManager();
Address address = manager.newAccount("passphrase".getBytes());  //create a new account
Sting strAddress = address.string();
```

### Get account public key
Get the public key. The public-private key pair is generated using secp256k1 (one of  ECDSA).

#### Returns
Returns the public key string.

SDK API:
* js

Defination
```js
account.getPublicKeyString();
```
Example
```js
var privKey = account.getPublicKeyString();
```
* java

Definition
```java

```
Example
```java
//unimplenmented
```

### Get account private key


#### Returns
Returns the private key string.

SDK API:
* js

Defination
```js
account.getPrivateKeyString();
```
Example
```js
var privKey = account.getPrivateKeyString();
```
* java

Defination
```javascript

```
SDK API:
```java
//unimplenmented
```

### Check address validity
To check if a given address is valid. Nebulas account address system is carefully designed and there is a checksum to avoid invalid address made by mistake.

#### ARGUMENTS 
address: the address that you want to check.

#### Returns
Returns a boolean value that indicates the address validity.

SDK API:
* js

Defination
```js
Account.isValidAddress(address);
```
Example
```js
var validity = Account.isValidAddress("n1QZMXSZtW7BUerroSms4axNfyBGyFGkrh5");
console.log( validity ? "valid address" : "invalid address" );
```
* java

Definition
```java

```
Example
```java
//unimplenmented
```

### Generate keystore json
Keystore Json is a Json object that contains your encrypted private key. To create a Keystore Json, you need to provide a "passphrase", firstly it will be encrypted by "scrypt" or "pbkdf2" to get an encrypted passphrase. Then this encrypted passphrase is used to encrypt your private-key with AES such as "aes-128-ctr". All these detailed encryption parameters  will be returned within a Json object.

#### ARGUMENTS 

* passphrase: the passphrase that used to encrypt your private-key

#### Returns
Returns a Json object that contains the encrypt message and encrypted private-key.

SDK API:

* js

Definition
```js
account.tokey(passphrase)  //return an object
account.toKeyString(passphrase) // return an keystore json string
```
Example
```js
var keystore = new Account().toKeyString("passphrase");
```
* java

Defination
```javascript

```
Example
```java
AccountManager manager = new AccountManager();
Address address = manager.newAccount("passphrase".getBytes());  //create a new account
byte[] walletFile = manager.export(address, passphrase);
```

### Restore account from keystore 
This is the inverse operation to generating keystore. You can restore your account from keystore Json with passphrase.

#### ARGUMENTS 

* keyJson: the KeyStroe Json. (in the format of string or buffer, which depends on the SDK you are using)
* passphrase: the passphrase that used to encrypt/decrypt your private-key
* strict: if the keyJson is in 'strict' mode, which means that if the Json data is case sensitive.

#### Returns
Returns an account object that restored from keystore data.

SDK API:

* js

Defination
```js
account.fromKey(keyJson, password, nonStrict)
```
Examples:
```js
var keyJson = '{"address":"n1FF1nz6tarkDVwWQkMnnwFPuPKUaQTdptE","crypto":{"cipher":"aes-128-ctr","ciphertext":"b5041a4b9d4738bc2bcce580aeaadf53aa7c63b6aa3916b76c452630692fc397","cipherparams":{"iv":"f9d54f7854929e9e28731ee69d306a22"},"kdf":"scrypt","kdfparams":{"dklen":32,"n":4096,"p":1,"r":8,"salt":"daa130fd5e3f9a77efe6028170becf7b1d9c73ce5c1d75d1142e90a68df12fed"},"mac":"aa390e6ed50741ed38670d1e1b11a1e44e174f9f66e41acc2e2d1762ebf1dfad","machash":"sha3256"},"id":"078fcad9-8f82-40e0-96c4-fb14b986c134","version":3}';
var password = "passphrase"
var account = new Account().fromKey(keyJson, password);
```

* java

Defination
```java
```
Example
```java
AccountManager manager = new AccountManager();
manager.load(walletFile, passphrase);
```
