## JSON-RPC methods
* [系统类](#系统类)
    * [getwalletinfo/查看系统信息](#getwalletinfo)
    * [omni_getinfo/返回节点和协议的各种状态信息](#omni_getinfo)
    * [getblockchaininfo/查看区块统信息](#getblockchaininfo)
    * [generate/手动挖矿](#generate)
    * [getblockhash/获取指定高度区块的哈希](#getblockhash)
    * [getblockcount/获取最新区块高度](#getblockcount)
    * [getblock/获取指定哈希的区块息](#getblock)
    * [keypoolrefill/预填充密钥池](#keypoolrefill)
* [账户类](#账户类)
    * [✔getnewaddress/为指定账户下创建地址](#getnewaddress)
    * [getbalance/查询余额](#getbalance)
    * [listunspent/返回归属于本钱包的未消费交易输出数组](#listunspent)
    * [✔listaccounts/列出账户列表](#listaccounts)
    * [✔getaddressesbyaccount/根据账户获取地址](#getaddressesbyaccount)
    * [getaccountaddress/获取指定账户的当前收款地址](#getaccountaddress)
    * [getaccount/根据地址取账户](#getaccount)
    * [dumpprivkey/导出指定地址私钥](#dumpprivkey)
    * [importprivkey/导入地址私钥](#importprivkey)
    * [dumpwallet/导出钱包文件为文本](#dumpwallet)
    * [importprivkey/导入地址私钥](#importprivkey)
    * [listaddressgroupings/按地址分组查询余额](#listaddressgroupings)
* [交易类](#交易类)
    * [sendtoaddress/从钱包给指定地址转比特币](#sendtoaddress)
    * [sendfrom/从指定账户发送比特币](#sendfrom)
    * [getrawtransaction/查询指定裸交易](#getrawtransaction)
    * [decoderawtransaction/解码交易内容](#decoderawtransaction)
    * [listreceivedbyaddress/查看所有账户下地址收到的比特币交易列表](#listreceivedbyaddress)
    * [gettransaction/获取指定BTC交易的详细信息](#gettransaction)
    * [listtransactions/查询最近发生的钱包交易](#listtransactions)
* [代币类](#代币类)
    * [omni_listproperties/查看当前所有代币](#omni_listproperties)
    * [omni_sendissuancemanaged/创建一个具有可调节供应量的新代币](#omni_sendissuancemanaged)
    * [omni_sendgrant/为代币充值](#omni_sendgrant)
    * [omni_getallbalancesforid/返回指定现金或资产的代币余额](#omni_getallbalancesforid)
    * [omni_getallbalancesforaddress/查看指定地址的所有代币余额](#omni_getallbalancesforaddress)
    * [✔omni_getbalance/返回指定地址和资产的代币余额](#omni_getbalance)
    * [✔omni_send/从钱包给指定地址转代币](#omni_send)
    * [omni_gettransaction/获取指定Omni交易的详细信息](#omni_gettransaction)
    * [✔omni_listtransactions/返回钱包代币交易清单，可以使用地址或区块进行过滤](#omni_listtransactions)
    
#### 系统类
#### getwalletinfo
```
#  获取钱包信息
omnicore-cli -rpcuser=admin -rpcpassword=123456 getwalletinfo
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getwalletinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### omni_getinfo
```
# 返回节点和协议的各种状态信息
omnicore-cli -rpcuser=admin -rpcpassword=123456 omni_getinfo
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_getinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### getblockchaininfo
```
# 查看区块统信息
omnicore-cli --datadir=./regtest/ -rpcuser=admin -rpcpassword=123456 getblockchaininfo
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockchaininfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### generate
```
# 手动挖矿
omnicore-cli -rpcuser=admin -rpcpassword=123456  generate 5
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "generate", "params": [5] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### getblockhash
```
# 获取指定高度区块的哈希
omnicore-cli -rpcuser=admin -rpcpassword=123456 getblockhash 88
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockhash", "params": [88] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### getblockcount
```
# 获取最新区块高度
omnicore-cli -rpcuser=admin -rpcpassword=123456  getblockcount
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### getblock
```
# 获取指定哈希的区块
omnicore-cli  -rpcuser=admin -rpcpassword=123456 getblock 6b97bed174fa25b7dd0a341d22c9e9f3f74e65747451c711fbd5d2f6d44d232d
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblock", "params": ["7bdfe7cb580ebe60c81d67a364fa8cf5ef3a06cdb18fca780957db0abd997413"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

#### keypoolrefill
```
# 预填充密钥池
#参数信息如下：
# KeyPoolSize：密钥池的大小，可选，默认值：100
omnicore-cli -rpcuser=admin -rpcpassword=123456  keypoolrefill 300
curl --user admin:mL5HoOV34k1r --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "keypoolrefill", "params": [300] }' -H 'content-type: text/plain;' http://172.31.56.169:9332/
```

#### 账户类
#### getnewaddress
```
# 为指定账户下创建地址
omnicore-cli -rpcuser=admin -rpcpassword=123456  getnewaddress account
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnewaddress", "params": ["account"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### getbalance
```
# 查询余额
omnicore-cli -rpcuser=admin -rpcpassword=123456  getbalance
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbalance", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbalance", "params": ["account"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### listunspent
```
# 返回归属于本钱包的未消费交易输出数组
# MinimumConfirmations：交易最少确认数，默认值：1
# MaximumConfirmations：交易最多确认数，默认值：9999999
# Addresses：交易输出中应当包含的地址数组
# 全部地址
omnicore-cli listunspent 6 9999999
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [6, 9999999] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
# 某个地址
omnicore-cli listunspent 6 9999999 "[\"19F5iAAAAAA3TEzYp24uQuwsJHaLBc7oL\"]"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [6, 9999999,["19F5iAAAAAA3TEzYp24uQuwsJHaLBc7oL"]] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
# 多个地址
omnicore-cli listunspent 6 9999999 "[\"19F5iAAAAAA3TEzYp24uQuwsJHaLBc7oL\",\"1GJBBBBBBqUX1nf5tDFQfvGbZwJ5r4J28X\"]"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [6, 9999999,["19F5iAAAAAA3TEzYp24uQuwsJHaLBc7oL","1GJBBBBBBqUX1nf5tDFQfvGbZwJ5r4J28X"]] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### listaccounts
```
# 列出账户列表
omnicore-cli -rpcuser=admin -rpcpassword=123456  listaccounts
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaccounts", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### getaddressesbyaccount
```
# 根据账户获取地址
omnicore-cli -rpcuser=admin -rpcpassword=123456  getaddressesbyaccount "account"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressesbyaccount", "params": ["account"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
##### getaccountaddress
```
# 获取指定账户的当前收款地址
omnicore-cli -rpcuser=admin -rpcpassword=123456  getaccountaddress "account"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccountaddress", "params": ["account"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### getaccount
```
# 根据地址取账户
omnicore-cli -rpcuser=admin -rpcpassword=123456  getaccount mxwc4jaoYNadmZGuFmfyiDH7V9mNyMziRF
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccount", "params": ["mxwc4jaoYNadmZGuFmfyiDH7V9mNyMziRF"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### dumpprivkey
```
# 导出指定地址私钥
omnicore-cli -rpcuser=admin -rpcpassword=123456 dumpprivkey "1CwsF2fJva1FRvn4RfwyeEaMpymAhtXMWi"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpprivkey", "params": ["mxwc4jaoYNadmZGuFmfyiDH7V9mNyMziRF"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### importprivkey
```
# 导入地址私钥
omnicore-cli -rpcuser=admin -rpcpassword=123456 importprivkey "cW1wuDBoDyxNicqN6Fg4YoYFYHzsw2q5sJbCDrurWueJuV7MNrHA" "lijie"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importprivkey", "params": ["cTGhZe1G3CphTnuJvySt9MuL3iEk5xkr9idBfQm9WraD9CKY9dg4","lijie",false] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### dumpwallet
```
# 导出钱包文件为文本
omnicore-cli -rpcuser=admin -rpcpassword=123456 dumpwallet /tmp/dump.txt
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpwallet", "params": ["/tmp/dump.txt"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### listaddressgroupings
```
# 按地址分组查询余额
omnicore-cli -rpcuser=admin -rpcpassword=123456 listaddressgroupings
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaddressgroupings", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

#### 交易类
#### sendtoaddress
```
# 从钱包给指定地址转比特币
omnicore-cli -rpcuser=admin -rpcpassword=123456 sendtoaddress "mhdFgoLdEpHxccGd1gBCHXm4sx15kZNCyL" "10.0"
curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendtoaddress", "params": ["mpuD9MkpEe9yWbjeJBopBC66qgZQzteQ9U", 0.1] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### sendfrom
```
# 从指定账户发送比特币
omnicore-cli -rpcuser=admin -rpcpassword=123456 sendfrom "" "n1c8acjABypgQ7xRpLNkwnE5R5bingzN41" "10.0"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendfrom", "params": ["account","mpuD9MkpEe9yWbjeJBopBC66qgZQzteQ9U","10"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### getrawtransaction
```
# 查询指定裸交易
omnicore-cli -rpcuser=admin -rpcpassword=123456 getrawtransaction 7aaeb8d03ea49a5138fa351e9e0313a31297e15b5f7ab3ce1f4dfe71edf1bc53
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawtransaction", "params": ["24f037750a412ba486ecb9bb5f030a35944dcb8263cc6a071ab717d19bc6dd0d"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### decoderawtransaction
```
omnicore-cli -rpcuser=admin -rpcpassword=123456 decoderawtransaction  0100000001598ac00e809d0829b2008b7c4fac09c95b477650f8041d84af2d02b86e8341270000000049483045022100bab5981918d76b920059cd24dfab93b0261f57d46501538078fde78a4960ee6c0220202fa1c0a9d93f15dee9c5bb7abbb487fedbc9085cd4c12083d6b0c82871f2d201feffffff0200ca9a3b000000001976a914172143fda161e37b5c1e749c0c6e3b1acb4a0c1f88ac80a3e60e000000001976a9144351a46d6afe9422fb7d43d12d2ec8660a5b774488ac03020000
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decoderawtransaction", "params": ["01000000026ef155d01a54b2eeba65951b54a2f5987939d8dce3d8ce941e1cde098f0ea287000000006a47304402206ed4a397dbe20dc6781465f61f19a3aca33985fb437abf23e5a3e3df6b0ee1330220546254bc47c4bbf3fedb8cec1d31fd94725f14078cc73160931d26b1c680003901210256fef8678338ca315d91d6d363a0261dbd2bc224502a5360654ab04d06b891fcfeffffffbbbd5b0dee2fce6fc7bb3f24d4bdc671f8925baa8035009a1b99ec9d4c50acec000000006a47304402206fef3bbb55d19411af5d121d4ad71ad809120c19b746d392fd21cbbfabcdd48f02200e92c3cbc8df7374b8fbc98846230a7f8e212a4977472758eaf85f6bb6ec9d4b012102d8fbd08ccb00d581d9a0ed898d526e9fe3f36f42839e8923efdccb82e7d7b9d8feffffff0200ca9a3b000000001976a91466eeadef8454a2750c20ab4248cb8c3334b9f6ee88ac72179800000000001976a9141adc4a980274d175e7a852baf3765b16053326e088ac7e020000"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### listreceivedbyaddress
```
# 查看所有账户下地址收到的比特币交易列表
omnicore-cli -rpcuser=admin -rpcpassword=123456 listreceivedbyaddress
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaddress", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### gettransaction
```
# 获取指定BTC交易的详细信息
omnicore-cli -rpcuser=admin -rpcpassword=123456 "gettransaction" d53d87868b814481499a4c8f2f083ee20da07d665e04edd237aa08b3aef6925e
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettransaction", "params": ["e33f95a026648e6a4cb1ae924c524f0e3772c52253b421050142eb2f1955c941"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
#### listtransactions
```
# 查询最近发生的钱包交易
# 参数信息如下：
# Account：钱包账户名
# Count：要提取的交易数量，默认值：10
# Skip：要跳过的交易数量，默认值：0
# IncludeWatchOnly：是否包含watch-only地址，默认值：false
omnicore-cli -rpcuser=admin -rpcpassword=123456  listtransactions "*" 500 0  
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listtransactions", "params": ["*",500,0] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

#### 代币类
##### omni_listproperties
```
# 查看当前所有代币
omnicore-cli -rpcuser=admin -rpcpassword=123456 omni_listproperties
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_listproperties", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

##### omni_sendissuancemanaged
```
# 创建一个具有可调节供应量的新代币
#参数信息如下：
# fromaddress：发送地址，字符串，必需
# ecosystem：生态系统代码，数值，1 - 主生态，2 - 测试生态，必需
# type：代币类型代码，数值，1 - 不可分 2 - 可分，必需
# previousid：前序代币ID，数值，0表示新代币，必需
# category：代币分类，字符串，可以为""，必需
# subcategory：代币子分类，字符串，可以为""，必需
# name：代币名称，字符串，必需
# url：代币网址，字符串，必需
# data：代币描述，字符串，必需
omnicore-cli -rpcuser=admin -rpcpassword=123456 omni_sendissuancemanaged n1c8acjABypgQ7xRpLNkwnE5R5bingzN41 2 2 0 "" "" "SEA" "" ""
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_sendissuancemanaged", "params": ["n1c8acjABypgQ7xRpLNkwnE5R5bingzN41", 2, 1, 0, "", "", "SEA", "", ""] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
##### omni_sendgrant
```
# 为代币充值
# fromaddress：发送地址，字符串，必需
# toaddress：目标地址，字符串，可以是""，必需
# propertyid：代币ID，数值，必需
# amount：代币数量，字符串，必需
# memo：交易附加文本备注，字符串，可选
omnicore-cli -rpcuser=admin -rpcpassword=123456 "omni_sendgrant" "n1c8acjABypgQ7xRpLNkwnE5R5bingzN41" "" 2147483651 "88888888"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_sendgrant", "params": ["n1c8acjABypgQ7xRpLNkwnE5R5bingzN41", "", 2147483651, "88888888"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
##### omni_getallbalancesforid
```
# 返回指定现金或资产的代币余额
omnicore-cli -rpcuser=admin -rpcpassword=123456 "omni_getallbalancesforid" 2147483651
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_getallbalancesforid", "params": [2147483651] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
##### omni_getallbalancesforaddress
```
# 查看指定地址的所有代币余额
omnicore-cli -rpcuser=admin -rpcpassword=123456 "omni_getallbalancesforaddress" "n1c8acjABypgQ7xRpLNkwnE5R5bingzN41"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_getallbalancesforaddress", "params": ["n1c8acjABypgQ7xRpLNkwnE5R5bingzN41"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
##### omni_getbalance
```
# 返回指定地址和资产的代币余额
omnicore-cli -rpcuser=admin -rpcpassword=123456 "omni_getbalance" "n1c8acjABypgQ7xRpLNkwnE5R5bingzN41" 2147483652 
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_getbalance", "params": ["n1c8acjABypgQ7xRpLNkwnE5R5bingzN41",2147483652] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
##### omni_send
```
# 从钱包给指定地址转代币
omnicore-cli -rpcuser=admin -rpcpassword=123456 "omni_send" "n1c8acjABypgQ7xRpLNkwnE5R5bingzN41" "mpPoCLZz72vBiq13MaRyYQE91ZSEEW1Ey7" 2147483651 "100.0"
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_send", "params": ["n1c8acjABypgQ7xRpLNkwnE5R5bingzN41", "mpPoCLZz72vBiq13MaRyYQE91ZSEEW1Ey7", 2147483651, "100.0"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
##### omni_gettransaction
```
# 获取指定Omni交易的详细信息
omnicore-cli -rpcuser=admin -rpcpassword=123456 "omni_gettransaction" e33f95a026648e6a4cb1ae924c524f0e3772c52253b421050142eb2f1955c941
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_gettransaction", "params": ["e33f95a026648e6a4cb1ae924c524f0e3772c52253b421050142eb2f1955c941"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
##### omni_listtransactions
```
# 返回钱包代币交易清单，可以使用地址或区块进行过滤
#参数信息如下：
# addfilt       string  可选    地址过滤 (default: "*")
# count         number  可选    最大数量(default: 10)
# skip          number  可选    跳过第n个事务 (default: 0)
# startblock    number  可选    起始的区块(default: 0)
# endblock      number  可选    最后的区块 (default: 999999)
omnicore-cli -rpcuser=admin -rpcpassword=123456  omni_listtransactions "*" 1000 
curl --user admin:123456 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "omni_listtransactions", "params": ["*",1000,0,730] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```


#### 正式环境 bitcoin.conf
```
#rpc接口的访问用户名
rpcuser=usdtrpc  
#rpc接口的访问用户密码
rpcpassword=fenHQ9oAy9fBWmlKVfZhwLM57TJ  
#是否启动JSON-RPC接口 0 - 不启动 1 - 启动
server=1  
#rpc访问白名单
rpcallowip=172.20.195.121  
#rpc接口的监听端口
rpcport=8332  
#监听 <端口> 上的连接  
port=8188
#所有交易进行索引；否则只保留钱包地址交易索引记录
txindex=1    
#设置允许传输的最小交易费用，可以减少交易内存池的使用
minrelaytxfee=0.00005  
#发送的交易每 KB 字节的手续费，类似gas price作用
paytxfee=0.00005  
# 最高交易手续费
maxtxfee=0.0001
```

#### 测试链环境 bitcoin.conf
```
testnet=1
server=1
rpcuser=admin
rpcpassword=123456
rpcallowip=0.0.0.0/0
rpcport=8332
port=8333
txindex=1
datacarriersize=80
logtimestamps=1
omnidebug=tally  
omnidebug=packets
omnidebug=pending
```

#### 私链环境 bitcoin.conf
```
# 0 - 否 1 - 是
regtest=1
#是否启动JSON-RPC接口 0 - 不启动 1 - 启动
server=1
#rpc接口的访问用户名
rpcuser=admin
#rpc接口的访问用户密码
rpcpassword=123456
#rpc访问白名单
rpcallowip=0.0.0.0/0
#rpc接口的监听端口
rpcport=8332
#监听 <端口> 上的连接
port=8333
#所有交易进行索引；否则只保留钱包地址交易索引记录
txindex=1
#嵌入在OP_RETURN脚本中的有效载荷的最大字节大小
datacarriersize=80
#调试信息前添加时间戳
logtimestamps=1
omnidebug=tally  
omnidebug=packets
omnidebug=pending
```
比特币并不是基于账户的方案，而是基于UTXO方案。这个和传统银行账户的思维完全不一样。张三拥有10个btc，其实就是当前区块链账本中，有若干笔交易的输出（UTXO）收款人都是张三的地址，而这些UXTO的总额为10。这个地址一共收了多少UTXO，则是要通过比特币钱包代为跟踪计算，所以钱包里显示的余额其实是有多少价值btc的输出指向你的地址。