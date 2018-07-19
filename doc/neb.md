## Neb

Neb introduction.

### Neb constructor
Neb is an object than handles the http request of Nebulas APIs. 

#### Arguments:
| | |
|---:|---|
|request| optional, the http request object for Neb.|

#### Returns

SDK API

* js

Definition
```js
new Neb(request)
```
Example
```js
var neb = new Neb()
//or
var neb = new Neb(new HttpRequest("http://127.0.0.1:8685"))
```

* python

Definition
```python
        
```
Example
```python
        
```

### Set Request
Assign an request object to Neb. 

#### Arguments:
* request: the http request object for Neb.

#### Returns

SDK API

* js

Definition
```js
neb.setRequest(request);        
```
Example
```js
var neb = new Neb();
neb.setRequest(new HttpRequest("http://127.0.0.1:8685"));
```

* python

Definition
```python

```
Example
```python

```
----

## Neb.api
`neb.api` 

### api.GetNebState
Get the current of the Nebulas node.

#### Arguments:
none

#### Returns
|  |  |
|---:|:---|
|chain_id| Block chain id，|
|tail |Current neb tail hash|
|lib |Current neb lib hash|
|height |Current neb tail block height|
|protocol_version |The current neb protocol version.|
|synchronized |The peer sync status.|
|version |neb version.|

SDK API

* js


Definition
```js
neb.api.getNebState();
```
Example request
```js
var neb = new Neb(new HttpRequest("https://testnet.nebulas.io"));
neb.api.getNebState().then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "chain_id": 1001,
    "tail": "5074f686cfa0ad7fc2ce9688828429d44c4122c8b51d1a8e14d43a5ed7683c9b",
    "lib": "3da30a67313cc449e8c303caa307aad68e53444b9d7373d8fd4868af1426734c",
    "height": "617278",
    "protocol_version": "/neb/1.0.0",
    "synchronized": false,
    "version": "0.7.0"
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.GetAccountState
Get the state of given account at a certain block height, including it's balance, nonce, type.

#### Arguments:
| | |
|---|---|
|address|Account address |
|height|[optional] the height at which you want to check account state|

#### Returns
|  |  |
|---:|:---|
|balance |Current balance in unit of 1/(10^18) nas.|
|nonce |Current transaction count.|
|type |The type of address, 87 stands for normal address and 88 stands for contract address|

SDK API

* js


Definition
```js
neb.api.GetAccountState();
```
Example request
```js
var neb = new Neb(new HttpRequest("https://testnet.nebulas.io"));
neb.api.GetAccountState("n1H2Yb5Q6ZfKvs61htVSV4b1U2gr2GA9vo6").then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
        "balance": "100998537876999980",
        "nonce": "45",
        "type": 87
    }

```

* python

Definition
```python
        
```
Example
```python
        
```

### api.LatestIrreversibleBlock


#### Arguments:
none

#### Returns
Return the block information of last irreversible block.
The return data structure is the same with `api.getBlockByHeight`, `api.getBlockByHash`.

|  |  |
|---:|:---|
|hash |Hex string of block hash.|
|parent_hash |Hex string of block parent hash.|
|height |block height.|
|nonce |block nonce.|
|coinbase |Hex string of coinbase address.|
|timestamp |lock timestamp.|
|chain_id |block chain id.|
|state_root |Hex string of state root.|
|txs_root |Hex string of txs root.|
|events_root| Hex string of event root.|
|consensus_root|    Timestamp: time of consensus state <br> Proposer: proposer of current consensus state <br> DynastyRoot: Hex string of dynasty root
|miner| the miner of this block|
|is_finality |block is finality|
|transactions |block transactions array.|

SDK API

* js


Definition
```js
neb.api.latestIrreversibleBlock();
```
Example request
```js
var neb = new Neb(new HttpRequest("http://127.0.0.1:8685"));
neb.api.latestIrreversibleBlock().then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "hash": "f58a07a8c447d12b288941eb5e71b62a0b1c4a6c9a242b944aac3023c539d263",
    "parent_hash": "818f7ac47e64471f978ba9012fd20da09f17eb723b6049f4469784bebe17aee6",
    "height": "616847",
    "nonce": "0",
    "coinbase": "n1EzGmFsVepKduN1U5QFyhLqpzFvM9sRSmG",
    "timestamp": "1531982310",
    "chain_id": 1001,
    "state_root": "e939ad077b3d8580f97e576377947a6c0f1743a8a57506690728445a2ed570a8",
    "txs_root": "5b87879276aab4d835d8757516e745f6ea6c6000f968d4adc0ad084eeac85579",
    "events_root": "e95c6ec9fad2e7f08857f996f50e511f597505b1601e1a39a8fcb6bc1bf18435",
    "consensus_root": {
        "timestamp": "1531982310",
        "proposer": "GVf10Wffwurzz8fRT7j1rE+7LRsAI/wTKCI=",
        "dynasty_root": "5bKcGDNXRehSNJRtpdg/B0erRprSzkUUjYm6UCu4fvw="
    },
    "miner": "n1cvciAzQHzvsWQoP12HJc2qGnuB8Fr7hcM",
    "randomSeed": "2129317d84d71e55db09b66fe0042bb6cc53b6a9c4989b69b492f14956b46384",
    "randomProof": "8ae5ad23c956176fcf2155dcb41fd08e45263f280bc3a9d0d8620d0ad1817b2ce5321ba5af790fc3dfe4f0898f2af292ae75bec1227b257166d32a6f2427a62a04bc5c0590939659d28300c5e7fa07ec54d05945bd55133f0aba2325e40dd12f8f81f4af0aaab8b87caffcf519e2800090db0795d6170df9641efac47d46f31fde",
    "is_finality": false,
    "transactions": []
    }
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.Call
Simulate a transaction execution, it's used to check the results or errors of an transaction, such as get data from a smart-contract. The transaction in only executed on current node, and will not be broadcast.


#### Arguments:
The arguments is the detailed information of an transaction, they are the same as `admin.sendTransaction`, `admin.sendTransactionWithPassphrase`, `api.estimateGas`.

| | |
|---:|---|
|from| Hex string of the sender account addresss.
|to |Hex string of the receiver account addresss.
value |Amount of value sending with this transaction. The unit is Wei (10^-18 NAS).
nonce |Transaction nonce.
gas_price |gasPrice sending with this transaction.
gas_limit |gasLimit sending with this transaction.
type |[optional] transaction payload type. If the type is specified, the transaction type is determined and the corresponding parameter needs to be passed in, otherwise the transaction type is determined according to the contract and binary data. 
contract |transaction contract object for deploy/call smart contract. [optional]
binary |any binary data with a length limit = 64bytes. [optional]

#### Returns
The execution result of this transaction

|  |  |
|---:|:---|
result| The execution result. For binary type, result="", for call type, result is the return value of function you called. 
execute_err| The execution error
estimate_gas| the gas consumption of this transaction

SDK API

* js

Definition
```js
neb.api.call();
```
Example request
```js
var neb = new Neb(new HttpRequest("http://127.0.0.1:8685"));
neb.api.call({
     "from": "n1GDCCpQ2Z97o9vei2ajq6frrTPyLNCbnt7",
     "to": "n1oXdmwuo5jJRExnZR5rbceMEyzRsPeALgm",
     "value": "100000",
     "nonce": 1,
     "gasPrice": "1000000",
     "gasLimit": "200000",
     "type":"call",
     "contract":{
        "function":"get",
        "args":"[\"nebulas\"]"
        
     }
}).then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "result": "{\"key\":\"nebulas\",\"value\":\"forever nebulas!\",\"author\":\"n1JmhE82GNjdZPNZr6dgUuSfzy2WRwmD9zy\"}",
    "execute_err": "",
    "estimate_gas": "20221"
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.SendRawTransaction

Send raw-transaction to Nebulas blockchain. The raw-transaction is the serialized raw data of a signed transaction in the format of ProtoBuff. 

#### Arguments:
| | |
|---:|---|
data| the raw-transaction data

#### Returns
Return the transaction hash, and contract-address if it's a deploy type.

|  |  |
|---:|:---|
txhash| Hex string of transaction hash.
contract_address |returns only for deploy contract transaction.

SDK API

* js

Definition
```js
neb.api.sendRawTransaction(rawData);
```
Example request
```js
var neb = new Neb(new HttpRequest("http://127.0.0.1:8685"));
neb.api.sendRawTransaction("CiBzV4bKsLX2vqLle2gU95CA1GsjjmmQXhhl3UE8fh9eiRIaGVdbcSH1YDnK0rCdK3N4j9AYzmuPgqjg+EcaGhlXW3Eh9WA5ytKwnStzeI/QGM5rj4Ko4PhHIhAAAAAAAAAAAAAAAAAAAAAAKAEwmeCC2QU6CAoGYmluYXJ5QGRKEAAAAAAAAAAAAAAAAAAPQkBSEAAAAAAAAAAAAAAAAAADDUBYAWJBCE3mlC/AJvGRbglshH8WeHo1waauObOm8vZLCnWeMC8FfnUwTjMrd+1o0PcrySEBtUi7FEWHfEEtyAHLZeu1mwE=")
.then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "txhash": "735786cab0b5f6bea2e57b6814f79080d46b238e69905e1865dd413c7e1f5e89",
    "contract_address": ""
}
```

* python

Definition
```python
        
```
Example
```python
        
```
### api.GetBlockByHash
Get the block information of a given hash.

#### Arguments:
|  |  |
|---:|:---|
hash |Hex string of block hash.
full_fill_transaction |If true it returns the full transaction objects, if false only the hashes of the transactions.

#### Returns
Return the block info.

SDK API

* js

Definition
```js
neb.api.getBlockByHash(hash);
```
Example request
```js
var neb = new Neb(new HttpRequest("https://testnet.nebulas.io"));
neb.api.getBlockByHash("67203509b8c312bbfee46955595659cecb412e1ec81f08d1c74d76f4dec08e64").then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "hash": "67203509b8c312bbfee46955595659cecb412e1ec81f08d1c74d76f4dec08e64",
    "parent_hash": "e9f20422a0bd40c4dbae855c4caaaf0d03390d14b8eddd8f9a3d59f11437cacc",
    "height": "616855",
    "nonce": "0",
    "coinbase": "n1EzGmFsVepKduN1U5QFyhLqpzFvM9sRSmG",
    "timestamp": "1531982430",
    "chain_id": 1001,
    "state_root": "2db5dc1c725d4336bd9aa5631dbc0921ad528e113e956c2294572444e4d91dac",
    "txs_root": "52e685b10c585f4ae20c1ef89f30af136350266050007809c7ad6434f2aa0635",
    "events_root": "80d2162b2233697b4fc6d31888ba8b2054abb4eaa6d3689e2efcca4ae9138620",
    "consensus_root": {
        "timestamp": "1531982430",
        "proposer": "GVc9sJxVjKzDpotRdRyTG0YT+t6f9X6uV7Q=",
        "dynasty_root": "5bKcGDNXRehSNJRtpdg/B0erRprSzkUUjYm6UCu4fvw="
    },
    "miner": "n1L936EYUJkh5FrFXaLCa8ogd88dEUHbHEK",
    "randomSeed": "c7b06b6209646dbf6db1600b882c9a433c75f1c4579042a96ebc4160d2fc9fe6",
    "randomProof": "b2040a5dc5cb5e5517273c3119b2a1a035e4fe9d1f653df77e9ebc9a76ecb775ff1dd1f5efc26a78204808158a2d8d8e7b2d62abe787ea68e036095c4804652e046a8e33ab48e5b78809645327a0589bbe7a7ffdbefa775de06fdf6eabf12ab7aeac3fe4a895d0be85ec5471d921b3f0f91f33aa428568fdd448176f4b32ce0aba",
    "is_finality": true,
    "transactions": [
        {
            "hash": "2438c15bf11341a5e401c26fcdf0b5ec599c791b8e7a1a184ac0b8912e848a29",
            "chainId": 0,
            "from": "",
            "to": "",
            "value": "",
            "nonce": "0",
            "timestamp": "0",
            "type": "",
            "data": null,
            "gas_price": "",
            "gas_limit": "",
            "contract_address": "",
            "status": 0,
            "gas_used": "",
            "execute_error": "",
            "execute_result": ""
        },
        {
            "hash": "92f27f046ba4a428eb36ed09d6d429660221b6a89b70b5953394aa4e5ed879e5",
            "chainId": 0,
            "from": "",
            "to": "",
            "value": "",
            "nonce": "0",
            "timestamp": "0",
            "type": "",
            "data": null,
            "gas_price": "",
            "gas_limit": "",
            "contract_address": "",
            "status": 0,
            "gas_used": "",
            "execute_error": "",
            "execute_result": ""
        }
    ]
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.GetBlockByHeight
Get the block information of a certain height.

#### Arguments:
|  |  |
|---:|:---|
height | [integer] the height of block.
full_fill_transaction |If true it returns the full transaction objects, if false only the hashes of the transactions.

#### Returns
Return the block info.

SDK API

* js

Definition
```js
neb.api.getBlockByHeight(height);
```
Example request
```js
var neb = new Neb(new HttpRequest("http://127.0.0.1:8685"));
neb.api.getBlockByHeight(616855).then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "hash": "67203509b8c312bbfee46955595659cecb412e1ec81f08d1c74d76f4dec08e64",
    "parent_hash": "e9f20422a0bd40c4dbae855c4caaaf0d03390d14b8eddd8f9a3d59f11437cacc",
    "height": "616855",
    "nonce": "0",
    "coinbase": "n1EzGmFsVepKduN1U5QFyhLqpzFvM9sRSmG",
    "timestamp": "1531982430",
    "chain_id": 1001,
    "state_root": "2db5dc1c725d4336bd9aa5631dbc0921ad528e113e956c2294572444e4d91dac",
    "txs_root": "52e685b10c585f4ae20c1ef89f30af136350266050007809c7ad6434f2aa0635",
    "events_root": "80d2162b2233697b4fc6d31888ba8b2054abb4eaa6d3689e2efcca4ae9138620",
    "consensus_root": {
        "timestamp": "1531982430",
        "proposer": "GVc9sJxVjKzDpotRdRyTG0YT+t6f9X6uV7Q=",
        "dynasty_root": "5bKcGDNXRehSNJRtpdg/B0erRprSzkUUjYm6UCu4fvw="
    },
    "miner": "n1L936EYUJkh5FrFXaLCa8ogd88dEUHbHEK",
    "randomSeed": "c7b06b6209646dbf6db1600b882c9a433c75f1c4579042a96ebc4160d2fc9fe6",
    "randomProof": "b2040a5dc5cb5e5517273c3119b2a1a035e4fe9d1f653df77e9ebc9a76ecb775ff1dd1f5efc26a78204808158a2d8d8e7b2d62abe787ea68e036095c4804652e046a8e33ab48e5b78809645327a0589bbe7a7ffdbefa775de06fdf6eabf12ab7aeac3fe4a895d0be85ec5471d921b3f0f91f33aa428568fdd448176f4b32ce0aba",
    "is_finality": true,
    "transactions": [
        {
            "hash": "2438c15bf11341a5e401c26fcdf0b5ec599c791b8e7a1a184ac0b8912e848a29",
            "chainId": 0,
            "from": "",
            "to": "",
            "value": "",
            "nonce": "0",
            "timestamp": "0",
            "type": "",
            "data": null,
            "gas_price": "",
            "gas_limit": "",
            "contract_address": "",
            "status": 0,
            "gas_used": "",
            "execute_error": "",
            "execute_result": ""
        },
        {
            "hash": "92f27f046ba4a428eb36ed09d6d429660221b6a89b70b5953394aa4e5ed879e5",
            "chainId": 0,
            "from": "",
            "to": "",
            "value": "",
            "nonce": "0",
            "timestamp": "0",
            "type": "",
            "data": null,
            "gas_price": "",
            "gas_limit": "",
            "contract_address": "",
            "status": 0,
            "gas_used": "",
            "execute_error": "",
            "execute_result": ""
        }
    ]
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.GetTransactionReceipt
Get the transaction receipt, which contains all the detailed information of this transaction.

#### Arguments:
|  |  |
|---:|:---|
hash |Hex string of transaction hash.

#### Returns
|  |  |
|---:|:---|
hash| Hex string of tx hash.
chainId |Transaction chain id.
from |Hex string of the sender account addresss.
to |Hex string of the receiver account addresss.
value |Value of transaction.
nonce |Transaction nonce.
timestamp |Transaction timestamp.
type |Transaction type.
data |Transaction data, return the payload data.
gas_price |Transaction gas price.
gas_limit |Transaction gas limit.
contract_address |Transaction contract address.
status |Transaction status, 0 failed, 1 success, 2 pending.
gas_used| transaction gas used
execute_error |the execute error of this transaction
execute_result |return value of the smart-contract function

SDK API

* js

Definition
```js
neb.api.getTransactionReceipt(txhash);
```
Example request
```js
var neb = new Neb(new HttpRequest("http://127.0.0.1:8685"));
neb.api.getTransactionReceipt("7c206696fd17e3bde27780d07c6cdf99f6f6439fe52218a5561aa6b0a8576177").then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "hash": "7c206696fd17e3bde27780d07c6cdf99f6f6439fe52218a5561aa6b0a8576177",
    "chainId": 1001,
    "from": "n1cqh2EQFbuZz5oXAs7i7qUbeELagggBoPy",
    "to": "n1JmhE82GNjdZPNZr6dgUuSfzy2WRwmD9zy",
    "value": "1000000000000000000",
    "nonce": "1312320",
    "timestamp": "1531726464",
    "type": "binary",
    "data": null,
    "gas_price": "1000000",
    "gas_limit": "2000000",
    "contract_address": "",
    "status": 1,
    "gas_used": "20000",
    "execute_error": "",
    "execute_result": ""
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.GetTransactionByContract
Get the transaction receipt that deployed a contract with the contract address.

#### Arguments:
|  |  |
|---:|:---|
address| Hex string of contract account address.

#### Returns
Return the transaction receipt that deployed this smart-contract.
It's the same with  `api.getTransactionReceipt`

SDK API

* js

Definition
```js
neb.api.getTransactionByContract(contract_address);
```
Example request
```js
var neb = new Neb(new HttpRequest("https://testnet.nebulas.io"));
neb.api.getTransactionByContract("n1oXdmwuo5jJRExnZR5rbceMEyzRsPeALgm").then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "hash": "9e3cd30438a8a280e1668ed5f448e880f09c1672c0f47b0042fb63a4dd693130",
    "chainId": 1001,
    "from": "n1JmhE82GNjdZPNZr6dgUuSfzy2WRwmD9zy",
    "to": "n1JmhE82GNjdZPNZr6dgUuSfzy2WRwmD9zy",
    "value": "0",
    "nonce": "20",
    "timestamp": "1524733139",
    "type": "deploy",
    "data": "eyJTb3VyY2VUeXBlIjoianMiLCJTb3VyY2UiOiJcInVzZSBzdHJpY3RcIjtcblxudmFyIFdpa2lJdGVtID0gZnVuY3Rpb24odGV4dCkge1xuXHRpZiAodGV4dCkge1xuXHRcdHZhciBvYmogPSBKU09OLnBhcnNlKHRleHQpO1xuXHRcdHRoaXMua2V5ID0gb2JqLmtleTtcblx0XHR0aGlzLnZhbHVlID0gb2JqLnZhbHVlO1xuXHRcdHRoaXMuYXV0aG9yID0gb2JqLmF1dGhvcjtcblx0fSBlbHNlIHtcblx0ICAgIHRoaXMua2V5ID0gXCJcIjtcblx0ICAgIHRoaXMuYXV0aG9yID0gXCJcIjtcblx0ICAgIHRoaXMudmFsdWUgPSBcIlwiO1xuXHR9XG59O1xuXG5XaWtpSXRlbS5wcm90b3R5cGUgPSB7XG5cdHRvU3RyaW5nOiBmdW5jdGlvbiAoKSB7XG5cdFx0cmV0dXJuIEpTT04uc3RyaW5naWZ5KHRoaXMpO1xuXHR9XG59O1xuXG52YXIgU3VwZXJXaWtpID0gZnVuY3Rpb24gKCkge1xuICAgIExvY2FsQ29udHJhY3RTdG9yYWdlLmRlZmluZU1hcFByb3BlcnR5KHRoaXMsIFwicmVwb1wiLCB7XG4gICAgICAgIHBhcnNlOiBmdW5jdGlvbiAodGV4dCkge1xuICAgICAgICAgICAgcmV0dXJuIG5ldyBXaWtpSXRlbSh0ZXh0KTtcbiAgICAgICAgfSxcbiAgICAgICAgc3RyaW5naWZ5OiBmdW5jdGlvbiAobykge1xuICAgICAgICAgICAgcmV0dXJuIG8udG9TdHJpbmcoKTtcbiAgICAgICAgfVxuICAgIH0pO1xufTtcblxuU3VwZXJXaWtpLnByb3RvdHlwZSA9IHtcbiAgICBpbml0OiBmdW5jdGlvbiAoKSB7XG4gICAgICAgIC8vIHRvZG9cbiAgICB9LFxuXG4gICAgc2F2ZTogZnVuY3Rpb24gKGtleSwgdmFsdWUpIHtcbiAgICAgICAgY29uc29sZS5sb2coXCJqY2pjIHNhdmUgXCIsIGtleSwgdmFsdWUpO1xuXG4gICAgICAgIGtleSA9IGtleS50cmltKCk7XG4gICAgICAgIHZhbHVlID0gdmFsdWUudHJpbSgpO1xuICAgICAgICBpZiAoa2V5ID09PSBcIlwiIHx8IHZhbHVlID09PSBcIlwiKXtcbiAgICAgICAgICAgIHRocm93IG5ldyBFcnJvcihcImVtcHR5IGtleSAvIHZhbHVlXCIpO1xuICAgICAgICB9XG4gICAgICAgIGlmICh2YWx1ZS5sZW5ndGggXHUwMDNlIDEyOCB8fCBrZXkubGVuZ3RoIFx1MDAzZSAxMjgpe1xuICAgICAgICAgICAgdGhyb3cgbmV3IEVycm9yKFwia2V5IC8gdmFsdWUgZXhjZWVkIGxpbWl0IGxlbmd0aFwiKVxuICAgICAgICB9XG5cbiAgICAgICAgdmFyIGZyb20gPSBCbG9ja2NoYWluLnRyYW5zYWN0aW9uLmZyb207XG4gICAgICAgIHZhciB3aWtpSXRlbSA9IHRoaXMucmVwby5nZXQoa2V5KTtcbiAgICAgICAgaWYgKHdpa2lJdGVtKXtcbiAgICAgICAgICAgIHRocm93IG5ldyBFcnJvcihcInZhbHVlIGhhcyBiZWVuIHRha2VuXCIpO1xuICAgICAgICB9XG5cbiAgICAgICAgd2lraUl0ZW0gPSBuZXcgV2lraUl0ZW0oKTtcbiAgICAgICAgd2lraUl0ZW0uYXV0aG9yID0gZnJvbTtcbiAgICAgICAgd2lraUl0ZW0ua2V5ID0ga2V5O1xuICAgICAgICB3aWtpSXRlbS52YWx1ZSA9IHZhbHVlO1xuXG4gICAgICAgIHRoaXMucmVwby5wdXQoa2V5LCB3aWtpSXRlbSk7XG4gICAgfSxcblxuICAgIGdldDogZnVuY3Rpb24gKGtleSkge1xuICAgICAgICBrZXkgPSBrZXkudHJpbSgpO1xuICAgICAgICBpZiAoIGtleSA9PT0gXCJcIiApIHtcbiAgICAgICAgICAgIHRocm93IG5ldyBFcnJvcihcImVtcHR5IGtleVwiKVxuICAgICAgICB9XG4gICAgICAgIHJldHVybiB0aGlzLnJlcG8uZ2V0KGtleSk7XG4gICAgfVxufTtcbm1vZHVsZS5leHBvcnRzID0gU3VwZXJXaWtpOyIsIkFyZ3MiOiIifQ==",
    "gas_price": "1000000",
    "gas_limit": "200000",
    "contract_address": "n1oXdmwuo5jJRExnZR5rbceMEyzRsPeALgm",
    "status": 1,
    "gas_used": "21846",
    "execute_error": "",
    "execute_result": ""
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.GetGasPrice
Return current gasPrice.

#### Arguments:
none

#### Returns
|  |  |
|---:|:---|
gas_price| current gas price.

SDK API

* js

Definition
```js
neb.api.gasPrice();
```
Example request
```js
var neb = new Neb(new HttpRequest("https://testnet.nebulas.io"));
neb.api.().then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "gas_price":"1000000"
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.EstimateGas
Estimate the gas consumption of a transaction.

#### Arguments:
The same as `api.call`, `admin.sendTransaction`

#### Returns
|  |  |
|---:|:---|
gas | the estimated gas consumption
err | error message 

SDK API

* js

Definition
```js
neb.api.estimateGas();
```
Example request
```js
var neb = new Neb(new HttpRequest("https://testnet.nebulas.io"));
neb.api.estimateGas({
    "from": "n1JmhE82GNjdZPNZr6dgUuSfzy2WRwmD9zy",
    "to": "n1oXdmwuo5jJRExnZR5rbceMEyzRsPeALgm",
    "value": "100000",
    "nonce": 0,
    "gasPrice": "200000",
    "gasLimit": "200000",
    "type": "call",
    "contract": {
        "function": "get",
        "args": "[\"nebulas\"]"
    }
}).then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "gas": "20221",
    "err": ""
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.GetEventsByHash
Get the events list of a transaction.

#### Arguments:
|  |  |
|---:|:---|
hash |Hex string of transaction hash.

#### Returns
|  |  |
|---:|---|
events |the events list.


SDK API

* js

Definition
```js
neb.api.getEventsByHash(hash);
```
Example request
```js
var neb = new Neb(new HttpRequest("https://testnet.nebulas.io"));
neb.api.getEventsByHash("4bc3a3b7e3269a6c62efa68fcb6197ee13c44441145771f57aeb58559a175ec1").then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "events": [
        {
            "topic": "chain.transactionResult",
            "data": "{\"hash\":\"4bc3a3b7e3269a6c62efa68fcb6197ee13c44441145771f57aeb58559a175ec1\",\"status\":1,\"gas_used\":\"25152\",\"error\":\"\",\"execute_result\":\"\\\"\\\"\"}"
        }
    ]
}
```

* python

Definition
```python
        
```
Example
```python
        
```

### api.Subscribe

#### Arguments:


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.api.();
```
Example request
```js
var neb = new Neb(new HttpRequest("http://127.0.0.1:8685"));
neb.api.().then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json

```

* python

Definition
```python
        
```
Example
```python
        
```

### api.GetDynasty
Get the Dpos dynasty at given block height.

#### Arguments:
|  |  |
|---:|:---|
height |block height

#### Returns
|  |  |
|---:|:---|
miners |an array of miner addresses.

SDK API

* js

Definition
```js
neb.api.getDynasty(height);
```
Example request
```js
var neb = new Neb(new HttpRequest("http://127.0.0.1:8685"));
neb.api.getDynasty(666).then(function(resp) {
  console.log(resp)
}).catch(function(err) {
  console.log(err)
});
```
Example response
```json
{
    "miners": [
        "n1EpHmyeX8DXgWrmbnEuRHCADtnuJeiYKU4",
        "n1FFT2y3xfBMVTDxtsFTygsdTHCbUwuUT1Y",
        "n1FRjbdYqhfaEtdbXY1oK9vQVJ43kmf9S4K",
        "n1GHZjF1yuA6euvvvzZA9c9MdXmt8cDjeza",
        "n1Jqh2PjwJHXhyxvATAqby7bHR3EKd6cTZi",
        "n1KbWwzqhkiSMKh5beMJriA1WJENzUNdEyD",
        "n1L936EYUJkh5FrFXaLCa8ogd88dEUHbHEK",
        "n1LPJ4h4SbhugCgDJTVnHUiyeGtvKfDWegh",
        "n1NEMW2jhwzGVT3RkBt44jcyQuKTQzSPQdW",
        "n1NK2hLQU23Ttn4jxHXFEdistMUvvHTNwBF",
        "n1PxjEu9sa2nvk9SjSGtJA91nthogZ1FhgY",
        "n1QCurQxL3inZRHEDvGKLEBNeeTNvSrGzyU",
        "n1RRsk1n5YevuhdU2jZqUfPMJYhWrmbZ61R",
        "n1ULxbaBLhQmLAa1WQEgHBJCECM12QA7TjH",
        "n1X1Jnfchqoo4Ck35np6EDUgtTsnemMHCPJ",
        "n1YJsCz8ZAX1ajy6esN8MZzJRsy1Kjw5FUN",
        "n1ZiyKqyFUKn2ych8k5dAitfq7NgLxUfgJW",
        "n1bCzYk2rGq8tFeAPLvDFpjvDM6qhmaCCpD",
        "n1cDFK4H2R79LRmVbPXh1nmuBSdDFaCvjNF",
        "n1cvciAzQHzvsWQoP12HJc2qGnuB8Fr7hcM",
        "n1dQ7TyMmmoFDqtJYq4RXXUdkkMWKEXpkEd"
    ]
}
```

* python

Definition
```python
        
```
Example
```python
        
```


## Neb.admin


### NodeInfo

#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```


### Accounts
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### NewAccount
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### UnLockAccount
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### LockAccount
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### SignTransactionWithPassphrase
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### SendTransactionWithPassphrase
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### SendTransaction
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### SignHash
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### StartPprof

#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

### GetConfig
#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

#### Arguments:
|  |  |
|---:|:---|


#### Returns
|  |  |
|---:|:---|


SDK API

* js

Definition
```js
neb.admin.nodeInfo();
```
Example request
```js

```
Example response
```json

```

