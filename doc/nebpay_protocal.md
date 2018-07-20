##  Nebpay protocols

### Payment Process



![](https://github.com/nebulasio/nebPay/raw/master/doc/flow_chart.png)

#### Initiate a transaction

When you use nebpay api to initiate a transaction, such as
```javascript
serialNumber = nebPay.pay(
    to = "n1H2Yb5Q6ZfKvs61htVSV4b1U2gr2GA9vo6", 
    value = 1, //nas
    options = {
                qrcode: {
                    showQRCode: true
                },
                extension: {
                    openExtension:  true //set if need show extension payment mode
                },
                gasPrice: 1000000 ,
                gasLimit: 20000,
                listener: listener,  //set listener for extension transaction result
                callback: NebPay.config.mainnetUrl
            });
```
#### The process of Nebpay

If it's on mobile device, Nebpay will try to open NasNano by reload page with the link below:

```
openapp.NASnano://virtual?params={"category":"jump","des":"confirmTransfer","pageParams":{"serialNumber":"WljZsanTbHKAeMqOGxqq8nqOlBys8COB","goods":{"name":"test","desc":"test goods"},"pay":{"currency":"NAS","to":"n1H2Yb5Q6ZfKvs61htVSV4b1U2gr2GA9vo6","value":"1000000000000000000","payload":{"type":"binary"},"gasLimit":"20000","gasPrice":"1000000"},"callback":"https://pay.nebulas.io/api/mainnet/pay"}}
```

If it's on PC browser(Chrome), NebPay will try to send the transaction data to extension by `postMessage`, the data for this message is :
```json
{
	"src": "nebPay",
	"logo": "nebulas",
	"params": {
		"serialNumber": "9QoC4vRT29d5qnjXcSMgbPqSY7fOhW82",
		"goods": {
			"name": "test",
			"desc": "test goods"
		},
		"pay": {
			"currency": "NAS",
			"to": "n1H2Yb5Q6ZfKvs61htVSV4b1U2gr2GA9vo6",
			"value": "1000000000000000000",
			"payload": {
				"type": "binary"
			},
			"gasLimit": "20000",
			"gasPrice": "1000000"
		},
		"callback": "https://pay.nebulas.io/api/mainnet/pay"
	}
}
```
#### The process of NasNano

Then the NasNano or extension will send this transaction. After the transaction is successfully sent, NasNano or extension will post the `serialNumber` and `txhash` to transaction result query server, the URL of this server is given by `options.callback`. This is achieved by the http request below:
```
https://pay.nebulas.io/api/mainnet/pay?payId=9QoC4vRT29d5qnjXcSMgbPqSY7fOhW82&txHash=3f8767a15e7ad2bbebfc5bf15d97d206e56229757a9f3acae260b68ca4df1a2a
```

#### Query the transaction result
To check the transaction result, your should use `nebpay.quertPayInfo(serialNumber)` to query the transaction receipt data.

On NebPay side, it use the http-request below to query tx-result:
```
https://pay.nebulas.io/api/mainnet/pay/query?payId=9QoC4vRT29d5qnjXcSMgbPqSY7fOhW82 
```

After the transaction is successfully executed on block-chain, the queried tx-result will be like this:
```
{
	"code": 0,
	"data": {
		"execute_error": "",
		"gas_price": "1000000",
		"data": null,
		"gas_used": "20000",
		"contract_address": "",
		"type": "binary",
		"nonce": 46,
		"gas_limit": "20000",
		"chainId": 1001,
		"from": "n1H2Yb5Q6ZfKvs61htVSV4b1U2gr2GA9vo6",
		"to": "n1H2Yb5Q6ZfKvs61htVSV4b1U2gr2GA9vo6",
		"execute_result": "",
		"value": "1000000000000000000",
		"hash": "3f8767a15e7ad2bbebfc5bf15d97d206e56229757a9f3acae260b68ca4df1a2a",
		"status": 1,
		"timestamp": 1532005512
	},
	"msg": "success"
}
```

