## 如何在Dapp中使用NebPay SDK


### NebPay SDK介绍
NeyPay（https://github.com/nebulasio/nebPay）是官方发布的星云链支付工具，可以用来解决Dapp中的支付需求。

用户在使用Dapp过程中需要发送交易，但是直接在Dapp中导入钱包文件或输入私钥是极不安全的，所以Nebulas官方提供了一个支付接口NebPay。Dapp开发者可以使用NebPay作为支付通道，来处理sendTransaction的需求。Dapp用户需要安装浏览器插件（桌面端）或钱包APP（移动端）来完成Dapp页面发起的交易请求。

如果Dapp页面需要与Nebulas网络进行其他非交易类的信息交互，比如查询数据、订阅event等，则可以使用neb.js直接与Nebulas网络交互。

NebPay 根据不同的支付场景提供了4个支付API和1个交易查询API。关于接口的详细说明可以参考文档https://github.com/nebulasio/nebPay/blob/master/doc/NebPay%E4%BB%8B%E7%BB%8D.md。

- pay	用于账户间的NAS转账
- nrc20pay	用于NRC20代币的转账,仅接口实现，app不支持
- deploy	用于部署智能合约，仅接口实现
- call	用于调用智能合约
- queryPayInfo	用于查询支付结果

调用支付API时会返回一个交易序列号，然后Dapp可以使用查询API通过该序列号查询交易的结果。

### Dapp页面中使用 NebPay
如果在Dapp中使用NebPay，需要在github下载NebPay源码，然后打包生成`nebpay.js`。然后插入到Dapp页面就可以使用了。

示例代码如下：
```html
<script src="nebPay.js"></script>
<script >
    var NebPay = require("nebpay");
    var nebPay = new NebPay();    
    var serialNumber; //交易序列号
    var intervalQuery; //定时查询交易结果
    
    //点击按钮发起交易, 这里为调用智能合约的例子
    function onButtonClick() {
        
        var to = dappAddress;
        var value = "0";
        var callFunction = "" //调用的函数名称
        var callArgs =  "" //格式为参数数组的JSON字符串, 比如'["arg"]','["arg1","arg2]'        
        var options = {
            goods: {        //商品描述
                name: "example"
            },        
            listener: undefined //为浏览器插件指定listener,处理交易返回结果
        }
        
        //发送交易(发起智能合约调用)
        serialNumber = nebPay.call(to, value, callFunction, callArgs, options);
        
        //设置定时查询交易结果
        intervalQuery = setInterval(function() {
            funcIntervalQuery();
        }, 5000);
    }
    
    //查询交易结果
    function funcIntervalQuery() {   
        nebPay.queryPayInfo(serialNumber)   //search transaction result from server (result upload to server by app)
            .then(function (resp) {
                console.log("tx result: " + resp)   //resp is a JSON string
                var respObject = JSON.parse(resp)
                if(respObject.code === 0){
                    //交易成功, 处理相关任务
                    
                    clearInterval(intervalQuery)    //清除定时查询
                }
            })
            .catch(function (err) {
                console.log(err);
            });
    }
    
</script>
```

queryPayInfo(serialNumber) 查询到的结果格式为JSON字符串,可以反序列化`JSON.parse(resp)`得到JS对象。查询结果的格式为：
```
//查询失败, 没有该记录, 可以多查询几次
{
    "code": 1,
    "data": {},
    "msg": "payId ZBTSkk74dB4tPJI9J8FDFMu270h7yaut get transaction error"
}
//查询成功
{
    "code": 0,
    "data": {
        "data": null,
        "contractAddress": "",
        "type": "binary",
        "nonce": 136,
        "gasLimit": "30000",
        "gasUsed": "20000",
        "chainId": 1001,
        "from": "n1JmhE82GNjdZPNZr6dgUuSfzy2WRwmD9zy",
        "to": "n1JmhE82GNjdZPNZr6dgUuSfzy2WRwmD9zy",
        "value": "1000000000000000000",
        "hash": "f9549a5c01f50f372607b9fd29bf15d483246578f6cc7008d6e2a537920802e6",
        "gasPrice": "1000000",
        "status": 1,
        "timestamp": 1525508076
    },
    "msg": "success"
}
```

### NebPay 使用范例

这里有个使用nebPay的例子可以参考: SuperDictionary (http://39.105.36.104:8080/index.html)

SuperDictionary 在桌面端的使用过程为:
[视频1]

SuperDictionary 在手机端的使用过程为:
[视频2]