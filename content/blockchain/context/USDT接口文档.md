# USDT接口文档

[TOC]

>注：  USDT小数位数为6位  

## Account相关

### 1、创建账户

**接口名称：** 创建账户接口

**请求URL：** `/api/account/create`
  
**请求方式：** POST

**请求参数：**  

|参数名|类型|是否必填|说明|
|---|---|---|---|
|password |string |是|账户密码|

 **返回示例：**
``` 
{
    "status": "0",
    "data": "0x291e415db1694e9ab8e9e13e507d4603ddb9f644"
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0创建成功 1创建失败  |
|data   | 账户地址 |


### 2、导出keystore

**接口名称：** 导出keystore接口

**请求URL：** `/api/account/exportKey`
  
**请求方式：** POST

**请求参数：**  

|参数名|类型|是否必填|说明|  
|---|---|---|---|  
|address |string |是|账户地址|  
|password |string |是|账户密码|  

 **返回示例：**
``` 
{
    "status": "0",
    "data": "{\"address\":\"6e60f5243e1a3f0be3f407b5afe9e5395ee82aa2\",\"crypto\":{\"cipher\":\"aes-128-ctr\",\"ciphertext\":\"6187e29f5145ea1b60cdf2d9b9982c84a53a97a211ed592c0e456e8a896a3da5\",\"cipherparams\":{\"iv\":\"724ffa0a954397e86fb55c1e68d60d65\"},\"kdf\":\"scrypt\",\"kdfparams\":{\"dklen\":32,\"n\":262144,\"p\":1,\"r\":8,\"salt\":\"8baec709546cdbd2fcfcb47c8d25c0246a2afaec7edb99b47628ae8464d50a90\"},\"mac\":\"fe9036a49f096552aa96a766a027f94656c727f31dbd01e256d91bfab30adecf\"},\"id\":\"6740319d-4ecf-430d-9b31-892dccdc95ff\",\"version\":3}"
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0导出成功 1导出失败  |
|data   | 账户keystore |  


### 3、导入keystore

**接口名称：** 导入keystore接口

**请求URL：** `/api/account/importKeystore`
  
**请求方式：** POST

**请求参数：**  

|参数名|类型|是否必填|说明|  
|---|---|---|---|  
|keystore |string |是|账户keystore|  
|password |string |是|账户密码|  

 **返回示例：**
``` 
{
    "status": "0",
    "data": "0xb0236da2bdb3be51424a7bd42b4509289d002452"
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0导入成功 1导入失败  |
|data   | 账户地址 |

---

## BlockChain相关

### 1、获取区块链基础信息

**接口名称：** 获取区块链基础信息接口

**请求URL：** `/api/blockchain/info`
  
**请求方式：** GET

**请求参数：**  无

 **返回示例：**
``` 
{
    "status": "0",
    "data": {
        "blockNumber": "0x1163d0"
    }
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0获取成功 1获取失败  |
|blockNumber   | 当前最新的区块编号 |

### 2、根据区块号获取区块信息

**接口名称：** 根据区块号获取区块信息接口

**请求URL：** `/api/blockchain/blockByNumber`
  
**请求方式：** GET

**请求参数：**  
|参数名|类型|是否必填|说明|  
|---|---|---|  ---|
|number |string |是|区块号|  

 **返回示例：**
``` 
{
    "status": "0",
    "data": {
        "hash": "0x6f3b1d78e389a279b74a91155767f9b3dab73c44405befd10f8ee98ffd9cfe6b",
        "number": "0x84b8d",
        "miner": "0x3333333333333333333333333333333333333333",
        "parentHash": "0x6a029d394903b19ffd92cf15c8ccec05c83a28e4c9be95e5b49798a40606d21d",
        "timestamp": "0x5d19a067",
        "transactions": [
            {
                "blockHash": "0x6f3b1d78e389a279b74a91155767f9b3dab73c44405befd10f8ee98ffd9cfe6b",
                "blockNumber": "0x84b8d",
                "from": "0x88a8b91f4896cf8b9d887c6c2dae2e74f3210fa3",
                "to": "0x705bf45985e30b1fa06106517923b23c93b2f5e6",
                "gasLimit": "0x61a80",
                "gasPrice": "0x0",
                "gasUsed": "0x61a80",
                "hash": "0x0877463d44d0f86059dc05dce8d907611c750081e205a12ba2b30896f53c2bb5",
                "input": "0xa9059cbb00000000000000000000000088a8b91f4896cf8b9d887c6c2dae2e74f3210fa30000000000000000000000000000000000000000000000000000000000000020",
                "transactionIndex": "0x0",
                "value": "0x0",
                "events": [],
                "pending": false,
                "tradeSuccessful": false,
                "fee": "0"
            }
        ]
    }
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0成功 1失败  |
|hash   | 区块 hash |
|number | 区块编号 |
|miner | 矿工地址 |
|parentHash | 父区块 hash|
|timestamp | 区块时间戳|
|transactions | 本区块包含的交易（transaction 的字段解释参见 transactionByHash 接口的说明）

### 3、根据区块Hash获取区块信息

**接口名称：** 根据区块Hash获取区块信息接口

**请求URL：** `/api/blockchain/blockByHash`
  
**请求方式：** GET

**请求参数：**  
|参数名|类型|是否必填|说明|  
|---|---|---|---|  
|hash |string |是|区块哈希值|  

 **返回示例：**
``` 
{
    "status": "0",
    "data": {
        "hash": "0x6f3b1d78e389a279b74a91155767f9b3dab73c44405befd10f8ee98ffd9cfe6b",
        "number": "0x84b8d",
        "miner": "0x3333333333333333333333333333333333333333",
        "parentHash": "0x6a029d394903b19ffd92cf15c8ccec05c83a28e4c9be95e5b49798a40606d21d",
        "timestamp": "0x5d19a067",
        "transactions": [
            {
                "blockHash": "0x6f3b1d78e389a279b74a91155767f9b3dab73c44405befd10f8ee98ffd9cfe6b",
                "blockNumber": "0x84b8d",
                "from": "0x88a8b91f4896cf8b9d887c6c2dae2e74f3210fa3",
                "to": "0x705bf45985e30b1fa06106517923b23c93b2f5e6",
                "gasLimit": "0x61a80",
                "gasPrice": "0x0",
                "gasUsed": "0x61a80",
                "hash": "0x0877463d44d0f86059dc05dce8d907611c750081e205a12ba2b30896f53c2bb5",
                "input": "0xa9059cbb00000000000000000000000088a8b91f4896cf8b9d887c6c2dae2e74f3210fa30000000000000000000000000000000000000000000000000000000000000020",
                "transactionIndex": "0x0",
                "value": "0x0",
                "events": [],
                "pending": false,
                "tradeSuccessful": false,
                "fee": "0"
            }
        ]
    }
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0成功 1失败  |
|hash   | 区块 hash |
|number | 区块编号 |
|miner | 矿工地址 |
|parentHash | 父区块 hash|
|timestamp | 区块时间戳|
|transactions | 本区块包含的交易（transaction 的字段解释参见 transactionByHash 接口的说明）

### 4、根据交易Hash获取交易信息

**接口名称：** 根据交易 Hash 获取交易信息接口

**请求URL：** `/api/blockchain/transactionByHash`
  
**请求方式：** GET

**请求参数：**  
|参数名|类型|是否必填|说明|  
|---|---|---|---|  
|hash |string |是|交易哈希值|  

 **返回示例：**
``` 
{
    "status": "0",
    "data": {
        "blockHash": "0xacbc944a0cb78e9717df8ed149eae2752f2affad9d3516fdd5cf3a9c2c4bf656",
        "blockNumber": "0x116705",
        "from": "0x379fc1ef51eacd249dd171b56e7befa6d3fb1b34",
        "to": "0x176af2ef1a3aa37449def0a891f159fa76a02413",
        "gasLimit": "0x30d40",
        "gasPrice": "0x3b9aca08",
        "gasUsed": "0x957e",
        "hash": "0xff6a6daa530bf7761178781d28059f269619710931d9bf6eb71207404df1a2e4",
        "input": "0xa9059cbb00000000000000000000000072a601bf11ccbe43fd403aac24a0373997e6f45b0000000000000000000000000000000000000000000000000000000000000064",
        "transactionIndex": "0x0",
        "value": "0x0",
        "events": [
            {
                "topic": "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                "eventType": "Transfer",
                "args": "0x000000000000000000000000379fc1ef51eacd249dd171b56e7befa6d3fb1b34,0x00000000000000000000000072a601bf11ccbe43fd403aac24a0373997e6f45b,100"
            }
        ],
        "pending": false,
        "tradeSuccessful": true,
        "fee": "0.0000382700003062"
    }
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0成功 1失败  |
|blockHash| 交易所在区块的hash (交易未被区块收入时，blockHash = 0x0000000000000000000000000000000000000000000000000000000000000000)|
|blockNumber| 交易所在区块的编号（交易未被区块收入时，blockNumber = null）|
|from| 交易发起地址|
|to| 交易接收地址|
|gasLimit| 燃料数量限额|
|gasPrice| 燃料价格（单位为 10^(-18) Coin）|
|gasUsed| 实际使用燃料数量（交易未被区块收入时，gasUsed = 0）|
|hash| 交易 hash|
|input| input的code值|
|value| 转移金额（单位为 10^(-4) Coin）|
|events| 智能合约事件
|topic| 智能合约事件的原始 topic 值|
|eventType| 事件类型|
|args| 传入参数|
|pending| 是否在等待写入区块（true: 等待中；false：已经写入区块）|
|tradeSuccessful| 交易是否成功（true: 成功；false：失败）|
|fee| 手续费|

### 5、查询地址的余额

**接口名称：** 查询地址的余额接口

**请求URL：** `/api/blockchain/balance`
  
**请求方式：** GET

**请求参数：**  
|参数名|类型|是否必填|说明|  
|---|---|---|---| 
|address |string |是|账户地址|  
|blockNumber |string |否|指定区块编号，查询最新区块时，设为空| 

 **返回示例：**
``` 
{
    "status": "0",
    "data": "0x63"
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0成功 1失败  |
|data| 账户余额 |


---

## Transaction相关

### 1、转账

**接口名称：** 转账接口

**请求URL：** `/api/transaction/sendCoins`
  
**请求方式：** POST

**请求参数：**  
|参数名|类型|是否必填|说明|  
|---|---|---|---| 
|from |string |是|账户地址|  
|to|string | 是|收款人地址|
|password|string | 是|账户密码|
|value|string | 是|转账金额（单位为 10^(-6) Coin）|
|gas|string |是| 转账所花费 gas 数[40000-200000]|
|gasPrice|string| 是|Gas单价范围是[1gw-20gw] 其中1gw=1000000000| 

 **返回示例：**
``` 
{
    "status": "0",
    "data": "0xff6a6daa530bf7761178781d28059f269619710931d9bf6eb71207404df1a2e4"
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0转账事件触发成功 1转账事件触发失败  |
|data| 成功创建的交易 Hash |

---


## USDT相关
 * ### 1、获取账户USDT余额

**接口名称：** 获取账户余额接口

**请求URL：** `/api/usdt/balance`
  
**请求方式：** POST

**请求参数：**  

|参数名|类型|是否必填|说明|
|---|---|---|---|
|address |string |是|账户地址|

 **返回示例：**
``` 
{
    "status": "0",
    "data": 1000000
}
```
 **返回值说明：** 
 
|字段名|说明|
|---|---|
|status |0提交成功 1提交失败  |
|data   | 账户目前的USDT余额 |

---


* ### 2、USDT转账

**接口名称：** USDT转账接口

**请求URL：** `/api/usdt/transfer`
  
**请求方式：** POST

**请求参数：**  

|参数名|类型|是否必填|说明|
|---|---|---|---|
|from |string |是|账户地址|
|to |string |是|转入方账户地址|
|password |string |是|账户密码|
|value |string |是|转账金额（正整数）|
|gas |string |是|愿意支付的最大Gas范围是[40000-200000]|
|gasPrice |string |是|Gas单价范围是[1gw-20gw] 其中1gw=1000000000|

 **返回示例：**
``` 
{
    "status": "0",
    "data": "0xba957541ae23cfd4919312da98342ddaff07e9988070337e728e555012bd85f5"
}
```
 **返回值说明：**   
 
|字段名|说明|
|---|---|
|status |0提交成功 1提交失败  |
|data   | 交易hash |  

