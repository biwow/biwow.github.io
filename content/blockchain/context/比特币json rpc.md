# 比特币JSON RPC.md

## JSON-RPC methods
### Blockchain
- [getbestblockhash 获取最新的区块哈希值](#getbestblockhash)
- [getblock 获取指定区块信息](#getblock)
- [getblockchaininfo](#getblockchaininfo)
- [getblockcount](#getblockcount)
- [getblockhash](#getblockhash)
- [getblockheader](#getblockheader)
- [getblockstats](#getblockstats)
- [getchaintips](#getchaintips)
- [getchaintxstats](#getchaintxstats)
- [getdifficulty](#getchaintxstats)
- [getmempoolancestors](#getmempoolancestors)
- [getmempooldescendants](#getmempooldescendants)
- [getmempoolentry](#getmempoolentry)
- [getmempoolinfo](#getmempoolinfo)
- [getrawmempool](#getrawmempool)
- [gettxout](#gettxout)
- [gettxoutproof](#gettxoutproof)
- [gettxoutsetinfo](#gettxoutsetinfo)
- [preciousblock](#preciousblock)
- [pruneblockchain](#pruneblockchain)
- [savemempool](#savemempool)
- [verifychain](#verifychain)
- [verifytxoutproof](#verifytxoutproof)

### Control
- [getmemoryinfo](#getmemoryinfo)
- [help](#help)
- [logging](#logging)
- [stop](#stop)
- [uptime](#uptime)

### Generating
- [generate](#generate)
- [generatetoaddress](#generatetoaddress)

### Mining
- [getblocktemplate](#getblocktemplate)
- [getmininginfo](#getblocktemplate)
- [getnetworkhashps](#getnetworkhashps)
- [prioritisetransaction](#prioritisetransaction)
- [submitblock](#submitblock)

### Network
- [addnode](#addnode)
- [clearbanned](#clearbanned)
- [disconnectnode](#disconnectnode)
- [getaddednodeinfo](#getaddednodeinfo)
- [getconnectioncount](#getconnectioncount)
- [getnettotals](#getnettotals)
- [getnetworkinfo](#getnetworkinfo)
- [getpeerinfo](#getpeerinfo)
- [listbanned](#listbanned)
- [ping](#ping)
- [setban](#setban)
- [setnetworkactive](#setnetworkactive)

### Rawtransactions
- [combinerawtransaction](#combinerawtransaction)
- [createrawtransaction](#createrawtransaction)
- [decoderawtransaction](#decoderawtransaction)
- [decodescript](#decodescript)
- [fundrawtransaction](#fundrawtransaction)
- [getrawtransaction](#getrawtransaction)
- [sendrawtransaction](#sendrawtransaction)
- [signrawtransaction](#signrawtransaction)
- [signrawtransactionwithkey](#signrawtransactionwithkey)
- [testmempoolaccept](#testmempoolaccept)

### Util
- [createmultisig](#createmultisig)
- [estimatesmartfee](#estimatesmartfee)
- [signmessagewithprivkey](#signmessagewithprivkey)
- [validateaddress](#validateaddress)
- [verifymessage](#verifymessage)

### Wallet
- [abandontransaction](#abandontransaction)
- [abortrescan](#abortrescan)
- [addmultisigaddress](#addmultisigaddress)
- [backupwallet](#backupwallet)
- [bumpfee](#bumpfee)
- [createwallet](#createwallet)
- [dumpprivkey 导出私钥](#dumpprivkey)
- [dumpwallet](#dumpwallet)
- [encryptwallet](#encryptwallet)
- [getaccount](#getaccount)
- [getaccountaddress](#getaccountaddress)
- [getaddressbyaccount](#getaddressbyaccount)
- [getaddressesbylabel](#getaddressesbylabel)
- [getaddressinfo](#getaddressinfo)
- [getbalance 获取余额](#getbalance)
- [getnewaddress 创建新的地址，也是创建账号](#getnewaddress)
- [getrawchangeaddress](#getrawchangeaddress)
- [getreceivedbyaccount](#getreceivedbyaccount)
- [getreceivedbyaddress](#getreceivedbyaddress)
- [gettransaction 获取详细交易信息](#gettransaction)
- [getunconfirmedbalance](#getunconfirmedbalance)
- [getwalletinfo](#getwalletinfo)
- [importaddress](#importaddress)
- [importmulti](#importmulti)
- [importprivkey 导入私钥到指定账户](#importprivkey)
- [importprunedfunds](#importprunedfunds)
- [importpubkey](#importpubkey)
- [importwallet](#importwallet)
- [keypoolrefill](#keypoolrefill)
- [listaccounts](#listaccounts)
- [listaddressgroupings](#listaddressgroupings)
- [listlabels](#listlabels)
- [listlockunspent](#listlockunspent)
- [listreceivedbyaccount](#listreceivedbyaccount)
- [listreceivedbyaddress](#listreceivedbyaddress)
- [listsinceblock](#listsinceblock)
- [listtransactions](#listtransactions)
- [listunspent](#listunspent)
- [listwallets](#listwallets)
- [loadwallet](#loadwallet)
- [lockunspent](#lockunspent)
- [move](#move)
- [removeprunedfunds](#removeprunedfunds)
- [rescanblockchain](#rescanblockchain)
- [sendfrom 转账](#sendfrom)
- [sendmany](#sendmany)
- [sendtoaddress](#sendtoaddress)
- [setaccount](#setaccount)
- [sethdseed](#sethdseed)
- [settxfee](#settxfee)
- [signmessage](#signmessage)
- [signrawtransactionwithwallet](#signrawtransactionwithwallet)
- [unloadwallet](#unloadwallet)
- [walletlock](#walletlock)
- [walletpassphrase](#walletpassphrase)
- [walletpassphrasechange](#walletpassphrasechange)

## JSON RPC API Reference
### <span id="getbestblockhash">getbestblockhash</span>
Returns the header hash of the most recent block on the best block chain.
#### Parameters
none
#### Returns
```
"hex"      (string) the block hash hex encoded
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbestblockhash", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":"0000000000000000000621af297d27d54b501f6a3d329399c29cf316932973ef","error":null,"id":"curltest"}
```
### <span id="getblock">getblock</span>
gets a block with a particular header hash from the local block database either as a JSON object or as a serialized block.
#### Parameters
```
1. blockhash    (string, required) The block hash
2. verbosity    (numeric, optional, default=1) 0 for hex encoded data, 1 for a json object, and 2 for json object with transaction data
```
#### Returns
```
Result (for verbosity = 0):
"data"             (string) A string that is serialized, hex-encoded data for block 'hash'.

Result (for verbosity = 1):
{
  "hash" : "hash",     (string) the block hash (same as provided)
  "confirmations" : n,   (numeric) The number of confirmations, or -1 if the block is not on the main chain
  "size" : n,            (numeric) The block size
  "strippedsize" : n,    (numeric) The block size excluding witness data
  "weight" : n           (numeric) The block weight as defined in BIP 141
  "height" : n,          (numeric) The block height or index
  "version" : n,         (numeric) The block version
  "versionHex" : "00000000", (string) The block version formatted in hexadecimal
  "merkleroot" : "xxxx", (string) The merkle root
  "tx" : [               (array of string) The transaction ids
     "transactionid"     (string) The transaction id
     ,...
  ],
  "time" : ttt,          (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
  "mediantime" : ttt,    (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
  "nonce" : n,           (numeric) The nonce
  "bits" : "1d00ffff", (string) The bits
  "difficulty" : x.xxx,  (numeric) The difficulty
  "chainwork" : "xxxx",  (string) Expected number of hashes required to produce the chain up to this block (in hex)
  "previousblockhash" : "hash",  (string) The hash of the previous block
  "nextblockhash" : "hash"       (string) The hash of the next block
}

Result (for verbosity = 2):
{
  ...,                     Same output as verbosity = 1.
  "tx" : [               (array of Objects) The transactions in the format of the getrawtransaction RPC. Different from verbosity = 1 "tx" result.
         ,...
  ],
  ,...                     Same output as verbosity = 1.
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblock", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09", false] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":"010000007de867cc8adc5cc8fb6b898ca4462cf9fd667d7830a275277447e60800000000338f121232e169d3100edd82004dc2a1f0e1f030c6c488fa61eafa930b0528fe021f7449ffff001d36b4af9a0101000000010000000000000000000000000000000000000000000000000000000000000000ffffffff0804ffff001d02fd04ffffffff0100f2052a01000000434104f5eeb2b10c944c6b9fbcfff94c35bdeecd93df977882babc7f3a2cf7f5c81d3b09a68db7f0e04f21de5d4230e75e6dbe7ad16eefe0d4325a62067dc6f369446aac00000000","error":null,"id":"curltest"}
```
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblock", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{"hash":"00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09","confirmations":536934,"strippedsize":216,"size":216,"weight":864,"height":1000,"version":1,"versionHex":"00000001","merkleroot":"fe28050b93faea61fa88c4c630f0e1f0a1c24d0082dd0e10d369e13212128f33","tx":["fe28050b93faea61fa88c4c630f0e1f0a1c24d0082dd0e10d369e13212128f33"],"time":1232346882,"mediantime":1232344831,"nonce":2595206198,"bits":"1d00ffff","difficulty":1,"chainwork":"000000000000000000000000000000000000000000000000000003e903e903e9","previousblockhash":"0000000008e647742775a230787d66fdf92c46a48c896bfbc85cdc8acc67e87d","nextblockhash":"00000000a2887344f8db859e372e7e4bc26b23b9de340f725afbf2edb265b4c6"},"error":null,"id":"curltest"}
```
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblock", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09",2] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{"hash":"00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09","confirmations":536935,"strippedsize":216,"size":216,"weight":864,"height":1000,"version":1,"versionHex":"00000001","merkleroot":"fe28050b93faea61fa88c4c630f0e1f0a1c24d0082dd0e10d369e13212128f33","tx":[{"txid":"fe28050b93faea61fa88c4c630f0e1f0a1c24d0082dd0e10d369e13212128f33","hash":"fe28050b93faea61fa88c4c630f0e1f0a1c24d0082dd0e10d369e13212128f33","version":1,"size":135,"vsize":135,"locktime":0,"vin":[{"coinbase":"04ffff001d02fd04","sequence":4294967295}],"vout":[{"value":50.00000000,"n":0,"scriptPubKey":{"asm":"04f5eeb2b10c944c6b9fbcfff94c35bdeecd93df977882babc7f3a2cf7f5c81d3b09a68db7f0e04f21de5d4230e75e6dbe7ad16eefe0d4325a62067dc6f369446a OP_CHECKSIG","hex":"4104f5eeb2b10c944c6b9fbcfff94c35bdeecd93df977882babc7f3a2cf7f5c81d3b09a68db7f0e04f21de5d4230e75e6dbe7ad16eefe0d4325a62067dc6f369446aac","reqSigs":1,"type":"pubkey","addresses":["1BW18n7MfpU35q4MTBSk8pse3XzQF8XvzT"]}}],"hex":"01000000010000000000000000000000000000000000000000000000000000000000000000ffffffff0804ffff001d02fd04ffffffff0100f2052a01000000434104f5eeb2b10c944c6b9fbcfff94c35bdeecd93df977882babc7f3a2cf7f5c81d3b09a68db7f0e04f21de5d4230e75e6dbe7ad16eefe0d4325a62067dc6f369446aac00000000"}],"time":1232346882,"mediantime":1232344831,"nonce":2595206198,"bits":"1d00ffff","difficulty":1,"chainwork":"000000000000000000000000000000000000000000000000000003e903e903e9","previousblockhash":"0000000008e647742775a230787d66fdf92c46a48c896bfbc85cdc8acc67e87d","nextblockhash":"00000000a2887344f8db859e372e7e4bc26b23b9de340f725afbf2edb265b4c6"},"error":null,"id":"curltest"}
```
### <span id="getblockchaininfo">getblockchaininfo</span>
Returns an object containing various state info regarding blockchain processing.
#### Parameters
none
#### Returns
```
Result:
{
  "chain": "xxxx",              (string) current network name as defined in BIP70 (main, test, regtest)
  "blocks": xxxxxx,             (numeric) the current number of blocks processed in the server
  "headers": xxxxxx,            (numeric) the current number of headers we have validated
  "bestblockhash": "...",       (string) the hash of the currently best block
  "difficulty": xxxxxx,         (numeric) the current difficulty
  "mediantime": xxxxxx,         (numeric) median time for the current best block
  "verificationprogress": xxxx, (numeric) estimate of verification progress [0..1]
  "initialblockdownload": xxxx, (bool) (debug information) estimate of whether this node is in Initial Block Download mode.
  "chainwork": "xxxx"           (string) total amount of work in active chain, in hexadecimal
  "size_on_disk": xxxxxx,       (numeric) the estimated size of the block and undo files on disk
  "pruned": xx,                 (boolean) if the blocks are subject to pruning
  "pruneheight": xxxxxx,        (numeric) lowest-height complete block stored (only present if pruning is enabled)
  "automatic_pruning": xx,      (boolean) whether automatic pruning is enabled (only present if pruning is enabled)
  "prune_target_size": xxxxxx,  (numeric) the target size used by pruning (only present if automatic pruning is enabled)
  "softforks": [                (array) status of softforks in progress
     {
        "id": "xxxx",           (string) name of softfork
        "version": xx,          (numeric) block version
        "reject": {             (object) progress toward rejecting pre-softfork blocks
           "status": xx,        (boolean) true if threshold reached
        },
     }, ...
  ],
  "bip9_softforks": {           (object) status of BIP9 softforks in progress
     "xxxx" : {                 (string) name of the softfork
        "status": "xxxx",       (string) one of "defined", "started", "locked_in", "active", "failed"
        "bit": xx,              (numeric) the bit (0-28) in the block version field used to signal this softfork (only for "started" status)
        "startTime": xx,        (numeric) the minimum median time past of a block at which the bit gains its meaning
        "timeout": xx,          (numeric) the median time past of a block at which the deployment is considered failed if not yet locked in
        "since": xx,            (numeric) height of the first block to which the status applies
        "statistics": {         (object) numeric statistics about BIP9 signalling for a softfork (only for "started" status)
           "period": xx,        (numeric) the length in blocks of the BIP9 signalling period 
           "threshold": xx,     (numeric) the number of blocks with the version bit set required to activate the feature 
           "elapsed": xx,       (numeric) the number of blocks elapsed since the beginning of the current period 
           "count": xx,         (numeric) the number of blocks with the version bit set in the current period 
           "possible": xx       (boolean) returns false if there are not enough blocks left in this period to pass activation threshold 
        }
     }
  }
  "warnings" : "...",           (string) any network and blockchain warnings.
}
```
### <span id="getblockcount">getblockcount</span>
Returns the number of blocks in the longest blockchain.
#### Parameters
none
#### Returns
```
n    (numeric) The current block count
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":537941,"error":null,"id":"curltest"}
```

### <span id="getblockhash">getblockhash</span>
Returns hash of block in best-block-chain at height provided.
#### Parameters
```
1. height         (numeric, required) The height index
```
#### Returns
```
"hash"         (string) The block hash
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockhash", "params": [1000] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":"00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09","error":null,"id":"curltest"}
```

### <span id="getblockheader">getblockheader</span>
```
getblockheader "hash" ( verbose )

If verbose is false, returns a string that is serialized, hex-encoded data for blockheader 'hash'.
If verbose is true, returns an Object with information about blockheader <hash>.
```
#### Parameters
```
1. "hash"          (string, required) The block hash
2. verbose           (boolean, optional, default=true) true for a json object, false for the hex encoded data
```
#### Returns
```
Result (for verbose = true):
{
  "hash" : "hash",     (string) the block hash (same as provided)
  "confirmations" : n,   (numeric) The number of confirmations, or -1 if the block is not on the main chain
  "height" : n,          (numeric) The block height or index
  "version" : n,         (numeric) The block version
  "versionHex" : "00000000", (string) The block version formatted in hexadecimal
  "merkleroot" : "xxxx", (string) The merkle root
  "time" : ttt,          (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
  "mediantime" : ttt,    (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
  "nonce" : n,           (numeric) The nonce
  "bits" : "1d00ffff", (string) The bits
  "difficulty" : x.xxx,  (numeric) The difficulty
  "chainwork" : "0000...1f3"     (string) Expected number of hashes required to produce the current chain (in hex)
  "previousblockhash" : "hash",  (string) The hash of the previous block
  "nextblockhash" : "hash",      (string) The hash of the next block
}

Result (for verbose=false):
"data"             (string) A string that is serialized, hex-encoded data for block 'hash'.
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockheader", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09", false] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":"010000007de867cc8adc5cc8fb6b898ca4462cf9fd667d7830a275277447e60800000000338f121232e169d3100edd82004dc2a1f0e1f030c6c488fa61eafa930b0528fe021f7449ffff001d36b4af9a","error":null,"id":"curltest"}
```
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockheader", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09", true] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{"hash":"00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09","confirmations":536945,"height":1000,"version":1,"versionHex":"00000001","merkleroot":"fe28050b93faea61fa88c4c630f0e1f0a1c24d0082dd0e10d369e13212128f33","time":1232346882,"mediantime":1232344831,"nonce":2595206198,"bits":"1d00ffff","difficulty":1,"chainwork":"000000000000000000000000000000000000000000000000000003e903e903e9","previousblockhash":"0000000008e647742775a230787d66fdf92c46a48c896bfbc85cdc8acc67e87d","nextblockhash":"00000000a2887344f8db859e372e7e4bc26b23b9de340f725afbf2edb265b4c6"},"error":null,"id":"curltest"}
```

### <span id="getchaintips">getchaintips</span>
Return information about all known tips in the block tree, including the main chain as well as orphaned branches.
#### Parameters
none
#### Returns
```
Result:
[
  {
    "height": xxxx,         (numeric) height of the chain tip
    "hash": "xxxx",         (string) block hash of the tip
    "branchlen": 0          (numeric) zero for main chain
    "status": "active"      (string) "active" for the main chain
  },
  {
    "height": xxxx,
    "hash": "xxxx",
    "branchlen": 1          (numeric) length of branch connecting the tip to the main chain
    "status": "xxxx"        (string) status of the chain (active, valid-fork, valid-headers, headers-only, invalid)
  }
]
Possible values for status:
1.  "invalid"               This branch contains at least one invalid block
2.  "headers-only"          Not all blocks for this branch are available, but the headers are valid
3.  "valid-headers"         All blocks are available for this branch, but they were never fully validated
4.  "valid-fork"            This branch is not part of the active chain, but is fully validated
5.  "active"                This is the tip of the active main chain, which is certainly valid
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getchaintips", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":[{"height":537945,"hash":"00000000000000000013592c1375691fd458122fdd9f1c51cfd9c24cd2076539","branchlen":0,"status":"active"}],"error":null,"id":"curltest"}
```

### <span id="getchaintxstats">getchaintxstats</span>
Compute statistics about the total number and rate of transactions in the chain.
#### Parameters
```
1. nblocks      (numeric, optional) Size of the window in number of blocks (default: one month).
2. "blockhash"  (string, optional) The hash of the block that ends the window.
```
#### Returns
```
Result:
{
  "time": xxxxx,                (numeric) The timestamp for the final block in the window in UNIX format.
  "txcount": xxxxx,             (numeric) The total number of transactions in the chain up to that point.
  "window_block_count": xxxxx,  (numeric) Size of the window in number of blocks.
  "window_tx_count": xxxxx,     (numeric) The number of transactions in the window. Only returned if "window_block_count" is > 0.
  "window_interval": xxxxx,     (numeric) The elapsed time in the window in seconds. Only returned if "window_block_count" is > 0.
  "txrate": x.xx,               (numeric) The average rate of transactions per second in the window. Only returned if "window_interval" is > 0.
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getchaintxstats", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{"time":1534986545,"txcount":336571193,"window_block_count":4320,"window_tx_count":6026063,"window_interval":2408756,"txrate":2.501732429519636},"error":null,"id":"curltest"}
```

### <span id="getdifficulty">getdifficulty</span>
Returns the proof-of-work difficulty as a multiple of the minimum difficulty.
#### Parameters
none
#### Returns
```
Result:
n.nnn       (numeric) the proof-of-work difficulty as a multiple of the minimum difficulty.
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getdifficulty", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":6727225469722.534,"error":null,"id":"curltest"}
```

### <span id="getmempoolancestors">getmempoolancestors</span>
If txid is in the mempool, returns all in-mempool ancestors.
#### Parameters
```
Arguments:
1. "txid"                 (string, required) The transaction id (must be in mempool)
2. verbose                  (boolean, optional, default=false) True for a json object, false for array of transaction ids
```
#### Returns
```
Result (for verbose=false):
[                       (json array of strings)
  "transactionid"           (string) The transaction id of an in-mempool ancestor transaction
  ,...
]

Result (for verbose=true):
{                           (json object)
  "transactionid" : {       (json object)
    "size" : n,             (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
    "fee" : n,              (numeric) transaction fee in BTC
    "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
    "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
    "height" : n,           (numeric) block height when transaction entered pool
    "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
    "descendantsize" : n,   (numeric) virtual transaction size of in-mempool descendants (including this one)
    "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
    "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
    "ancestorsize" : n,     (numeric) virtual transaction size of in-mempool ancestors (including this one)
    "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one)
    "wtxid" : hash,         (string) hash of serialized transaction, including witness data
    "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
        "transactionid",    (string) parent transaction id
       ... ]
  }, ...
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolancestors", "params": ["52273e0ce6cf3452932cfbc1c517c0ce1af1d255fda67a6e3bd63ba1d908c8c2"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":["b104586f229e330caf42c475fd52684e9eb5e2d02f0fcd216d9554c5347b0873",
"094f7dcbc7494510d4daeceb2941ed73b1bd011bf527f6c3b7c897fee85c11d4"
],"error":null,"id":"curltest"}
```
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolancestors", "params": ["52273e0ce6cf3452932cfbc1c517c0ce1af1d255fda67a6e3bd63ba1d908c8c2", true] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{
  "b104586f229e330caf42c475fd52684e9eb5e2d02f0fcd216d9554c5347b0873": {
    "size": 485,
    "fee": 0.00009700,
    "modifiedfee": 0.00009700,
    "time": 1479423635,
    "height": 439431,
    "startingpriority": 15327081.81818182,
    "currentpriority": 21536936.36363636,
    "descendantcount": 1,
    "descendantsize": 485,
    "descendantfees": 9700,
    "ancestorcount": 1,
    "ancestorsize": 485,
    "ancestorfees": 9700,
    "depends": [
    ]
  },
  "094f7dcbc7494510d4daeceb2941ed73b1bd011bf527f6c3b7c897fee85c11d4": {
    "size": 554,
    "fee": 0.00005540,
    "modifiedfee": 0.00005540,
    "time": 1479423327,
    "height": 439430,
    "startingpriority": 85074.91071428571,
    "currentpriority": 3497174.4375,
    "descendantcount": 1,
    "descendantsize": 554,
    "descendantfees": 5540,
    "ancestorcount": 1,
    "ancestorsize": 554,
    "ancestorfees": 5540,
    "depends": [
    ]
  }
},"error":null,"id":"curltest"}
```
### <span id="getmempooldescendants">getmempooldescendants</span>
If txid is in the mempool, returns all in-mempool descendants.
#### Parameters
```
Arguments:
1. "txid"                 (string, required) The transaction id (must be in mempool)
2. verbose                  (boolean, optional, default=false) True for a json object, false for array of transaction ids
```
#### Returns
```
Result (for verbose=false):
[                       (json array of strings)
  "transactionid"           (string) The transaction id of an in-mempool descendant transaction
  ,...
]

Result (for verbose=true):
{                           (json object)
  "transactionid" : {       (json object)
    "size" : n,             (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
    "fee" : n,              (numeric) transaction fee in BTC
    "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
    "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
    "height" : n,           (numeric) block height when transaction entered pool
    "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
    "descendantsize" : n,   (numeric) virtual transaction size of in-mempool descendants (including this one)
    "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
    "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
    "ancestorsize" : n,     (numeric) virtual transaction size of in-mempool ancestors (including this one)
    "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one)
    "wtxid" : hash,         (string) hash of serialized transaction, including witness data
    "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
        "transactionid",    (string) parent transaction id
       ... ]
  }, ...
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempooldescendants", "params": ["52273e0ce6cf3452932cfbc1c517c0ce1af1d255fda67a6e3bd63ba1d908c8c2"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":[
    "b104586f229e330caf42c475fd52684e9eb5e2d02f0fcd216d9554c5347b0873",
    "094f7dcbc7494510d4daeceb2941ed73b1bd011bf527f6c3b7c897fee85c11d4"
],"error":null,"id":"curltest"}
```
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempooldescendants", "params": ["52273e0ce6cf3452932cfbc1c517c0ce1af1d255fda67a6e3bd63ba1d908c8c2", true] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{
  "b104586f229e330caf42c475fd52684e9eb5e2d02f0fcd216d9554c5347b0873": {
    "size": 485,
    "fee": 0.00009700,
    "modifiedfee": 0.00009700,
    "time": 1479423635,
    "height": 439431,
    "startingpriority": 15327081.81818182,
    "currentpriority": 21536936.36363636,
    "descendantcount": 1,
    "descendantsize": 485,
    "descendantfees": 9700,
    "ancestorcount": 1,
    "ancestorsize": 485,
    "ancestorfees": 9700,
    "depends": [
    ]
  },
  "094f7dcbc7494510d4daeceb2941ed73b1bd011bf527f6c3b7c897fee85c11d4": {
    "size": 554,
    "fee": 0.00005540,
    "modifiedfee": 0.00005540,
    "time": 1479423327,
    "height": 439430,
    "startingpriority": 85074.91071428571,
    "currentpriority": 3497174.4375,
    "descendantcount": 1,
    "descendantsize": 554,
    "descendantfees": 5540,
    "ancestorcount": 1,
    "ancestorsize": 554,
    "ancestorfees": 5540,
    "depends": [
    ]
  }
},"error":null,"id":"curltest"}
```
### <span id="getmempoolentry">getmempoolentry</span>
Returns mempool data for given transaction
#### Parameters
```
Arguments:
1. "txid"                   (string, required) The transaction id (must be in mempool)
```
#### Returns
```
Result:
{                           (json object)
    "size" : n,             (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
    "fee" : n,              (numeric) transaction fee in BTC
    "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
    "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
    "height" : n,           (numeric) block height when transaction entered pool
    "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
    "descendantsize" : n,   (numeric) virtual transaction size of in-mempool descendants (including this one)
    "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
    "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
    "ancestorsize" : n,     (numeric) virtual transaction size of in-mempool ancestors (including this one)
    "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one)
    "wtxid" : hash,         (string) hash of serialized transaction, including witness data
    "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
        "transactionid",    (string) parent transaction id
       ... ]
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolentry", "params": ["52273e0ce6cf3452932cfbc1c517c0ce1af1d255fda67a6e3bd63ba1d908c8c2"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{
    "size": 485,
    "fee": 0.00009700,
    "modifiedfee": 0.00009700,
    "time": 1479423635,
    "height": 439431,
    "startingpriority": 15327081.81818182,
    "currentpriority": 21536936.36363636,
    "descendantcount": 1,
    "descendantsize": 485,
    "descendantfees": 9700,
    "ancestorcount": 1,
    "ancestorsize": 485,
    "ancestorfees": 9700,
    "depends": [
    ]
},"error":null,"id":"curltest"}
```

### <span id="getmempoolinfo">getmempoolinfo</span>
Returns details on the active state of the TX memory pool.
#### Parameters
none
#### Returns
```
Result:
{
  "size": xxxxx,               (numeric) Current tx count
  "bytes": xxxxx,              (numeric) Sum of all virtual transaction sizes as defined in BIP 141. Differs from actual serialized size because witness data is discounted
  "usage": xxxxx,              (numeric) Total memory usage for the mempool
  "maxmempool": xxxxx,         (numeric) Maximum memory usage for the mempool
  "mempoolminfee": xxxxx       (numeric) Minimum fee rate in BTC/kB for tx to be accepted. Is the maximum of minrelaytxfee and minimum mempool fee
  "minrelaytxfee": xxxxx       (numeric) Current minimum relay fee for transactions
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolinfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{"size":1271,"bytes":586697,"usage":2021712,"maxmempool":300000000,"mempoolminfee":0.00001000,"minrelaytxfee":0.00001000},"error":null,"id":"curltest"}
```

### <span id="getrawmempool">getrawmempool</span>
Returns all transaction ids in memory pool as a json array of string transaction ids.
#### Parameters
```
Arguments:
1. verbose (boolean, optional, default=false) True for a json object, false for array of transaction ids
```
#### Returns
```
Result: (for verbose = false):
[                     (json array of string)
  "transactionid"     (string) The transaction id
  ,...
]

Result: (for verbose = true):
{                           (json object)
  "transactionid" : {       (json object)
    "size" : n,             (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
    "fee" : n,              (numeric) transaction fee in BTC
    "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
    "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
    "height" : n,           (numeric) block height when transaction entered pool
    "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
    "descendantsize" : n,   (numeric) virtual transaction size of in-mempool descendants (including this one)
    "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
    "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
    "ancestorsize" : n,     (numeric) virtual transaction size of in-mempool ancestors (including this one)
    "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one)
    "wtxid" : hash,         (string) hash of serialized transaction, including witness data
    "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
        "transactionid",    (string) parent transaction id
       ... ]
  }, ...
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawmempool", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":[
    "b104586f229e330caf42c475fd52684e9eb5e2d02f0fcd216d9554c5347b0873",
    "094f7dcbc7494510d4daeceb2941ed73b1bd011bf527f6c3b7c897fee85c11d4"
],"error":null,"id":"curltest"}
```
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawmempool", "params": [true] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{
  "b104586f229e330caf42c475fd52684e9eb5e2d02f0fcd216d9554c5347b0873": {
    "size": 485,
    "fee": 0.00009700,
    "modifiedfee": 0.00009700,
    "time": 1479423635,
    "height": 439431,
    "startingpriority": 15327081.81818182,
    "currentpriority": 21536936.36363636,
    "descendantcount": 1,
    "descendantsize": 485,
    "descendantfees": 9700,
    "ancestorcount": 1,
    "ancestorsize": 485,
    "ancestorfees": 9700,
    "depends": [
    ]
  },
  "094f7dcbc7494510d4daeceb2941ed73b1bd011bf527f6c3b7c897fee85c11d4": {
    "size": 554,
    "fee": 0.00005540,
    "modifiedfee": 0.00005540,
    "time": 1479423327,
    "height": 439430,
    "startingpriority": 85074.91071428571,
    "currentpriority": 3497174.4375,
    "descendantcount": 1,
    "descendantsize": 554,
    "descendantfees": 5540,
    "ancestorcount": 1,
    "ancestorsize": 554,
    "ancestorfees": 5540,
    "depends": [
    ]
  }
},"error":null,"id":"curltest"}
```

### <span id="gettxout">gettxout</span>
Returns details about an unspent transaction output.
#### Parameters
```
Arguments:
1. "txid"             (string, required) The transaction id
2. "n"                (numeric, required) vout number
3. "include_mempool"  (boolean, optional) Whether to include the mempool. Default: true.     Note that an unspent output that is spent in the mempool won't appear.
```
#### Returns
```
Result:
{
  "bestblock":  "hash",    (string) The hash of the block at the tip of the chain
  "confirmations" : n,       (numeric) The number of confirmations
  "value" : x.xxx,           (numeric) The transaction value in BTC
  "scriptPubKey" : {         (json object)
     "asm" : "code",       (string) 
     "hex" : "hex",        (string) 
     "reqSigs" : n,          (numeric) Number of required signatures
     "type" : "pubkeyhash", (string) The type, eg pubkeyhash
     "addresses" : [          (array of string) array of bitcoin addresses
        "address"     (string) bitcoin address
        ,...
     ]
  },
  "coinbase" : true|false   (boolean) Coinbase or not
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxout", "params": ["d77aee99e8bdc11f40b8a9354956f0346fec5535b82c77c8b5c06047e3bca86a", 0, true] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{
    "bestblock" : "00000000c92356f7030b1deeab54b3b02885711320b4c48523be9daa3e0ace5d",
    "confirmations" : 0,
    "value" : 0.00100000,
    "scriptPubKey" : {
        "asm" : "OP_DUP OP_HASH160 a11418d3c144876258ba02909514d90e71ad8443 OP_EQUALVERIFY OP_CHECKSIG",
        "hex" : "76a914a11418d3c144876258ba02909514d90e71ad844388ac",
        "reqSigs" : 1,
        "type" : "pubkeyhash",
        "addresses" : [
            "mvCfAJSKaoFXoJEvv8ssW7wxaqRPphQuSv"
        ]
    },
    "version" : 1,
    "coinbase" : false
},"error":null,"id":"curltest"}
```

### <span id="gettxoutsetinfo">gettxoutsetinfo</span>
Returns statistics about the unspent transaction output set.
#### Parameters
none
#### Returns
```
Result:
{
  "height":n,     (numeric) The current block height (index)
  "bestblock": "hex",   (string) The hash of the block at the tip of the chain
  "transactions": n,      (numeric) The number of transactions with unspent outputs
  "txouts": n,            (numeric) The number of unspent transaction outputs
  "bogosize": n,          (numeric) A meaningless metric for UTXO set size
  "hash_serialized_2": "hash", (string) The serialized hash
  "disk_size": n,         (numeric) The estimated size of the chainstate on disk
  "total_amount": x.xxx          (numeric) The total amount
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxoutsetinfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":{"height":539303,"bestblock":"000000000000000000216bee1a1561987bb39791f77299932acc85bf77224b1c","transactions":24407134,"txouts":49350207,"bogosize":3718816262,"hash_serialized_2":"cde9ec5e29dde60b49a06aeeb054ff28d933ce81637a40f9524419691be8ca56","disk_size":2841970027,"total_amount":17241117.33080327},"error":null,"id":"curltest"}
```

### <span id="pruneblockchain">pruneblockchain</span>
#### Parameters
```
Arguments:
1. "height"       (numeric, required) The block height to prune up to. May be set to a discrete height, or a unix timestamp
                  to prune blocks whose block time is at least 2 hours older than the provided timestamp.
```
#### Returns
```
Result:
n    (numeric) Height of the last block pruned.
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "pruneblockchain", "params": [1000] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":1000,"error":null,"id":"curltest"}
```

### <span id="savemempool">savemempool</span>
#### Parameters
none
#### Returns
none
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "savemempool", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="verifychain">verifychain</span>
Verifies blockchain database.
#### Parameters
```
Arguments:
1. checklevel   (numeric, optional, 0-4, default=3) How thorough the block verification is.
2. nblocks      (numeric, optional, default=6, 0=all) The number of blocks to check.
```
#### Returns
```
Result:
true|false       (boolean) Verified or not
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifychain", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/
//result
{"result":true,"error":null,"id":"curltest"}
```

### <span id="verifytxoutproof">verifytxoutproof</span>
Verifies that a proof points to a transaction in a block, returning the transaction it commits to and throwing an RPC error if the block is not in our best chain
#### Parameters
```
Arguments:
1. "proof"    (string, required) The hex-encoded proof generated by gettxoutproof
```
#### Returns
```
Result:
["txid"]      (array, strings) The txid(s) which the proof commits to, or empty array if the proof is invalid
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifytxoutproof", "params": ["03000000394ab3f08f712aa0f1d26c5daa4040b50e96d31d4e8e3c130000000000000000ca89aaa0bbbfcd5d1210c7888501431256135736817100d8c2cf7e4ab9c02b168115d45504dd1418836b20a6cb0800000d3a61beb3859abf1b773d54796c83b0b937968cc4ce3c0f71f981b2407a3241cb8908f2a88ac90a2844596e6019450f507e7efb8542cbe54ea55634c87bee474ee48aced68179564290d476e16cff01b483edcd2004d555c617dfc08200c08308ba511250e459b49d6a465e1ab1d5d8005e0778359c2993236c85ec66bac4bfd974131adc1ee0ad8b645f459164eb38325ac88f98c9607752bc1b637e16814f0d9d8c2775ac3f20f85260947929ceef16ead56fcbfd77d9dc6126cce1b5aacd9f834690f7508ee2db2ab67d382c5e738b1b6fe3fb079511952d33ec18c8440ef291eb8d3546a971ee4aa5e574b7be7f5aff0b1c989b2059ae5a611c8ce5c58e8e8476246c5e7c6b70e0065f2a6654e2e6cf4efb6ae19bf2548a7d9febf5b0aceaff28610922e1b9e23e52f650a4a11d2986c9c2b09bb168a70a7d4ac16e4d389bc2868ee91da1837d2cd79288bdc680e9c35ebb3ddfd045d69d767b164ec69d5db9f995c045d10af5bd90cd9d1116c3732e14796ef9d1a57fa7bb718c07989ed06ff359bf2009eaf1b9e000c054b87230567991b447757bc6ca8e1bb6e9816ad604dbd60600"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":["f20e44c818ec332d95119507fbe36f1b8b735e2c387db62adbe28e50f7904683"],"error":null,"id":"curltest"}
```

### <span id="getmemoryinfo">getmemoryinfo</span>
Returns an object containing information about memory usage.
#### Parameters
```
Arguments:
1. "mode" determines what kind of information is returned. This argument is optional, the default mode is "stats".
  - "stats" returns general statistics about memory usage in the daemon.
  - "mallocinfo" returns an XML string describing low-level heap state (only available if compiled with glibc 2.10+).
```
#### Returns
```
Result (mode "stats"):
{
  "locked": {               (json object) Information about locked memory manager
    "used": xxxxx,          (numeric) Number of bytes used
    "free": xxxxx,          (numeric) Number of bytes available in current arenas
    "total": xxxxxxx,       (numeric) Total number of bytes managed
    "locked": xxxxxx,       (numeric) Amount of bytes that succeeded locking. If this number is smaller than total, locking pages failed at some point and key data could be swapped to disk.
    "chunks_used": xxxxx,   (numeric) Number allocated chunks
    "chunks_free": xxxxx,   (numeric) Number unused chunks
  }
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmemoryinfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"locked":{"used":0,"free":65536,"total":65536,"locked":65536,"chunks_used":0,"chunks_free":1}},"error":null,"id":"curltest"}
```

### <span id="help">help</span>
List all commands, or get help for a specified command.
#### Parameters
```
Arguments:
Arguments:
1. "command"     (string, optional) The command to get help on
```
#### Returns
```
Result:
"text"     (string) The help text
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "help", "params": ["getblockcount"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"getblockcount\n\nReturns the number of blocks in the longest blockchain.\n\nResult:\nn    (numeric) The current block count\n\nExamples:\n> bitcoin-cli getblockcount \n> curl --user myusername --data-binary '{\"jsonrpc\": \"1.0\", \"id\":\"curltest\", \"method\": \"getblockcount\", \"params\": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/\n","error":null,"id":"curltest"}
```

### <span id="logging">logging</span>
Gets and sets the logging configuration.
#### Parameters
```
Arguments:
1. "include"        (array of strings, optional) A json array of categories to add debug logging
     [
       "category"   (string) the valid logging category
       ,...
     ]
2. "exclude"        (array of strings, optional) A json array of categories to remove debug logging
     [
       "category"   (string) the valid logging category
       ,...
     ]
```
#### Returns
```
Result:
{                   (json object where keys are the logging categories, and values indicates its status
  "category": 0|1,  (numeric) if being debug logged or not. 0:inactive, 1:active
  ...
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "logging", "params": [["all"], "[libevent]"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"net":1,"tor":1,"mempool":1,"http":1,"bench":1,"zmq":1,"db":1,"rpc":1,"estimatefee":1,"addrman":1,"selectcoins":1,"reindex":1,"cmpctblock":1,"rand":1,"prune":1,"proxy":1,"mempoolrej":1,"libevent":1,"coindb":1,"qt":1,"leveldb":1},"error":null,"id":"curltest"}
```

### <span id="stop">stop</span>
Stop Bitcoin server.
#### Parameters
```
none
```
#### Returns
```
none
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "stop", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"Bitcoin server stopping","error":null,"id":"curltest"}
```

### <span id="uptime">uptime</span>
Returns the total uptime of the server.
#### Parameters
```
none
```
#### Returns
```
Result:
ttt        (numeric) The number of seconds that the server has been running
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "uptime", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":134,"error":null,"id":"curltest"}
```

### <span id="generate">generate</span>
generate nblocks ( maxtries ).
#### Parameters
```
Arguments:
1. nblocks      (numeric, required) How many blocks are generated immediately.
2. maxtries     (numeric, optional) How many iterations to try (default = 1000000).
```
#### Returns
```
Result:
[ blockhashes ]     (array) hashes of blocks generated
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "generate", "params": [11] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":[],"error":null,"id":"curltest"}
```

### <span id="generatetoaddress">generatetoaddress</span>
generatetoaddress nblocks address (maxtries)
#### Parameters
```
Arguments:
1. nblocks      (numeric, required) How many blocks are generated immediately.
2. address      (string, required) The address to send the newly generated bitcoin to.
3. maxtries     (numeric, optional) How many iterations to try (default = 1000000).
```
#### Returns
```
Result:
[ blockhashes ]     (array) hashes of blocks generated
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "generatetoaddress", "params": [2, "1BRo7qrYHMPrzdBDzfjmzteBdYAyTMXW75", 50000] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":["36252b5852a5921bdfca8701f936b39edeb1f8c39fffe73b0d8437921401f9af",
    "5f2956817db1e386759aa5794285977c70596b39ea093b9eab0aa4ba8cd50c06"],"error":null,"id":"curltest"}
```

### <span id="getblocktemplate">getblocktemplate</span>
If the request parameters include a 'mode' key, that is used to explicitly select between the default 'template' request or a 'proposal'.
It returns data needed to construct a block to work on.
#### Parameters
```
Arguments:
1. template_request         (json object, optional) A json object in the following spec
     {
       "mode":"template"    (string, optional) This must be set to "template", "proposal" (see BIP 23), or omitted
       "capabilities":[     (array, optional) A list of strings
           "support"          (string) client side supported feature, 'longpoll', 'coinbasetxn', 'coinbasevalue', 'proposal', 'serverlist', 'workid'
           ,...
       ],
       "rules":[            (array, optional) A list of strings
           "support"          (string) client side supported softfork deployment
           ,...
       ]
     }
```
#### Returns
```
Result:
{
  "version" : n,                    (numeric) The preferred block version
  "rules" : [ "rulename", ... ],    (array of strings) specific block rules that are to be enforced
  "vbavailable" : {                 (json object) set of pending, supported versionbit (BIP 9) softfork deployments
      "rulename" : bitnumber          (numeric) identifies the bit number as indicating acceptance and readiness for the named softfork rule
      ,...
  },
  "vbrequired" : n,                 (numeric) bit mask of versionbits the server requires set in submissions
  "previousblockhash" : "xxxx",     (string) The hash of current highest block
  "transactions" : [                (array) contents of non-coinbase transactions that should be included in the next block
      {
         "data" : "xxxx",             (string) transaction data encoded in hexadecimal (byte-for-byte)
         "txid" : "xxxx",             (string) transaction id encoded in little-endian hexadecimal
         "hash" : "xxxx",             (string) hash encoded in little-endian hexadecimal (including witness data)
         "depends" : [                (array) array of numbers 
             n                          (numeric) transactions before this one (by 1-based index in 'transactions' list) that must be present in the final block if this one is
             ,...
         ],
         "fee": n,                    (numeric) difference in value between transaction inputs and outputs (in satoshis); for coinbase transactions, this is a negative Number of the total collected block fees (ie, not including the block subsidy); if key is not present, fee is unknown and clients MUST NOT assume there isn't one
         "sigops" : n,                (numeric) total SigOps cost, as counted for purposes of block limits; if key is not present, sigop cost is unknown and clients MUST NOT assume it is zero
         "weight" : n,                (numeric) total transaction weight, as counted for purposes of block limits
         "required" : true|false      (boolean) if provided and true, this transaction must be in the final block
      }
      ,...
  ],
  "coinbaseaux" : {                 (json object) data that should be included in the coinbase's scriptSig content
      "flags" : "xx"                  (string) key name is to be ignored, and value included in scriptSig
  },
  "coinbasevalue" : n,              (numeric) maximum allowable input to coinbase transaction, including the generation award and transaction fees (in satoshis)
  "coinbasetxn" : { ... },          (json object) information for coinbase transaction
  "target" : "xxxx",                (string) The hash target
  "mintime" : xxx,                  (numeric) The minimum timestamp appropriate for next block time in seconds since epoch (Jan 1 1970 GMT)
  "mutable" : [                     (array of string) list of ways the block template may be changed 
     "value"                          (string) A way the block template may be changed, e.g. 'time', 'transactions', 'prevblock'
     ,...
  ],
  "noncerange" : "00000000ffffffff",(string) A range of valid nonces
  "sigoplimit" : n,                 (numeric) limit of sigops in blocks
  "sizelimit" : n,                  (numeric) limit of block size
  "weightlimit" : n,                (numeric) limit of block weight
  "curtime" : ttt,                  (numeric) current timestamp in seconds since epoch (Jan 1 1970 GMT)
  "bits" : "xxxxxxxx",              (string) compressed target of next block
  "height" : n                      (numeric) The height of the next block
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblocktemplate", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
略
```

### <span id="getmininginfo">getmininginfo</span>
Returns a json object containing mining-related information.
#### Parameters
```
none
```
#### Returns
```
Result:
{
  "blocks": nnn,             (numeric) The current block
  "currentblockweight": nnn, (numeric) The last block weight
  "currentblocktx": nnn,     (numeric) The last block transaction
  "difficulty": xxx.xxxxx    (numeric) The current difficulty
  "networkhashps": nnn,      (numeric) The network hashes per second
  "pooledtx": n              (numeric) The size of the mempool
  "chain": "xxxx",           (string) current network name as defined in BIP70 (main, test, regtest)
  "warnings": "..."          (string) any network and blockchain warnings
  "errors": "..."            (string) DEPRECATED. Same as warnings. Only shown when bitcoind is started with -deprecatedrpc=getmininginfo
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmininginfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"blocks":539337,"currentblockweight":2377656,"currentblocktx":1158,"difficulty":6727225469722.534,"networkhashps":4.990843090877286e+19,"pooledtx":7226,"chain":"main","warnings":""},"error":null,"id":"curltest"}
```

### <span id="getnetworkhashps">getnetworkhashps</span>
Returns the estimated network hashes per second based on the last n blocks.
#### Parameters
```
Arguments:
1. nblocks     (numeric, optional, default=120) The number of blocks, or -1 for blocks since last difficulty change.
2. height      (numeric, optional, default=-1) To estimate at the time of the given height.
```
#### Returns
```
Result:
x             (numeric) Hashes per second estimated
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnetworkhashps", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":4.990843090877286e+19,"error":null,"id":"curltest"}
```

### <span id="prioritisetransaction">prioritisetransaction</span>
prioritisetransaction <txid> <dummy value> <fee delta>
Accepts the transaction into mined blocks at a higher (or lower) priority
#### Parameters
```
Arguments:
1. "txid"       (string, required) The transaction id.
2. dummy          (numeric, optional) API-Compatibility for previous API. Must be zero or null.
                  DEPRECATED. For forward compatibility use named arguments and omit this parameter.
3. fee_delta      (numeric, required) The fee value (in satoshis) to add (or subtract, if negative).
                  The fee is not actually paid, only the algorithm for selecting transactions into a block
                  considers the transaction as it would have paid a higher (or lower) fee.
```
#### Returns
```
Result:
true              (boolean) Returns true
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "prioritisetransaction", "params": ["fe0165147da737e16f5096ab6c1709825217377a95a882023ed089a89af4cff9", 0.0, 10000] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":true,"error":null,"id":"curltest"}
```

### <span id="submitblock">submitblock</span>
Attempts to submit new block to network.
#### Parameters
```
Arguments
1. "hexdata"        (string, required) the hex-encoded block data to submit
2. "dummy"          (optional) dummy value, for compatibility with BIP22. This value is ignored.
```
#### Returns
```
Result:
null或错误字符串
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "prioritisetransaction", "params": ["02000000df11c014a8d798395b5059c722ebdf3171a4217ead71bf6e0e99f4c7000000004a6f6a2db225c81e77773f6f0457bcb05865a94900ed11356d0b75228efb38c7785d6053ffff001d005d43700101000000010000000000000000000000000000000000000000000000000000000000000000ffffffff0d03b477030164062f503253482fffffffff0100f9029500000000232103adb7d8ef6b63de74313e0cd4e07670d09a169b13e4eda2d650f529332c47646dac00000000"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="addnode">addnode</span>
Attempts to add or remove a node from the addnode list.Or try a connection to a node once.
#### Parameters
```
Arguments:
1. "node"     (string, required) The node (see getpeerinfo for nodes)
2. "command"  (string, required) 'add' to add a node to the list, 'remove' to remove a node from the list, 'onetry' to try a connection to the node once
```
#### Returns
```
Result:
null
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "addnode", "params": ["192.168.0.6:8333", "onetry"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="clearbanned">clearbanned</span>
Clear all banned IPs.
#### Parameters
```
none
```
#### Returns
```
Result:
null
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "clearbanned", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="disconnectnode">disconnectnode</span>
Immediately disconnects from the specified peer node.
#### Parameters
```
Arguments:
1. "address"     (string, optional) The IP address/port of the node
2. "nodeid"      (number, optional) The node ID (see getpeerinfo for node IDs)
```
#### Returns
```
Result:
null
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "disconnectnode", "params": ["192.0.2.113:18333"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="getaddednodeinfo">getaddednodeinfo</span>
Returns information about the given added node, or all added nodes
#### Parameters
```
Arguments:
1. "node"   (string, optional) If provided, return information about this specific node, otherwise all nodes are returned.
```
#### Returns
```
Result:
[
  {
    "addednode" : "192.168.0.201",   (string) The node IP address or name (as provided to addnode)
    "connected" : true|false,          (boolean) If connected
    "addresses" : [                    (list of objects) Only when connected = true
       {
         "address" : "192.168.0.201:8333",  (string) The bitcoin server IP and port we're connected to
         "connected" : "outbound"           (string) connection, inbound or outbound
       }
     ]
  }
  ,...
]
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddednodeinfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="getaddednodeinfo">getaddednodeinfo</span>
Returns information about the given added node, or all added nodes(只有使用RPC手动添加的节点才会显示其信息)
#### Parameters
```
Arguments:
1. "node"   (string, optional) If provided, return information about this specific node, otherwise all nodes are returned.
```
#### Returns
```
Result:
[
  {
    "addednode" : "192.168.0.201",   (string) The node IP address or name (as provided to addnode)
    "connected" : true|false,          (boolean) If connected
    "addresses" : [                    (list of objects) Only when connected = true
       {
         "address" : "192.168.0.201:8333",  (string) The bitcoin server IP and port we're connected to
         "connected" : "outbound"           (string) connection, inbound or outbound
       }
     ]
  }
  ,...
]
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddednodeinfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="getconnectioncount">getconnectioncount</span>
Returns the number of connections to other nodes.
#### Parameters
```
Arguments:
none
```
#### Returns
```
Result:
n          (numeric) The connection count
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getconnectioncount", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":8,"error":null,"id":"curltest"}
```

### <span id="getnettotals">getnettotals</span>
Returns information about network traffic, including bytes in, bytes out,
and current time.
#### Parameters
```
Arguments:
none
```
#### Returns
```
Result:
{
  "totalbytesrecv": n,   (numeric) Total bytes received
  "totalbytessent": n,   (numeric) Total bytes sent
  "timemillis": t,       (numeric) Current UNIX time in milliseconds
  "uploadtarget":
  {
    "timeframe": n,                         (numeric) Length of the measuring timeframe in seconds
    "target": n,                            (numeric) Target in bytes
    "target_reached": true|false,           (boolean) True if target is reached
    "serve_historical_blocks": true|false,  (boolean) True if serving historical blocks
    "bytes_left_in_cycle": t,               (numeric) Bytes left in current time cycle
    "time_left_in_cycle": t                 (numeric) Seconds left in current time cycle
  }
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnettotals", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"totalbytesrecv":138332398,"totalbytessent":49705336,"timemillis":1535791780345,"uploadtarget":{"timeframe":86400,"target":0,"target_reached":false,"serve_historical_blocks":true,"bytes_left_in_cycle":0,"time_left_in_cycle":0}},"error":null,"id":"curltest"}
```

### <span id="getnetworkinfo">getnetworkinfo</span>
Returns an object containing various state info regarding P2P networking.
#### Parameters
```
Arguments:
none
```
#### Returns
```
Result:
{
  "version": xxxxx,                      (numeric) the server version
  "subversion": "/Satoshi:x.x.x/",     (string) the server subversion string
  "protocolversion": xxxxx,              (numeric) the protocol version
  "localservices": "xxxxxxxxxxxxxxxx", (string) the services we offer to the network
  "localrelay": true|false,              (bool) true if transaction relay is requested from peers
  "timeoffset": xxxxx,                   (numeric) the time offset
  "connections": xxxxx,                  (numeric) the number of connections
  "networkactive": true|false,           (bool) whether p2p networking is enabled
  "networks": [                          (array) information per network
  {
    "name": "xxx",                     (string) network (ipv4, ipv6 or onion)
    "limited": true|false,               (boolean) is the network limited using -onlynet?
    "reachable": true|false,             (boolean) is the network reachable?
    "proxy": "host:port"               (string) the proxy that is used for this network, or empty if none
    "proxy_randomize_credentials": true|false,  (string) Whether randomized credentials are used
  }
  ,...
  ],
  "relayfee": x.xxxxxxxx,                (numeric) minimum relay fee for transactions in BTC/kB
  "incrementalfee": x.xxxxxxxx,          (numeric) minimum fee increment for mempool limiting or BIP 125 replacement in BTC/kB
  "localaddresses": [                    (array) list of local addresses
  {
    "address": "xxxx",                 (string) network address
    "port": xxx,                         (numeric) network port
    "score": xxx                         (numeric) relative score
  }
  ,...
  ]
  "warnings": "..."                    (string) any network and blockchain warnings
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnetworkinfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"version":160100,"subversion":"/Satoshi:0.16.1/","protocolversion":70015,"localservices":"000000000000040d","localrelay":true,"timeoffset":0,"networkactive":true,"connections":8,"networks":[{"name":"ipv4","limited":false,"reachable":true,"proxy":"","proxy_randomize_credentials":false},{"name":"ipv6","limited":false,"reachable":true,"proxy":"","proxy_randomize_credentials":false},{"name":"onion","limited":true,"reachable":false,"proxy":"","proxy_randomize_credentials":false}],"relayfee":0.00001000,"incrementalfee":0.00001000,"localaddresses":[],"warnings":""},"error":null,"id":"curltest"}
```

### <span id="getpeerinfo">getpeerinfo</span>
Returns data about each connected network node as a json array of objects.
#### Parameters
```
Arguments:
none
```
#### Returns
```
Result:
[
  {
    "id": n,                   (numeric) Peer index
    "addr":"host:port",      (string) The IP address and port of the peer
    "addrbind":"ip:port",    (string) Bind address of the connection to the peer
    "addrlocal":"ip:port",   (string) Local address as reported by the peer
    "services":"xxxxxxxxxxxxxxxx",   (string) The services offered
    "relaytxes":true|false,    (boolean) Whether peer has asked us to relay transactions to it
    "lastsend": ttt,           (numeric) The time in seconds since epoch (Jan 1 1970 GMT) of the last send
    "lastrecv": ttt,           (numeric) The time in seconds since epoch (Jan 1 1970 GMT) of the last receive
    "bytessent": n,            (numeric) The total bytes sent
    "bytesrecv": n,            (numeric) The total bytes received
    "conntime": ttt,           (numeric) The connection time in seconds since epoch (Jan 1 1970 GMT)
    "timeoffset": ttt,         (numeric) The time offset in seconds
    "pingtime": n,             (numeric) ping time (if available)
    "minping": n,              (numeric) minimum observed ping time (if any at all)
    "pingwait": n,             (numeric) ping wait (if non-zero)
    "version": v,              (numeric) The peer version, such as 70001
    "subver": "/Satoshi:0.8.5/",  (string) The string version
    "inbound": true|false,     (boolean) Inbound (true) or Outbound (false)
    "addnode": true|false,     (boolean) Whether connection was due to addnode/-connect or if it was an automatic/inbound connection
    "startingheight": n,       (numeric) The starting height (block) of the peer
    "banscore": n,             (numeric) The ban score
    "synced_headers": n,       (numeric) The last header we have in common with this peer
    "synced_blocks": n,        (numeric) The last block we have in common with this peer
    "inflight": [
       n,                        (numeric) The heights of blocks we're currently asking from this peer
       ...
    ],
    "whitelisted": true|false, (boolean) Whether the peer is whitelisted
    "bytessent_per_msg": {
       "addr": n,              (numeric) The total bytes sent aggregated by message type
       ...
    },
    "bytesrecv_per_msg": {
       "addr": n,              (numeric) The total bytes received aggregated by message type
       ...
    }
  }
  ,...
]
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getpeerinfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":[{"id":0,"addr":"101.100.216.131:8333","addrlocal":"124.126.207.163:47242","addrbind":"10.20.11.27:55294","services":"000000000000000d","relaytxes":true,"lastsend":1535792016,"lastrecv":1535792013,"bytessent":6431834,"bytesrecv":17188873,"conntime":1535718830,"timeoffset":0,"pingtime":0.082279,"minping":0.081826,"version":70015,"subver":"/Satoshi:0.13.2/","inbound":false,"addnode":false,"startingheight":539332,"banscore":0,"synced_headers":539464,"synced_blocks":539464,"inflight":[],"whitelisted":false,"bytessent_per_msg":{"addr":41115,"cmpctblock":79695,"feefilter":32,"getaddr":24,"getdata":1048001,"getheaders":1053,"headers":13674,"inv":4764555,"notfound":3391,"ping":19520,"pong":19520,"reject":392,"sendcmpct":66,"sendheaders":24,"tx":440622,"verack":24,"version":126},"bytesrecv_per_msg":{"addr":53387,"getdata":51304,"getheaders":1053,"headers":2438,"inv":3243986,"notfound":61,"ping":19520,"pong":19520,"reject":241,"sendcmpct":264,"sendheaders":24,"tx":13796925,"verack":24,"version":126}},{"id":1,"addr":"46.4.100.141:8333","addrlocal":"124.126.199.29:13890","addrbind":"10.20.11.27:40744","services":"000000000000000d","relaytxes":true,"lastsend":1535792011,"lastrecv":1535792009,"bytessent":6142703,"bytesrecv":19439666,"conntime":1535718836,"timeoffset":-1,"pingtime":0.266462,"minping":0.168834,"version":70015,"subver":"/Satoshi:0.14.2/","inbound":false,"addnode":false,"startingheight":539332,"banscore":0,"synced_headers":539469,"synced_blocks":539469,"inflight":[],"whitelisted":false,"bytessent_per_msg":{"addr":39860,"feefilter":32,"getaddr":24,"getblocktxn":89,"getdata":1116824,"getheaders":1053,"headers":10494,"inv":4776948,"notfound":976,"ping":19488,"pong":19520,"reject":1091,"sendcmpct":132,"sendheaders":24,"tx":155998,"verack":24,"version":126},"bytesrecv_per_msg":{"addr":58197,"blocktxn":17218,"cmpctblock":194022,"feefilter":32,"getdata":20195,"getheaders":1053,"headers":13886,"inv":3461904,"notfound":122,"ping":19520,"pong":19488,"reject":159,"sendcmpct":66,"sendheaders":24,"tx":15633630,"verack":24,"version":126}},{"id":5,"addr":"39.107.14.236:8333","addrlocal":"124.126.199.29:13898","addrbind":"10.20.11.27:57372","services":"000000000000000d","relaytxes":true,"lastsend":1535792016,"lastrecv":1535792013,"bytessent":4709753,"bytesrecv":14446851,"conntime":1535718839,"timeoffset":0,"pingtime":0.004096,"minping":0.003346,"version":70015,"subver":"/Satoshi:0.15.1/","inbound":false,"addnode":false,"startingheight":539332,"banscore":0,"synced_headers":539468,"synced_blocks":539468,"inflight":[],"whitelisted":false,"bytessent_per_msg":{"addr":42085,"feefilter":32,"getaddr":24,"getblocktxn":60,"getdata":1017141,"getheaders":1053,"headers":8056,"inv":3483298,"notfound":12893,"ping":19520,"pong":19520,"reject":553,"sendcmpct":99,"sendheaders":24,"tx":105245,"verack":24,"version":126},"bytesrecv_per_msg":{"addr":46202,"blocktxn":361,"cmpctblock":492030,"feefilter":32,"getdata":28511,"getheaders":1053,"headers":318,"inv":2502475,"notfound":507,"ping":19520,"pong":19520,"reject":2997,"sendcmpct":66,"sendheaders":24,"tx":11333085,"verack":24,"version":126}},{"id":6,"addr":"174.112.70.224:8333","addrlocal":"124.126.199.29:13899","addrbind":"10.20.11.27:51260","services":"000000000000040d","relaytxes":true,"lastsend":1535792015,"lastrecv":1535792015,"bytessent":6765706,"bytesrecv":14583996,"conntime":1535718840,"timeoffset":-1,"pingtime":0.264539,"minping":0.251464,"version":70015,"subver":"/Satoshi:0.16.0/","inbound":false,"addnode":false,"startingheight":539332,"banscore":0,"synced_headers":539469,"synced_blocks":539469,"inflight":[],"whitelisted":false,"bytessent_per_msg":{"addr":41100,"feefilter":32,"getaddr":24,"getblocktxn":60,"getdata":898395,"getheaders":3159,"headers":11130,"inv":4890627,"notfound":8550,"ping":19520,"pong":19520,"reject":466,"sendcmpct":132,"sendheaders":24,"tx":872817,"verack":24,"version":126},"bytesrecv_per_msg":{"addr":60312,"blocktxn":777,"cmpctblock":207733,"feefilter":32,"getdata":96448,"getheaders":1053,"headers":11161,"inv":3142894,"notfound":280,"ping":19520,"pong":19520,"reject":155,"sendcmpct":66,"sendheaders":24,"tx":11023871,"verack":24,"version":126}},{"id":7,"addr":"218.75.158.183:8333","addrlocal":"124.126.207.163:47285","addrbind":"10.20.11.27:35682","services":"000000000000000d","relaytxes":true,"lastsend":1535792016,"lastrecv":1535792013,"bytessent":6714251,"bytesrecv":14592923,"conntime":1535718840,"timeoffset":0,"pingtime":0.038915,"minping":0.03848,"version":70015,"subver":"/Satoshi:0.15.1/","inbound":false,"addnode":false,"startingheight":539332,"banscore":0,"synced_headers":539469,"synced_blocks":539469,"inflight":[],"whitelisted":false,"bytessent_per_msg":{"addr":39700,"cmpctblock":19508,"feefilter":32,"getaddr":24,"getdata":963950,"getheaders":1053,"headers":7314,"inv":4799873,"notfound":6222,"ping":19520,"pong":19520,"reject":549,"sendcmpct":165,"sendheaders":24,"tx":836647,"verack":24,"version":126},"bytesrecv_per_msg":{"addr":59247,"cmpctblock":1007819,"feefilter":32,"getdata":103702,"getheaders":1053,"headers":742,"inv":3017439,"notfound":435,"ping":19520,"pong":19520,"reject":471,"sendcmpct":66,"sendheaders":24,"tx":10362703,"verack":24,"version":126}},{"id":8,"addr":"67.110.209.172:8333","addrlocal":"124.126.207.163:47353","addrbind":"10.20.11.27:45322","services":"000000000000040d","relaytxes":true,"lastsend":1535792016,"lastrecv":1535791998,"bytessent":6732098,"bytesrecv":12088641,"conntime":1535718853,"timeoffset":-1,"pingtime":0.191583,"minping":0.185982,"version":70015,"subver":"/Satoshi:0.16.1/","inbound":false,"addnode":false,"startingheight":539332,"banscore":0,"synced_headers":539469,"synced_blocks":539469,"inflight":[],"whitelisted":false,"bytessent_per_msg":{"addr":41030,"cmpctblock":32572,"feefilter":32,"getaddr":24,"getdata":795580,"getheaders":14742,"headers":13780,"inv":5046331,"notfound":3488,"ping":19520,"pong":19520,"reject":626,"sendcmpct":66,"sendheaders":24,"tx":744613,"verack":24,"version":126},"bytesrecv_per_msg":{"addr":64167,"cmpctblock":4079,"feefilter":32,"getdata":100249,"getheaders":1053,"headers":10256,"inv":2968007,"notfound":183,"ping":19520,"pong":19520,"reject":550,"sendcmpct":66,"sendheaders":24,"tx":8900785,"verack":24,"version":126}},{"id":9,"addr":"52.53.197.34:8333","addrlocal":"124.126.207.163:12036","addrbind":"10.20.11.27:58726","services":"000000000000000d","relaytxes":true,"lastsend":1535792014,"lastrecv":1535792016,"bytessent":6209457,"bytesrecv":20401697,"conntime":1535718854,"timeoffset":-5,"pingtime":0.158736,"minping":0.158589,"version":70015,"subver":"/Satoshi:0.13.2/","inbound":false,"addnode":false,"startingheight":539332,"banscore":0,"synced_headers":539468,"synced_blocks":539468,"inflight":[],"whitelisted":false,"bytessent_per_msg":{"addr":40410,"cmpctblock":48726,"feefilter":32,"getaddr":24,"getdata":1283902,"getheaders":33696,"headers":13886,"inv":4501999,"notfound":1378,"ping":19520,"pong":19520,"reject":387,"sendcmpct":66,"sendheaders":24,"tx":245737,"verack":24,"version":126},"bytesrecv_per_msg":{"addr":57327,"getdata":30808,"getheaders":1053,"headers":10490,"inv":3405181,"notfound":183,"ping":19520,"pong":19520,"reject":154,"sendcmpct":198,"sendheaders":24,"tx":16857089,"verack":24,"version":126}},{"id":73,"addr":"91.155.111.197:8333","addrlocal":"124.126.207.163:24328","addrbind":"10.20.11.27:35802","services":"000000000000040d","relaytxes":true,"lastsend":1535792018,"lastrecv":1535792018,"bytessent":744577,"bytesrecv":2478445,"conntime":1535781952,"timeoffset":-13,"pingtime":0.360199,"minping":0.293042,"version":70015,"subver":"/Satoshi:0.16.0/","inbound":false,"addnode":false,"startingheight":539451,"banscore":0,"synced_headers":539469,"synced_blocks":539469,"inflight":[],"whitelisted":false,"bytessent_per_msg":{"addr":4130,"feefilter":32,"getaddr":24,"getblocktxn":60,"getdata":138706,"getheaders":1053,"headers":1484,"inv":559231,"notfound":549,"ping":2688,"pong":2688,"reject":234,"sendcmpct":99,"sendheaders":24,"tx":33425,"verack":24,"version":126},"bytesrecv_per_msg":{"addr":37102,"blocktxn":270513,"cmpctblock":66230,"feefilter":32,"getdata":4888,"getheaders":1053,"headers":1484,"inv":407273,"ping":2688,"pong":2688,"sendcmpct":66,"sendheaders":24,"tx":1684254,"verack":24,"version":126}}],"error":null,"id":"curltest"}
```

### <span id="listbanned">listbanned</span>
List all banned IPs/Subnets.
#### Parameters
```
Arguments:
none
```
#### Returns
```
null
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listbanned", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="ping">ping</span>
Requests that a ping be sent to all other nodes, to measure ping time.
#### Parameters
```
Arguments:
none
```
#### Returns
```
null
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "ping", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="setban">setban</span>
Attempts to add or remove an IP/Subnet from the banned list.
#### Parameters
```
Arguments:
1. "subnet"       (string, required) The IP/Subnet (see getpeerinfo for nodes IP) with an optional netmask (default is /32 = single IP)
2. "command"      (string, required) 'add' to add an IP/Subnet to the list, 'remove' to remove an IP/Subnet from the list
3. "bantime"      (numeric, optional) time in seconds how long (or until when if [absolute] is set) the IP is banned (0 or empty means using the default time of 24h which can also be overwritten by the -bantime startup argument)
4. "absolute"     (boolean, optional) If set, the bantime must be an absolute timestamp in seconds since epoch (Jan 1 1970 GMT)
```
#### Returns
```
null
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setban", "params": ["192.168.0.6", "add", 86400] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="setnetworkactive">setnetworkactive</span>
Disable/enable all p2p network activity.
#### Parameters
```
Arguments:
1. "state"        (boolean, required) true to enable networking, false to disable
```
#### Returns
```
true/false
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setnetworkactive", "params": [true] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":true,"error":null,"id":"curltest"}
```

### <span id="combinerawtransaction">combinerawtransaction</span>
Combine multiple partially signed transactions into one transaction.
#### Parameters
```
Arguments:
1. "txs"         (string) A json array of hex strings of partially signed transactions
    [
      "hexstring"     (string) A transaction hash
      ,...
    ]
```
#### Returns
```
Result:
"hex"            (string) The hex-encoded raw transaction with signature(s)
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "combinerawtransaction", "params": ["myhex1", "myhex2", "myhex3"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"hex","error":null,"id":"curltest"}
```

### <span id="createrawtransaction">createrawtransaction</span>
Create a transaction spending the given inputs and creating new outputs.
Outputs can be addresses or data.
Returns hex-encoded raw transaction.
Note that the transaction's inputs are not signed, and
it is not stored in the wallet or transmitted to the network.
#### Parameters
```
Arguments:
1. "inputs"                (array, required) A json array of json objects
     [
       {
         "txid":"id",    (string, required) The transaction id
         "vout":n,         (numeric, required) The output number
         "sequence":n      (numeric, optional) The sequence number
       } 
       ,...
     ]
2. "outputs"               (object, required) a json object with outputs
    {
      "address": x.xxx,    (numeric or string, required) The key is the bitcoin address, the numeric value (can be string) is the BTC amount
      "data": "hex"      (string, required) The key is "data", the value is hex encoded data
      ,...
    }
3. locktime                  (numeric, optional, default=0) Raw locktime. Non-0 value also locktime-activates inputs
4. replaceable               (boolean, optional, default=false) Marks this transaction as BIP125 replaceable.
                             Allows this transaction to be replaced by a transaction with higher fees. If provided, it is an error if explicit sequence numbers are incompatible.
```
#### Returns
```
Result:
"transaction"              (string) hex string of the transaction
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": ["[{\"txid\":\"myid\",\"vout\":0}]", "{\"address\":0.01}"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"transaction","error":null,"id":"curltest"}
```

### <span id="decoderawtransaction">decoderawtransaction</span>
Return a JSON object representing the serialized, hex-encoded transaction.
#### Parameters
```
Arguments:
1. "hexstring"      (string, required) The transaction hex string
2. iswitness          (boolean, optional) Whether the transaction hex is a serialized witness transaction
                         If iswitness is not present, heuristic tests will be used in decoding
```
#### Returns
```
Result:
{
  "txid" : "id",        (string) The transaction id
  "hash" : "id",        (string) The transaction hash (differs from txid for witness transactions)
  "size" : n,             (numeric) The transaction size
  "vsize" : n,            (numeric) The virtual transaction size (differs from size for witness transactions)
  "version" : n,          (numeric) The version
  "locktime" : ttt,       (numeric) The lock time
  "vin" : [               (array of json objects)
     {
       "txid": "id",    (string) The transaction id
       "vout": n,         (numeric) The output number
       "scriptSig": {     (json object) The script
         "asm": "asm",  (string) asm
         "hex": "hex"   (string) hex
       },
       "txinwitness": ["hex", ...] (array of string) hex-encoded witness data (if any)
       "sequence": n     (numeric) The script sequence number
     }
     ,...
  ],
  "vout" : [             (array of json objects)
     {
       "value" : x.xxx,            (numeric) The value in BTC
       "n" : n,                    (numeric) index
       "scriptPubKey" : {          (json object)
         "asm" : "asm",          (string) the asm
         "hex" : "hex",          (string) the hex
         "reqSigs" : n,            (numeric) The required sigs
         "type" : "pubkeyhash",  (string) The type, eg 'pubkeyhash'
         "addresses" : [           (json array of string)
           "12tvKAXCxZjSmdNbao16dKXC8tRWfcF5oc"   (string) bitcoin address
           ,...
         ]
       }
     }
     ,...
  ],
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decoderawtransaction", "params": ["0100000001bafe2175b9d7b3041ebac529056b393cf2997f7964485aa382ffa449ffdac02a000000008a473044022013d212c22f0b46bb33106d148493b9a9723adb2c3dd3a3ebe3a9c9e3b95d8cb00220461661710202fbab550f973068af45c294667fc4dc526627a7463eb23ab39e9b01410479be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798483ada7726a3c4655da4fbfc0e1108a8fd17b448a68554199c47d08ffb10d4b8ffffffff01b0a86a00000000001976a91401b81d5fa1e55e069e3cc2db9c19e2e80358f30688ac00000000"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"txid":"52309405287e737cf412fc42883d65a392ab950869fae80b2a5f1e33326aca46","hash":"52309405287e737cf412fc42883d65a392ab950869fae80b2a5f1e33326aca46","version":1,"size":223,"vsize":223,"locktime":0,"vin":[{"txid":"2ac0daff49a4ff82a35a4864797f99f23c396b0529c5ba1e04b3d7b97521feba","vout":0,"scriptSig":{"asm":"3044022013d212c22f0b46bb33106d148493b9a9723adb2c3dd3a3ebe3a9c9e3b95d8cb00220461661710202fbab550f973068af45c294667fc4dc526627a7463eb23ab39e9b[ALL] 0479be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798483ada7726a3c4655da4fbfc0e1108a8fd17b448a68554199c47d08ffb10d4b8","hex":"473044022013d212c22f0b46bb33106d148493b9a9723adb2c3dd3a3ebe3a9c9e3b95d8cb00220461661710202fbab550f973068af45c294667fc4dc526627a7463eb23ab39e9b01410479be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798483ada7726a3c4655da4fbfc0e1108a8fd17b448a68554199c47d08ffb10d4b8"},"sequence":4294967295}],"vout":[{"value":0.06990000,"n":0,"scriptPubKey":{"asm":"OP_DUP OP_HASH160 01b81d5fa1e55e069e3cc2db9c19e2e80358f306 OP_EQUALVERIFY OP_CHECKSIG","hex":"76a91401b81d5fa1e55e069e3cc2db9c19e2e80358f30688ac","reqSigs":1,"type":"pubkeyhash","addresses":["1A6Ei5cRfDJ8jjhwxfzLJph8B9ZEthR9Z"]}}]},"error":null,"id":"curltest"}
```

### <span id="decodescript">decodescript</span>
Decode a hex-encoded script.
#### Parameters
```
Arguments:
1. "hexstring"     (string) the hex encoded script
```
#### Returns
```
Result:
{
  "asm":"asm",   (string) Script public key
  "hex":"hex",   (string) hex encoded public key
  "type":"type", (string) The output type
  "reqSigs": n,    (numeric) The required signatures
  "addresses": [   (json array of string)
     "address"     (string) bitcoin address
     ,...
  ],
  "p2sh","address" (string) address of P2SH script wrapping this redeem script (not returned if the script is already a P2SH).
}
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decodescript", "params": ["522103ede722780d27b05f0b1169efc90fa15a601a32fc6c3295114500c586831b6aaf2102ecd2d250a76d204011de6bc365a56033b9b3a149f679bc17205555d3c2b2854f21022d609d2f0d359e5bc0e5d0ea20ff9f5d3396cb5b1906aa9c56a0e7b5edc0c5d553ae"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":{"asm":"2 03ede722780d27b05f0b1169efc90fa15a601a32fc6c3295114500c586831b6aaf 02ecd2d250a76d204011de6bc365a56033b9b3a149f679bc17205555d3c2b2854f 022d609d2f0d359e5bc0e5d0ea20ff9f5d3396cb5b1906aa9c56a0e7b5edc0c5d5 3 OP_CHECKMULTISIG","reqSigs":2,"type":"multisig","addresses":["mjbLRSidW1MY8oubvs4SMEnHNFXxCcoehQ","mo1vzGwCzWqteip29vGWWW6MsEBREuzW94","mt17cV37fBqZsnMmrHnGCm9pM28R1kQdMG"],"p2sh":"2MyVxxgNBk5zHRPRY2iVjGRJHYZEp1pMCSq"},"error":null,"id":"curltest"}
```

### <span id="getrawtransaction">getrawtransaction</span>
Return the raw transaction data.
#### Parameters
```
Arguments:
1. "txid"      (string, required) The transaction id
2. verbose     (bool, optional, default=false) If false, return a string, otherwise return a json object
3. "blockhash" (string, optional) The block in which to look for the transaction
```
#### Returns
```
Result (if verbose is not set or set to false):
"data"      (string) The serialized, hex-encoded data for 'txid'

Result (if verbose is set to true):
{
  "in_active_chain": b, (bool) Whether specified block is in the active chain or not (only present with explicit "blockhash" argument)
  "hex" : "data",       (string) The serialized, hex-encoded data for 'txid'
  "txid" : "id",        (string) The transaction id (same as provided)
  "hash" : "id",        (string) The transaction hash (differs from txid for witness transactions)
  "size" : n,             (numeric) The serialized transaction size
  "vsize" : n,            (numeric) The virtual transaction size (differs from size for witness transactions)
  "version" : n,          (numeric) The version
  "locktime" : ttt,       (numeric) The lock time
  "vin" : [               (array of json objects)
     {
       "txid": "id",    (string) The transaction id
       "vout": n,         (numeric) 
       "scriptSig": {     (json object) The script
         "asm": "asm",  (string) asm
         "hex": "hex"   (string) hex
       },
       "sequence": n      (numeric) The script sequence number
       "txinwitness": ["hex", ...] (array of string) hex-encoded witness data (if any)
     }
     ,...
  ],
  "vout" : [              (array of json objects)
     {
       "value" : x.xxx,            (numeric) The value in BTC
       "n" : n,                    (numeric) index
       "scriptPubKey" : {          (json object)
         "asm" : "asm",          (string) the asm
         "hex" : "hex",          (string) the hex
         "reqSigs" : n,            (numeric) The required sigs
         "type" : "pubkeyhash",  (string) The type, eg 'pubkeyhash'
         "addresses" : [           (json array of string)
           "address"        (string) bitcoin address
           ,...
         ]
       }
     }
     ,...
  ],
  "blockhash" : "hash",   (string) the block hash
  "confirmations" : n,      (numeric) The confirmations
  "time" : ttt,             (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT)
  "blocktime" : ttt         (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawtransaction", "params": ["52309405287e737cf412fc42883d65a392ab950869fae80b2a5f1e33326aca46", true]}' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"txid":"52309405287e737cf412fc42883d65a392ab950869fae80b2a5f1e33326aca46","hash":"52309405287e737cf412fc42883d65a392ab950869fae80b2a5f1e33326aca46","version":1,"size":223,"vsize":223,"locktime":0,"vin":[{"txid":"2ac0daff49a4ff82a35a4864797f99f23c396b0529c5ba1e04b3d7b97521feba","vout":0,"scriptSig":{"asm":"3044022013d212c22f0b46bb33106d148493b9a9723adb2c3dd3a3ebe3a9c9e3b95d8cb00220461661710202fbab550f973068af45c294667fc4dc526627a7463eb23ab39e9b[ALL] 0479be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798483ada7726a3c4655da4fbfc0e1108a8fd17b448a68554199c47d08ffb10d4b8","hex":"473044022013d212c22f0b46bb33106d148493b9a9723adb2c3dd3a3ebe3a9c9e3b95d8cb00220461661710202fbab550f973068af45c294667fc4dc526627a7463eb23ab39e9b01410479be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798483ada7726a3c4655da4fbfc0e1108a8fd17b448a68554199c47d08ffb10d4b8"},"sequence":4294967295}],"vout":[{"value":0.06990000,"n":0,"scriptPubKey":{"asm":"OP_DUP OP_HASH160 01b81d5fa1e55e069e3cc2db9c19e2e80358f306 OP_EQUALVERIFY OP_CHECKSIG","hex":"76a91401b81d5fa1e55e069e3cc2db9c19e2e80358f30688ac","reqSigs":1,"type":"pubkeyhash","addresses":["1A6Ei5cRfDJ8jjhwxfzLJph8B9ZEthR9Z"]}}],"hex":"0100000001bafe2175b9d7b3041ebac529056b393cf2997f7964485aa382ffa449ffdac02a000000008a473044022013d212c22f0b46bb33106d148493b9a9723adb2c3dd3a3ebe3a9c9e3b95d8cb00220461661710202fbab550f973068af45c294667fc4dc526627a7463eb23ab39e9b01410479be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798483ada7726a3c4655da4fbfc0e1108a8fd17b448a68554199c47d08ffb10d4b8ffffffff01b0a86a00000000001976a91401b81d5fa1e55e069e3cc2db9c19e2e80358f30688ac00000000","blockhash":"0000000000000000015955e197fc362502a32f76290e5b5e5be822f9f161b3f3","confirmations":92787,"time":1483591778,"blocktime":1483591778},"error":null,"id":"curltest"}
```

### <span id="sendrawtransaction">sendrawtransaction</span>
Submits raw transaction (serialized, hex-encoded) to local node and network.
#### Parameters
```
Arguments:
1. "hexstring"    (string, required) The hex string of the raw transaction)
2. allowhighfees    (boolean, optional, default=false) Allow high fees
```
#### Returns
```
Result:
"hex"             (string) The transaction hash in hex
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendrawtransaction", "params": ["01000000011da9283b4ddf8d89eb996988b89ead56cecdc44041ab38bf787f1206cd90b51e000000006a47304402200ebea9f630f3ee35fa467ffc234592c79538ecd6eb1c9199eb23c4a16a0485a20220172ecaf6975902584987d295b8dddf8f46ec32ca19122510e22405ba52d1f13201210256d16d76a49e6c8e2edc1c265d600ec1a64a45153d45c29a2fd0228c24c3a524ffffffff01405dc600000000001976a9140dfc8bafc8419853b34d5e072ad37d1a5159f58488ac00000000"]}' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":"f5a5ce5988cc72b9b90e8d1d6c910cda53c88d2175177357cc2f2cf0899fbaad","error":null,"id":"curltest"}
```

### <span id="signrawtransaction">signrawtransaction</span>
Sign inputs for raw transaction
#### Parameters
```
Arguments:
1. "hexstring"     (string, required) The transaction hex string
2. "prevtxs"       (string, optional) An json array of previous dependent transaction outputs
     [               (json array of json objects, or 'null' if none provided)
       {
         "txid":"id",             (string, required) The transaction id
         "vout":n,                  (numeric, required) The output number
         "scriptPubKey": "hex",   (string, required) script key
         "redeemScript": "hex",   (string, required for P2SH or P2WSH) redeem script
         "amount": value            (numeric, required) The amount spent
       }
       ,...
    ]
3. "privkeys"     (string, optional) A json array of base58-encoded private keys for signing
    [                  (json array of strings, or 'null' if none provided)
      "privatekey"   (string) private key in base58-encoding
      ,...
    ]
4. "sighashtype"     (string, optional, default=ALL) The signature hash type. Must be one of
       "ALL"
       "NONE"
       "SINGLE"
       "ALL|ANYONECANPAY"
       "NONE|ANYONECANPAY"
       "SINGLE|ANYONECANPAY"
```
#### Returns
```
Result:
{
  "hex" : "value",           (string) The hex-encoded raw transaction with signature(s)
  "complete" : true|false,   (boolean) If the transaction has a complete set of signatures
  "errors" : [                 (json array of objects) Script verification errors (if there are any)
    {
      "txid" : "hash",           (string) The hash of the referenced, previous transaction
      "vout" : n,                (numeric) The index of the output to spent and used as input
      "scriptSig" : "hex",       (string) The hex-encoded signature script
      "sequence" : n,            (numeric) Script sequence number
      "error" : "text"           (string) Verification or signing error related to the input
    }
    ,...
  ]
}
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendrawtransaction", "params": ["01000000011da9283b4ddf8d89eb996988b89ead56cecdc44041ab38bf787f1206cd90b51e0000000000ffffffff01405dc600000000001976a9140dfc8bafc8419853b34d5e072ad37d1a5159f58488ac00000000"]}' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":{
    "hex" : "01000000011da9283b4ddf8d89eb996988b89ead56cecdc44041ab38bf787f1206cd90b51e000000006a47304402200ebea9f630f3ee35fa467ffc234592c79538ecd6eb1c9199eb23c4a16a0485a20220172ecaf6975902584987d295b8dddf8f46ec32ca19122510e22405ba52d1f13201210256d16d76a49e6c8e2edc1c265d600ec1a64a45153d45c29a2fd0228c24c3a524ffffffff01405dc600000000001976a9140dfc8bafc8419853b34d5e072ad37d1a5159f58488ac00000000",
    "complete" : true
},"error":null,"id":"curltest"}
```

### <span id="createmultisig">createmultisig</span>
Creates a multi-signature address with n signature of m keys required.
It returns a json object with the address and redeemScript.
#### Parameters
```
Arguments:
1. nrequired                    (numeric, required) The number of required signatures out of the n keys or addresses.
2. "keys"                       (string, required) A json array of hex-encoded public keys
     [
       "key"                    (string) The hex-encoded public key
       ,...
     ]
```
#### Returns
```
Result:
{
  "address":"multisigaddress",  (string) The value of the new multisig address.
  "redeemScript":"script"       (string) The string value of the hex-encoded redemption script.
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createmultisig", "params": [2, "[\"03789ed0bb717d88f7d321a368d905e7430207ebbd82bd342cf11ae157a7ace5fd\",\"03dbc6764b8884a92e871274b87583e6d5c2a58819473e17e107ef3f6aa5a61626\"]"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{
  "address" : "2MyVxxgNBk5zHRPRY2iVjGRJHYZEp1pMCSq",
  "redeemScript" : "522103ede722780d27b05f0b1169efc90fa15a601a32fc6c3295114500c586831b6aaf2102ecd2d250a76d204011de6bc365a56033b9b3a149f679bc17205555d3c2b2854f21022d609d2f0d359e5bc0e5d0ea20ff9f5d3396cb5b1906aa9c56a0e7b5edc0c5d553ae"
},"error":null,"id":"curltest"}
```

### <span id="signmessagewithprivkey">signmessagewithprivkey</span>
Sign a message with the private key of an address
#### Parameters
```
Arguments:
1. "privkey"         (string, required) The private key to sign the message with.
2. "message"         (string, required) The message to create a signature of.
```
#### Returns
```
Result:
"signature"          (string) The signature of the message encoded in base 64
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signmessagewithprivkey", "params": ["5HpHagT65TZzG1PH3CSu63k8DbpvD8s5ip4nEB3kEsreKamq6aB", "Hello, World!"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"G+ZauMFgQExAJRKZSldbAVEaZo4i0p2AVivbFASo50PkUnynAMDUiNMVdXDlpYMWvatxCmYmLn8C9zygPRn3Y1c=","error":null,"id":"curltest"}
```

### <span id="validateaddress">validateaddress</span>
Return information about the given bitcoin address.
#### Parameters
```
Arguments:
1. "address"     (string, required) The bitcoin address to validate
```
#### Returns
```
Result:
{
  "isvalid" : true|false,       (boolean) If the address is valid or not. If not, this is the only property returned.
  "address" : "address",        (string) The bitcoin address validated
  "scriptPubKey" : "hex",       (string) The hex encoded scriptPubKey generated by the address
  "ismine" : true|false,        (boolean) If the address is yours or not
  "iswatchonly" : true|false,   (boolean) If the address is watchonly
  "isscript" : true|false,      (boolean, optional) If the address is P2SH or P2WSH. Not included for unknown witness types.
  "iswitness" : true|false,     (boolean) If the address is P2WPKH, P2WSH, or an unknown witness version
  "witness_version" : version   (number, optional) For all witness output types, gives the version number.
  "witness_program" : "hex"     (string, optional) For all witness output types, gives the script or key hash present in the address.
  "script" : "type"             (string, optional) The output script type. Only if "isscript" is true and the redeemscript is known. Possible types: nonstandard, pubkey, pubkeyhash, scripthash, multisig, nulldata, witness_v0_keyhash, witness_v0_scripthash, witness_unknown
  "hex" : "hex",                (string, optional) The redeemscript for the P2SH or P2WSH address
  "addresses"                   (string, optional) Array of addresses associated with the known redeemscript (only if "iswitness" is false). This field is superseded by the "pubkeys" field and the address inside "embedded".
    [
      "address"
      ,...
    ]
  "pubkeys"                     (string, optional) Array of pubkeys associated with the known redeemscript (only if "script" is "multisig")
    [
      "pubkey"
      ,...
    ]
  "sigsrequired" : xxxxx        (numeric, optional) Number of signatures required to spend multisig output (only if "script" is "multisig")
  "pubkey" : "publickeyhex",    (string, optional) The hex value of the raw public key, for single-key addresses (possibly embedded in P2SH or P2WSH)
  "embedded" : {...},           (object, optional) information about the address embedded in P2SH or P2WSH, if relevant and known. It includes all validateaddress output fields for the embedded address, excluding "isvalid", metadata ("timestamp", "hdkeypath", "hdmasterkeyid") and relation to the wallet ("ismine", "iswatchonly", "account").
  "iscompressed" : true|false,  (boolean) If the address is compressed
  "account" : "account"         (string) DEPRECATED. The account associated with the address, "" is the default account
  "timestamp" : timestamp,      (number, optional) The creation time of the key if available in seconds since epoch (Jan 1 1970 GMT)
  "hdkeypath" : "keypath"       (string, optional) The HD keypath if the key is HD and available
  "hdmasterkeyid" : "<hash160>" (string, optional) The Hash160 of the HD master pubkey
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "validateaddress", "params": ["17fshh33qUze2yifiJ2sXgijSMzJ2KNEwu"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"isvalid":true,"address":"17fshh33qUze2yifiJ2sXgijSMzJ2KNEwu","scriptPubKey":"76a914492ae280d70af33acf0ae7cd329b961e65e9cbd888ac","ismine":false,"iswatchonly":false,"isscript":false,"iswitness":false},"error":null,"id":"curltest"}
```

### <span id="verifymessage">verifymessage</span>
Verify a signed message
#### Parameters
```
Arguments:
1. "address"         (string, required) The bitcoin address to use for the signature.
2. "signature"       (string, required) The signature provided by the signer in base 64 encoding (see signmessage).
3. "message"         (string, required) The message that was signed.
```
#### Returns
```
Result:
true|false   (boolean) If the signature is verified or not.
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifymessage", "params": ["mgnucj8nYqdrPFh2JfZSB1NmUThUGnmsqe", "IL98ziCmwYi5pL+dqKp4Ux+zCa4hP/xbjHmWh+Mk/lefV/0pWV1p/gQ94jgExSmgH2/+PDcCCrOHAady2IEySSI=", "Hello, World!"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":true,"error":null,"id":"curltest"}
```

### <span id="abandontransaction">abandontransaction</span>
Mark in-wallet transaction <txid> as abandoned
#### Parameters
```
Arguments:
1. "txid"    (string, required) The transaction id
```
#### Returns
```
Result:
null
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "abandontransaction", "params": ["fa3970c341c9f5de6ab13f128cbfec58d732e736a505fe32137ad551c799ecc4"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="abortrescan">abortrescan</span>
Stops current wallet rescan triggered by an RPC call, e.g. by an importprivkey call.
#### Parameters
```
none
```
#### Returns
```
Result:
true/false
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "abortrescan", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":false,"error":null,"id":"curltest"}
```

### <span id="backupwallet">backupwallet</span>
Safely copies current wallet file to destination, which can be a directory or a path with filename.
#### Parameters
```
Arguments:
1. "destination"   (string) The destination directory or file
```
#### Returns
```
Result:
true/false
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "backupwallet", "params": ["backup.dat"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="dumpprivkey">dumpprivkey</span>
Reveals the private key corresponding to 'address'.
Then the importprivkey can be used with this output
#### Parameters
```
Arguments:
1. "address"   (string, required) The bitcoin address for the private key
```
#### Returns
```
Result:
"key"                (string) The private key
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpprivkey", "params": ["1GGBGzhJwu1pjd4XsWNuc1TJtgeKeXMHsJ"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"L2mN9wjRTFdcz9i7oJAWqzaSpepPT3WqQaTpjUaGPAjot27ftgJS","error":null,"id":"curltest"}
```

### <span id="dumpwallet">dumpwallet</span>
Dumps all wallet keys in a human-readable format to a server-side file. This does not allow overwriting existing files.
#### Parameters
```
Arguments:
1. "filename"    (string, required) The filename with path (either absolute or relative to bitcoind)
```
#### Returns
```
Result:
{                           (json object)
  "filename" : {        (string) The filename with full absolute path
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpwallet", "params": ["/tmp/wallet.dat"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"filename":"/tmp/wallet.dat"},"error":null,"id":"curltest"}
```

### <span id="encryptwallet">encryptwallet</span>
Encrypts the wallet with 'passphrase'. This is for first time encryption.
#### Parameters
```
Arguments:
1. "passphrase"    (string) The pass phrase to encrypt the wallet with. It must be at least 1 character, but should be long.
```
#### Returns
```
Result:
{                           (json object)
  "filename" : {        (string) The filename with full absolute path
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "encryptwallet", "params": ["123456"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"wallet encrypted; Bitcoin server stopping, restart to run with encrypted
wallet. The keypool has been flushed, you need to make a new backup."},"error":null,"id":"curltest"}
```

### <span id="getaccount">getaccount</span>
DEPRECATED. Returns the account associated with the given address.
#### Parameters
```
Arguments:
1. "address"         (string, required) The bitcoin address for account lookup.
```
#### Returns
```
Result:
"accountname"        (string) the account address
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccount", "params": ["1GGBGzhJwu1pjd4XsWNuc1TJtgeKeXMHsJ"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"xzy","error":null,"id":"curltest"}
```

### <span id="getaccountaddress">getaccountaddress</span>
DEPRECATED. Returns the current Bitcoin address for receiving payments to this account.
#### Parameters
```
Arguments:
1. "account"       (string, required) The account name for the address. It can also be set to the empty string "" to represent the default account. The account does not need to exist, it will be created and a new address created  if there is no account by the given name
```
#### Returns
```
Result:
"address"          (string) The account bitcoin address
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccountaddress", "params": ["xzy"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"326DqUAtAkfeF9PJN1L7nPngb8VmRM4JBS","error":null,"id":"curltest"}
```

### <span id="getaddressesbyaccount">getaddressesbyaccount</span>
DEPRECATED. Returns the list of addresses for the given account.
#### Parameters
```
Arguments:
1. "account"        (string, required) The account name.
```
#### Returns
```
Result:
[                     (json array of string)
  "address"         (string) a bitcoin address associated with the given account
  ,...
]
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressesbyaccount", "params": ["xzy"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":["1GGBGzhJwu1pjd4XsWNuc1TJtgeKeXMHsJ","326DqUAtAkfeF9PJN1L7nPngb8VmRM4JBS","359bmBTthPmjtSFbR7XVnXwh6GTUY2oVJ9","35fx2bgdBRhBVn7ZqrtnHbSKxhCoMXkyDE","36pEkZuEKr3Q5s5FFN2p1nun8pFb6FpLhc","38uvj6ob92Tg8aqScLvVzomUPkuXwpxP6v","3BNzjdt1kgqWf6sTksfCGeUMjGEm6jg246","3BR72j9YYjD2SQfo5Bo3QVJJGhSsEt6cHm","3CDbG7ZcNsxJrXXMxWvHvL9ihB7BmdGwq9","3CjdFE35j6d6UnzMRunDfgrqzL1e5A7bh8","3Eg5DAMEyVd4344EP9QMXozdZkbzynkXZE","3G8u7WGnZoEC9fiHbpK4vdxY41Xr3edwFp","3KTguhDtdJCtNvKXZAFzJuPbxeGNNEEKQJ","3LgKrNXZsRqzrM5Pqs43ZyddZuy4HKcARz","3LwTpnVkB2sz5VGwZH3tBKTFij3BdXxG7o","3NhAaXT9sPv5P85zMBv2WqG1geoZVVdove","bc1q5a5tgdc4y6v883lt7hd59q8r5hc9yu8g20tn4r"],"error":null,"id":"curltest"}
```

### <span id="getbalance">getbalance</span>
If account is not specified, returns the server's total available balance.
#### Parameters
```
Arguments:
1. "account"         (string, optional) DEPRECATED. The account string may be given as a
                     specific account name to find the balance associated with wallet keys in
                     a named account, or as the empty string ("") to find the balance
                     associated with wallet keys not in any named account, or as "*" to find
                     the balance associated with all wallet keys regardless of account.
                     When this option is specified, it calculates the balance in a different
                     way than when it is not specified, and which can count spends twice when
                     there are conflicting pending transactions (such as those created by
                     the bumpfee command), temporarily resulting in low or even negative
                     balances. In general, account balance calculation is not considered
                     reliable and has resulted in confusing outcomes, so it is recommended to
                     avoid passing this argument.
2. minconf           (numeric, optional, default=1) Only include transactions confirmed at least this many times.
3. include_watchonly (bool, optional, default=false) Also include balance in watch-only addresses (see 'importaddress')
```
#### Returns
```
Result:
amount              (numeric) The total amount in BTC received for this account.
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbalance", "params": ["xzy"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":0.00000000,"error":null,"id":"curltest"}
```

### <span id="getnewaddress">getnewaddress</span>
Returns a new Bitcoin address for receiving payments.
#### Parameters
```
Arguments:
1. "account"        (string, optional) DEPRECATED. The account name for the address to be linked to. If not provided, the default account "" is used. It can also be set to the empty string "" to represent the default account. The account does not need to exist, it will be created if there is no account by the given name.
2. "address_type"   (string, optional) The address type to use. Options are "legacy", "p2sh-segwit", and "bech32". Default is set by -addresstype.
```
#### Returns
```
Result:
"address"    (string) The new bitcoin address
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnewaddress", "params": ["xzy"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"3KxYUn1x6dRnQnLD6LZQw48VfS2dCWtwvn","error":null,"id":"curltest"}
```

### <span id="getrawchangeaddress">getrawchangeaddress</span>
Returns a new Bitcoin address, for receiving change.
This is for use with raw transactions, NOT normal use.
#### Parameters
```
Arguments:
1. "address_type"           (string, optional) The address type to use. Options are "legacy", "p2sh-segwit", and "bech32". Default is set by -changetype.
```
#### Returns
```
Result:
"address"    (string) The address
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawchangeaddress", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":"3MuQ5Van6kVXemNCTHBbipE91j2vUyq8dj","error":null,"id":"curltest"}
```

### <span id="getreceivedbyaccount">getreceivedbyaccount</span>
DEPRECATED. Returns the total amount received by addresses with <account> in transactions with at least [minconf] confirmations.
#### Parameters
```
Arguments:
1. "account"      (string, required) The selected account, may be the default account using "".
2. minconf          (numeric, optional, default=1) Only include transactions confirmed at least this many times.
```
#### Returns
```
Result:
amount              (numeric) The total amount in BTC received for this account.
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getreceivedbyaccount", "params": ["xzy"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":0.58000000,"error":null,"id":"curltest"}
```

### <span id="getreceivedbyaddress">getreceivedbyaddress</span>
Returns the total amount received by the given address in transactions with at least minconf confirmations.
#### Parameters
```
Arguments:
1. "address"         (string, required) The bitcoin address for transactions.
2. minconf             (numeric, optional, default=1) Only include transactions confirmed at least this many times.
```
#### Returns
```
Result:
amount   (numeric) The total amount in BTC received at this address.
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getreceivedbyaddress", "params": ["2N6BjhgkJANxpcb5DFJdsQmsXGTS12wPkJs"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":0.00000000,"error":null,"id":"curltest"}
```

### <span id="gettransaction">gettransaction</span>
Get detailed information about in-wallet transaction <txid>
#### Parameters
```
Arguments:
1. "txid"                  (string, required) The transaction id
2. "include_watchonly"     (bool, optional, default=false) Whether to include watch-only addresses in balance calculation and details[]
```
#### Returns
```
Result:
{
  "amount" : x.xxx,        (numeric) The transaction amount in BTC
  "fee": x.xxx,            (numeric) The amount of the fee in BTC. This is negative and only available for the 
                              'send' category of transactions.
  "confirmations" : n,     (numeric) The number of confirmations
  "blockhash" : "hash",  (string) The block hash
  "blockindex" : xx,       (numeric) The index of the transaction in the block that includes it
  "blocktime" : ttt,       (numeric) The time in seconds since epoch (1 Jan 1970 GMT)
  "txid" : "transactionid",   (string) The transaction id.
  "time" : ttt,            (numeric) The transaction time in seconds since epoch (1 Jan 1970 GMT)
  "timereceived" : ttt,    (numeric) The time received in seconds since epoch (1 Jan 1970 GMT)
  "bip125-replaceable": "yes|no|unknown",  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                   may be unknown for unconfirmed transactions not in the mempool
  "details" : [
    {
      "account" : "accountname",      (string) DEPRECATED. The account name involved in the transaction, can be "" for the default account.
      "address" : "address",          (string) The bitcoin address involved in the transaction
      "category" : "send|receive",    (string) The category, either 'send' or 'receive'
      "amount" : x.xxx,                 (numeric) The amount in BTC
      "label" : "label",              (string) A comment for the address/transaction, if any
      "vout" : n,                       (numeric) the vout value
      "fee": x.xxx,                     (numeric) The amount of the fee in BTC. This is negative and only available for the 
                                           'send' category of transactions.
      "abandoned": xxx                  (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the 
                                           'send' category of transactions.
    }
    ,...
  ],
  "hex" : "data"         (string) Raw data for transaction
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettransaction", "params": ["1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{
    "amount" : 0.00000000,
    "fee" : 0.00000000,
    "confirmations" : 106670,
    "blockhash" : "000000008b630b3aae99b6fe215548168bed92167c47a2f7ad4df41e571bcb51",
    "blockindex" : 1,
    "blocktime" : 1396321351,
    "txid" : "5a7d24cd665108c66b2d56146f244932edae4e2376b561b3d396d5ae017b9589",
    "walletconflicts" : [
    ],
    "time" : 1396321351,
    "timereceived" : 1418924711,
    "bip125-replaceable" : "no",
    "details" : [
        {
            "account" : "",
            "address" : "mjSk1Ny9spzU2fouzYgLqGUD8U41iR35QN",
            "category" : "send",
            "amount" : -0.10000000,
            "vout" : 0,
            "fee" : 0.00000000
        },
        {
            "account" : "doc test",
            "address" : "mjSk1Ny9spzU2fouzYgLqGUD8U41iR35QN",
            "category" : "receive",
            "amount" : 0.10000000,
            "vout" : 0
        }
    ],
    "hex" : "0100000001cde58f2e37d000eabbb60d9cf0b79ddf67cede6dba58732539983fa341dd5e6c010000006a47304402201feaf12908260f666ab369bb8753cdc12f78d0c8bdfdef997da17acff502d321022049ba0b80945a7192e631c03bafd5c6dc3c7cb35ac5c1c0ffb9e22fec86dd311c01210321eeeb46fd878ce8e62d5e0f408a0eab41d7c3a7872dc836ce360439536e423dffffffff0180969800000000001976a9142b14950b8d31620c6cc923c5408a701b1ec0a02088ac00000000"
},"error":null,"id":"curltest"}
```

### <span id="getunconfirmedbalance">getunconfirmedbalance</span>
Returns the server's total unconfirmed balance
#### Parameters
```
none
```
#### Returns
```
Result:
number
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getunconfirmedbalance", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":0.00000000,"error":null,"id":"curltest"}
```

### <span id="getwalletinfo">getwalletinfo</span>
Returns an object containing various wallet state info.
#### Parameters
```
none
```
#### Returns
```
Result:
{
  "walletname": xxxxx,             (string) the wallet name
  "walletversion": xxxxx,          (numeric) the wallet version
  "balance": xxxxxxx,              (numeric) the total confirmed balance of the wallet in BTC
  "unconfirmed_balance": xxx,      (numeric) the total unconfirmed balance of the wallet in BTC
  "immature_balance": xxxxxx,      (numeric) the total immature balance of the wallet in BTC
  "txcount": xxxxxxx,              (numeric) the total number of transactions in the wallet
  "keypoololdest": xxxxxx,         (numeric) the timestamp (seconds since Unix epoch) of the oldest pre-generated key in the key pool
  "keypoolsize": xxxx,             (numeric) how many new keys are pre-generated (only counts external keys)
  "keypoolsize_hd_internal": xxxx, (numeric) how many new keys are pre-generated for internal use (used for change outputs, only appears if the wallet is using this feature, otherwise external keys are used)
  "unlocked_until": ttt,           (numeric) the timestamp in seconds since epoch (midnight Jan 1 1970 GMT) that the wallet is unlocked for transfers, or 0 if the wallet is locked
  "paytxfee": x.xxxx,              (numeric) the transaction fee configuration, set in BTC/kB
  "hdmasterkeyid": "<hash160>"     (string, optional) the Hash160 of the HD master pubkey (only present when HD is enabled)
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getwalletinfo", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"walletname":"wallet.dat","walletversion":159900,"balance":0.00000000,"unconfirmed_balance":0.00000000,"immature_balance":0.00000000,"txcount":0,"keypoololdest":1534402945,"keypoolsize":999,"keypoolsize_hd_internal":999,"unlocked_until":0,"paytxfee":0.00000000,"hdmasterkeyid":"eca07e9ccab1f823dfbfaf5b0660bcbbc224c7bc"},"error":null,"id":"curltest"}
```

### <span id="importaddress">importaddress</span>
Adds a script (in hex) or address that can be watched as if it were in your wallet but cannot be used to spend. Requires a new wallet backup.
#### Parameters
```
Arguments:
1. "script"           (string, required) The hex-encoded script (or address)
2. "label"            (string, optional, default="") An optional label
3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions
4. p2sh                 (boolean, optional, default=false) Add the P2SH version of the script as well
```
#### Returns
```
none
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importaddress", "params": ["muhtvdmsnbQEPFuEmxcChX58fGvXaaUoVt "] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
没有输出;成功
```

### <span id="importprivkey">importprivkey</span>
Adds a private key (as returned by dumpprivkey) to your wallet. Requires a new wallet backup.
#### Parameters
```
Arguments:
1. "privkey"          (string, required) The private key (see dumpprivkey)
2. "label"            (string, optional, default="") An optional label
3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions
```
#### Returns
```
none
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importprivkey", "params": ["cU8Q2jGeX3GNKNa5etiC8mgEgFSeVUTRQfWE2ZCzszyqYNK4Mepy"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
没有输出;成功
```

### <span id="importwallet">importwallet</span>
Imports keys from a wallet dump file (see dumpwallet). Requires a new wallet backup to include imported keys.
#### Parameters
```
Arguments:
1. "filename"    (string, required) The wallet file
```
#### Returns
```
none
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importwallet", "params": ["/tmp/dump.txt"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
没有输出;成功
```

### <span id="keypoolrefill">keypoolrefill</span>
Fills the keypool.
Requires wallet passphrase to be set with walletpassphrase call.
#### Parameters
```
Arguments
1. newsize     (numeric, optional, default=100) The new keypool size
```
#### Returns
```
null
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "keypoolrefill", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="listaccounts">listaccounts</span>
DEPRECATED. Returns Object that has account names as keys, account balances as values.
#### Parameters
```
Arguments:
1. minconf             (numeric, optional, default=1) Only include transactions with at least this many confirmations
2. include_watchonly   (bool, optional, default=false) Include balances in watch-only addresses (see 'importaddress')
```
#### Returns
```
Result:
{                      (json object where keys are account names, and values are numeric balances
  "account": x.xxx,  (numeric) The property name is the account name, and the value is the total balance for the account.
  ...
}
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaccounts", "params": [6] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":{"":0.66825951,"xxx":0.50000000,"xzy":0.07723632,"xzy1":0.00000000},"error":null,"id":"curltest"}
```

### <span id="listaddressgroupings">listaddressgroupings</span>
Lists groups of addresses which have had their common ownership
made public by common use as inputs or as the resulting change in past transactions
#### Parameters
```
none
```
#### Returns
```
Result:
[
  [
    [
      "address",            (string) The bitcoin address
      amount,                 (numeric) The amount in BTC
      "account"             (string, optional) DEPRECATED. The account
    ]
    ,...
  ]
  ,...
]
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaddressgroupings", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":[[["mgnucj8nYqdrPFh2JfZSB1NmUThUGnmsqe",0.01000000,""]],[["muhtvdmsnbQEPFuEmxcChX58fGvXaaUoVt",0.00000000,""]],[["2MtTiF9Pg4C61pmSb6pGrVZ2NwDxmkPYtgL",0.20208723],["2MthDjfCEjuG42v3uavy7i6j6Hfwtu7kc4c",0.00000000,"xzy"],["2MxYG2xeKuRyDTG6ULbZGMnBYCckM7kSU2u",0.00000000],["2N11bnjMX1B9Sqka7w9K3HSsZ4uHE9AQ5pa",0.00000000],["2N2ZfXpjMibHX3MkWzkh8RtwRd44Es7rkSs",0.00000000],["2N4roo7c5KChT1pyp6sJJbeNUmn9ZQiAm4P",0.00000000,""],["2NA3GuX5VbCHn19RUMd1kDyekQ6wY9vwPv5",0.00000000],["2NAS6E68p7G6mAU41JfthdmL78eVQYYsc4K",0.00000000],["2ND5nq1TAuPjdGYDtamPLHLKCvM293SnwKN",0.00000000],["2NDdqRJ8VmHgqcmDu9BkQ8MmSnZ9R8HLvbf",0.00000000],["2NFuVsqE46XKgZ6cQkD2XmunAt857L1m8ye",0.00000000]],[["2MuFard6DF5eFNqNdfRdpAXUi1u8ZfK3Gto",0.00000000,""],["2MyadDTC7wXc17CjEGqUJWRjdrRx9P5qxR3",0.44922110]],[["2Mv2DXsh8tajUjLJNy9V2vX7PWVKAzUA9NC",0.00000000],["2N3dMFz2t3AG57xwaZX3gm9Fna1p9o8JwU8",0.00500000,"xzy"],["2NBEVML5bL77TNSLZnuSPkXuHPZNZb77NCd",0.07918750]],[["2MwMuc1SEHUdCcJrq7Mz9zZcV4xMHBZp5zk",0.50000000,"xxx"]]],"error":null,"id":"curltest"}
```

### <span id="listlockunspent">listlockunspent</span>
Returns list of temporarily unspendable outputs.
See the lockunspent call to lock and unlock transactions for spending.
#### Parameters
```
none
```
#### Returns
```
Result:
[
  {
    "txid" : "transactionid",     (string) The transaction id locked
    "vout" : n                      (numeric) The vout value
  }
  ,...
]
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listlockunspent", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":[],"error":null,"id":"curltest"}
```

### <span id="listreceivedbyaccount">listreceivedbyaccount</span>
DEPRECATED. List balances by account.
#### Parameters
```
Arguments:
1. minconf           (numeric, optional, default=1) The minimum number of confirmations before payments are included.
2. include_empty     (bool, optional, default=false) Whether to include accounts that haven't received any payments.
3. include_watchonly (bool, optional, default=false) Whether to include watch-only addresses (see 'importaddress').
```
#### Returns
```
Result:
[
  {
    "involvesWatchonly" : true,   (bool) Only returned if imported addresses were involved in transaction
    "account" : "accountname",  (string) The account name of the receiving account
    "amount" : x.xxx,             (numeric) The total amount received by addresses with this account
    "confirmations" : n,          (numeric) The number of confirmations of the most recent transaction included
    "label" : "label"           (string) A comment for the address/transaction, if any
  }
  ,...
]
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaccount", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":[{"account":"","amount":2.83171000,"confirmations":56723},{"account":"xxx","amount":0.50000000,"confirmations":1645},{"account":"xzy","amount":0.58000000,"confirmations":1667}],"error":null,"id":"curltest"}
```

### <span id="listreceivedbyaddress">listreceivedbyaddress</span>
List balances by receiving address.
#### Parameters
```
Arguments:
1. minconf           (numeric, optional, default=1) The minimum number of confirmations before payments are included.
2. include_empty     (bool, optional, default=false) Whether to include addresses that haven't received any payments.
3. include_watchonly (bool, optional, default=false) Whether to include watch-only addresses (see 'importaddress').
```
#### Returns
```
Result:
[
  {
    "involvesWatchonly" : true,        (bool) Only returned if imported addresses were involved in transaction
    "address" : "receivingaddress",  (string) The receiving address
    "account" : "accountname",       (string) DEPRECATED. The account of the receiving address. The default account is "".
    "amount" : x.xxx,                  (numeric) The total amount in BTC received by the address
    "confirmations" : n,               (numeric) The number of confirmations of the most recent transaction included
    "label" : "label",               (string) A comment for the address/transaction, if any
    "txids": [
       n,                                (numeric) The ids of transactions received with the address 
       ...
    ]
  }
  ,...
]
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaddress", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":[{"address":"mgnucj8nYqdrPFh2JfZSB1NmUThUGnmsqe","account":"","amount":1.18171000,"confirmations":57430,"label":"","txids":["ef7c0cbf6ba5af68d2ea239bba709b26ff7b0b669839a63bb01c2cb8e8de481e","6d62d3f74be5ca614e32a2fb662deabe87ff95c7d90228cd8615da39cc824e34","ec259ab74ddff199e61caa67a26e29b13b5688dc60f509ce0df4d044e8f4d63d","4ab08d44edf035eeea27048318cfbb629b835fb7ff45517d0180e264cae2825b","ca7cb6a5ffcc2f21036879493db4530c0ce9b5bff9648f9a3be46e2dfc8e0166","a897d85cb2f30560c2f925dc622ca995fa9a69443533382bb23fc3927a1db06a","9d8f685656e6a5c786f0e90a5d206ab6e4cfd876b5e3124dbfa7929ed8c7a782","683ef8927f66040ca5114cd6320da0a0b3b29ea5b43915e37aafb10f4349858a","d54994ece1d11b19785c7248868696250ab195605b469632b7bd68130e880c9a","f5a5ce5988cc72b9b90e8d1d6c910cda53c88d2175177357cc2f2cf0899fbaad","efe58187c522770d1e44d56aa55b437f3e09dee0557729a4421325fa054feab3","6c5edd41a33f9839257358ba6ddece67df9db7f09c0db6bbea00d0372e8fe5cd","f14ee5368c339644d3037d929bbe1f1544a532f8826c7b7288cb994b0b0ff5d8"]},{"address":"2MthDjfCEjuG42v3uavy7i6j6Hfwtu7kc4c","account":"xzy","amount":0.27500000,"confirmations":56723,"label":"xzy","txids":["a6356a3c2be373937bf0968007a04ef299a0c637ab223c604dfa01dbafe0ca5b"]},{"address":"2MuFard6DF5eFNqNdfRdpAXUi1u8ZfK3Gto","account":"","amount":0.55000000,"confirmations":56723,"label":"","txids":["09486862e9c1c4b1c14513a90b3d44d5d567b97689ea4f754687c1cdb6b0f974"]},{"address":"2MwMuc1SEHUdCcJrq7Mz9zZcV4xMHBZp5zk","account":"xxx","amount":0.50000000,"confirmations":1645,"label":"xxx","txids":["7689e028f9b3368c81a834f1afba3951713e27d58c203c1052b5014cd8593405","931d2d9578714988b881d9f0017289d44b4e6a848478b0ef1529bf68cb742f29","955e161742995f45add62f385149e5e7cf420ef7917454b2eb934adab49bfaf3"]},{"address":"2N3dMFz2t3AG57xwaZX3gm9Fna1p9o8JwU8","account":"xzy","amount":0.30500000,"confirmations":1667,"label":"xzy","txids":["9f3d46c23d9258e716557a868c5f31dd03ca9ca7da57106a4554460ad2ecc140","f1b1ab345f6bb29bff0f7c1eb01bb3015ec84385c855555a69998538c8c2164f"]},{"address":"2N4roo7c5KChT1pyp6sJJbeNUmn9ZQiAm4P","account":"","amount":1.10000000,"confirmations":56725,"label":"","txids":["229d09d30ddac705aeb0e55384b90cf3310d59601977109df8a369c7597f5cc3"]}],"error":null,"id":"curltest"}
```

### <span id="listsinceblock">listsinceblock</span>
Get all transactions in blocks since block [blockhash], or all transactions if omitted.
If "blockhash" is no longer a part of the main chain, transactions from the fork point onward are included.
Additionally, if include_removed is set, transactions affecting the wallet which were removed are returned in the "removed" array.
#### Parameters
```
Arguments:
1. "blockhash"            (string, optional) The block hash to list transactions since
2. target_confirmations:    (numeric, optional, default=1) Return the nth block hash from the main chain. e.g. 1 would mean the best block hash. Note: this is not used as a filter, but only affects [lastblock] in the return value
3. include_watchonly:       (bool, optional, default=false) Include transactions to watch-only addresses (see 'importaddress')
4. include_removed:         (bool, optional, default=true) Show transactions that were removed due to a reorg in the "removed" array
                                                           (not guaranteed to work on pruned nodes)
```
#### Returns
```
Result:
{
  "transactions": [
    "account":"accountname",       (string) DEPRECATED. The account name associated with the transaction. Will be "" for the default account.
    "address":"address",    (string) The bitcoin address of the transaction. Not present for move transactions (category = move).
    "category":"send|receive",     (string) The transaction category. 'send' has negative amounts, 'receive' has positive amounts.
    "amount": x.xxx,          (numeric) The amount in BTC. This is negative for the 'send' category, and for the 'move' category for moves 
                                          outbound. It is positive for the 'receive' category, and for the 'move' category for inbound funds.
    "vout" : n,               (numeric) the vout value
    "fee": x.xxx,             (numeric) The amount of the fee in BTC. This is negative and only available for the 'send' category of transactions.
    "confirmations": n,       (numeric) The number of confirmations for the transaction. Available for 'send' and 'receive' category of transactions.
                                          When it's < 0, it means the transaction conflicted that many blocks ago.
    "blockhash": "hashvalue",     (string) The block hash containing the transaction. Available for 'send' and 'receive' category of transactions.
    "blockindex": n,          (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive' category of transactions.
    "blocktime": xxx,         (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
    "txid": "transactionid",  (string) The transaction id. Available for 'send' and 'receive' category of transactions.
    "time": xxx,              (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT).
    "timereceived": xxx,      (numeric) The time received in seconds since epoch (Jan 1 1970 GMT). Available for 'send' and 'receive' category of transactions.
    "bip125-replaceable": "yes|no|unknown",  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                   may be unknown for unconfirmed transactions not in the mempool
    "abandoned": xxx,         (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the 'send' category of transactions.
    "comment": "...",       (string) If a comment is associated with the transaction.
    "label" : "label"       (string) A comment for the address/transaction, if any
    "to": "...",            (string) If a comment to is associated with the transaction.
  ],
  "removed": [
    <structure is the same as "transactions" above, only present if include_removed=true>
    Note: transactions that were readded in the active chain will appear as-is in this array, and may thus have a positive confirmation count.
  ],
  "lastblock": "lastblockhash"     (string) The hash of the block (target_confirmations-1) from the best block on the main chain. This is typically used to feed back into listsinceblock the next time you call it. So you would generally use a target_confirmations of say 6, so you will be continually re-notified of transactions until they've reached 6 confirmations plus any new ones
}
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listsinceblock", "params": ["000000000000000bacf66f7497b7dc45ef753ee9a7d38571037cdb1a57f663ad", 6] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":{"transactions":[],"removed":[],"lastblock":"000000000000000000033697d8be6e2b13a2976caa87b14d64ac151424b3653c"},"error":null,"id":"curltest"}
```

### <span id="listtransactions">listtransactions</span>
Returns up to 'count' most recent transactions skipping the first 'from' transactions for account 'account'.
#### Parameters
```
Arguments:
1. "account"    (string, optional) DEPRECATED. The account name. Should be "*".
2. count          (numeric, optional, default=10) The number of transactions to return
3. skip           (numeric, optional, default=0) The number of transactions to skip
4. include_watchonly (bool, optional, default=false) Include transactions to watch-only addresses (see 'importaddress')
```
#### Returns
```
Result:
[
  {
    "account":"accountname",       (string) DEPRECATED. The account name associated with the transaction. 
                                                It will be "" for the default account.
    "address":"address",    (string) The bitcoin address of the transaction. Not present for 
                                                move transactions (category = move).
    "category":"send|receive|move", (string) The transaction category. 'move' is a local (off blockchain)
                                                transaction between accounts, and not associated with an address,
                                                transaction id or block. 'send' and 'receive' transactions are 
                                                associated with an address, transaction id and block details
    "amount": x.xxx,          (numeric) The amount in BTC. This is negative for the 'send' category, and for the
                                         'move' category for moves outbound. It is positive for the 'receive' category,
                                         and for the 'move' category for inbound funds.
    "label": "label",       (string) A comment for the address/transaction, if any
    "vout": n,                (numeric) the vout value
    "fee": x.xxx,             (numeric) The amount of the fee in BTC. This is negative and only available for the 
                                         'send' category of transactions.
    "confirmations": n,       (numeric) The number of confirmations for the transaction. Available for 'send' and 
                                         'receive' category of transactions. Negative confirmations indicate the
                                         transaction conflicts with the block chain
    "trusted": xxx,           (bool) Whether we consider the outputs of this unconfirmed transaction safe to spend.
    "blockhash": "hashvalue", (string) The block hash containing the transaction. Available for 'send' and 'receive'
                                          category of transactions.
    "blockindex": n,          (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive'
                                          category of transactions.
    "blocktime": xxx,         (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
    "txid": "transactionid", (string) The transaction id. Available for 'send' and 'receive' category of transactions.
    "time": xxx,              (numeric) The transaction time in seconds since epoch (midnight Jan 1 1970 GMT).
    "timereceived": xxx,      (numeric) The time received in seconds since epoch (midnight Jan 1 1970 GMT). Available 
                                          for 'send' and 'receive' category of transactions.
    "comment": "...",       (string) If a comment is associated with the transaction.
    "otheraccount": "accountname",  (string) DEPRECATED. For the 'move' category of transactions, the account the funds came 
                                          from (for receiving funds, positive amounts), or went to (for sending funds,
                                          negative amounts).
    "bip125-replaceable": "yes|no|unknown",  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                     may be unknown for unconfirmed transactions not in the mempool
    "abandoned": xxx          (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the 
                                         'send' category of transactions.
  }
]
```
#### Example
```
//request
curl --user bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listtransactions", "params": ["*", 20, 100] }' -H 'content-type: text/plain;' http://10.20.11.27:8332/

//result
{"result":[],"error":null,"id":"curltest"}
```

### <span id="listunspent">listunspent</span>
Returns array of unspent transaction outputs
with between minconf and maxconf (inclusive) confirmations.
Optionally filter to only include txouts paid to specified addresses.
#### Parameters
```
Arguments:
1. minconf          (numeric, optional, default=1) The minimum confirmations to filter
2. maxconf          (numeric, optional, default=9999999) The maximum confirmations to filter
3. "addresses"      (string) A json array of bitcoin addresses to filter
    [
      "address"     (string) bitcoin address
      ,...
    ]
4. include_unsafe (bool, optional, default=true) Include outputs that are not safe to spend
                  See description of "safe" attribute below.
5. query_options    (json, optional) JSON with query options
    {
      "minimumAmount"    (numeric or string, default=0) Minimum value of each UTXO in BTC
      "maximumAmount"    (numeric or string, default=unlimited) Maximum value of each UTXO in BTC
      "maximumCount"     (numeric or string, default=unlimited) Maximum number of UTXOs
      "minimumSumAmount" (numeric or string, default=unlimited) Minimum sum value of all UTXOs in BTC
    }
```
#### Returns
```
Result
[                   (array of json object)
  {
    "txid" : "txid",          (string) the transaction id 
    "vout" : n,               (numeric) the vout value
    "address" : "address",    (string) the bitcoin address
    "account" : "account",    (string) DEPRECATED. The associated account, or "" for the default account
    "scriptPubKey" : "key",   (string) the script key
    "amount" : x.xxx,         (numeric) the transaction output amount in BTC
    "confirmations" : n,      (numeric) The number of confirmations
    "redeemScript" : n        (string) The redeemScript if scriptPubKey is P2SH
    "spendable" : xxx,        (bool) Whether we have the private keys to spend this output
    "solvable" : xxx,         (bool) Whether we know how to spend this output, ignoring the lack of keys
    "safe" : xxx              (bool) Whether this output is considered safe to spend. Unconfirmed transactions
                              from outside keys and unconfirmed replacement transactions are considered unsafe
                              and are not eligible for spending by fundrawtransaction and sendtoaddress.
  }
  ,...
]
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [6, 9999999, [] , true, { "minimumAmount": 0.005 }] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":[{"txid":"7689e028f9b3368c81a834f1afba3951713e27d58c203c1052b5014cd8593405","vout":0,"address":"2MtTiF9Pg4C61pmSb6pGrVZ2NwDxmkPYtgL","redeemScript":"0014c51f2fe39b3c77c84f2967aef8b879469f063843","scriptPubKey":"a9140d54b4563f42213254838fcc8fddcf1e1ddf6dac87","amount":0.20208723,"confirmations":1645,"spendable":true,"solvable":true,"safe":true},{"txid":"7689e028f9b3368c81a834f1afba3951713e27d58c203c1052b5014cd8593405","vout":1,"address":"2MwMuc1SEHUdCcJrq7Mz9zZcV4xMHBZp5zk","account":"xxx","redeemScript":"00140be2155c06642751ec9a1e75df0f16304cf1b302","scriptPubKey":"a9142d24119167590cb23a930da58e6b60f991c257ae87","amount":0.30000000,"confirmations":1645,"spendable":true,"solvable":true,"safe":true},{"txid":"931d2d9578714988b881d9f0017289d44b4e6a848478b0ef1529bf68cb742f29","vout":1,"address":"2MwMuc1SEHUdCcJrq7Mz9zZcV4xMHBZp5zk","account":"xxx","redeemScript":"00140be2155c06642751ec9a1e75df0f16304cf1b302","scriptPubKey":"a9142d24119167590cb23a930da58e6b60f991c257ae87","amount":0.10000000,"confirmations":1645,"spendable":true,"solvable":true,"safe":true},{"txid":"f1b1ab345f6bb29bff0f7c1eb01bb3015ec84385c855555a69998538c8c2164f","vout":0,"address":"2N3dMFz2t3AG57xwaZX3gm9Fna1p9o8JwU8","account":"xzy","redeemScript":"0014bab5f45aab9b2caad5b223cd1d6c95dfd943d007","scriptPubKey":"a91471e07a6fa1383855c366405fee80fa97bf4aeb0487","amount":0.00500000,"confirmations":1667,"spendable":true,"solvable":true,"safe":true},{"txid":"c8e4d0f4f9db10e90873b595326a7c7f6cf1dd9350688d804220f966572f5b7c","vout":0,"address":"2NBEVML5bL77TNSLZnuSPkXuHPZNZb77NCd","redeemScript":"00146723822a250e30dd1f4141abd98273b2c9ba9ede","scriptPubKey":"a914c54eac236368fac3d880a7afaafed36669ce016187","amount":0.07918750,"confirmations":353,"spendable":true,"solvable":true,"safe":true},{"txid":"683ef8927f66040ca5114cd6320da0a0b3b29ea5b43915e37aafb10f4349858a","vout":0,"address":"mgnucj8nYqdrPFh2JfZSB1NmUThUGnmsqe","account":"","scriptPubKey":"76a9140dfc8bafc8419853b34d5e072ad37d1a5159f58488ac","amount":0.01000000,"confirmations":57430,"spendable":true,"solvable":true,"safe":true},{"txid":"955e161742995f45add62f385149e5e7cf420ef7917454b2eb934adab49bfaf3","vout":0,"address":"2MwMuc1SEHUdCcJrq7Mz9zZcV4xMHBZp5zk","account":"xxx","redeemScript":"00140be2155c06642751ec9a1e75df0f16304cf1b302","scriptPubKey":"a9142d24119167590cb23a930da58e6b60f991c257ae87","amount":0.10000000,"confirmations":1645,"spendable":true,"solvable":true,"safe":true},{"txid":"955e161742995f45add62f385149e5e7cf420ef7917454b2eb934adab49bfaf3","vout":1,"address":"2MyadDTC7wXc17CjEGqUJWRjdrRx9P5qxR3","redeemScript":"0014d2b15055cba615210918a5768d9e733ff5dc0145","scriptPubKey":"a914457c0c03ef56a2eab5c0656c7b90b464381a575787","amount":0.44922110,"confirmations":1645,"spendable":true,"solvable":true,"safe":true}],"error":null,"id":"curltest"}
```

### <span id="listwallets">listwallets</span>
Returns a list of currently loaded wallets.
For full information on the wallet, use "getwalletinfo"
#### Parameters
```
none
```
#### Returns
```
Result:
[                         (json array of strings)
  "walletname"            (string) the wallet name
   ...
]
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listwallets", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":["wallet.dat"],"error":null,"id":"curltest"}
```

### <span id="lockunspent">lockunspent</span>
Updates list of temporarily unspendable outputs.
Temporarily lock (unlock=false) or unlock (unlock=true) specified transaction outputs.
If no transaction outputs are specified when unlocking then all current locked transaction outputs are unlocked.
A locked transaction output will not be chosen by automatic coin selection, when spending bitcoins.
Locks are stored in memory only. Nodes start with zero locked outputs, and the locked output list
is always cleared (by virtue of process exit) when a node stops or fails.
Also see the listunspent call
#### Parameters
```
Arguments:
1. unlock            (boolean, required) Whether to unlock (true) or lock (false) the specified transactions
2. "transactions"  (string, optional) A json array of objects. Each object the txid (string) vout (numeric)
     [           (json array of json objects)
       {
         "txid":"id",    (string) The transaction id
         "vout": n         (numeric) The output number
       }
       ,...
     ]
```
#### Returns
```
Result:
true|false    (boolean) Whether the command was successful or not
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "lockunspent", "params": [false, "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":true,"error":null,"id":"curltest"}
```

### <span id="move">move</span>
DEPRECATED. Move a specified amount from one account in your wallet to another.
#### Parameters
```
Arguments:
1. "fromaccount"   (string, required) The name of the account to move funds from. May be the default account using "".
2. "toaccount"     (string, required) The name of the account to move funds to. May be the default account using "".
3. amount            (numeric) Quantity of BTC to move between accounts.
4. (dummy)           (numeric, optional) Ignored. Remains for backward compatibility.
5. "comment"       (string, optional) An optional comment, stored in the wallet only.
```
#### Returns
```
Result:
true|false           (boolean) true if successful.
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "move", "params": ["xxx", "xzy", 0.2] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":true,"error":null,"id":"curltest"}
```

### <span id="rescanblockchain">rescanblockchain</span>
Rescan the local blockchain for wallet related transactions.
#### Parameters
```
Arguments:
1. "start_height"    (numeric, optional) block height where the rescan should start
2. "stop_height"     (numeric, optional) the last block height that should be scanned
```
#### Returns
```
Result:
{
  "start_height"     (numeric) The block height where the rescan has started. If omitted, rescan started from the genesis block.
  "stop_height"      (numeric) The height of the last rescanned block. If omitted, rescan stopped at the chain tip.
}
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "rescanblockchain", "params": [100000, 120000] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":{"start_height":100000,"stop_height":120000},"error":null,"id":"curltest"}
```

### <span id="sendfrom">sendfrom</span>
DEPRECATED (use sendtoaddress). Sent an amount from an account to a bitcoin address.
Requires wallet passphrase to be set with walletpassphrase call.
#### Parameters
```
Arguments:
1. "fromaccount"       (string, required) The name of the account to send funds from. May be the default account using "".
                       Specifying an account does not influence coin selection, but it does associate the newly created
                       transaction with the account, so the account's balance computation and transaction history can reflect
                       the spend.
2. "toaddress"         (string, required) The bitcoin address to send funds to.
3. amount                (numeric or string, required) The amount in BTC (transaction fee is added on top).
4. minconf               (numeric, optional, default=1) Only use funds with at least this many confirmations.
5. "comment"           (string, optional) A comment used to store what the transaction is for. 
                                     This is not part of the transaction, just kept in your wallet.
6. "comment_to"        (string, optional) An optional comment to store the name of the person or organization 
                                     to which you're sending the transaction. This is not part of the transaction, 
                                     it is just kept in your wallet.
```
#### Returns
```
Result:
"txid"                 (string) The transaction id.
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendfrom", "params": ["", "2N6BjhgkJANxpcb5DFJdsQmsXGTS12wPkJs", 0.1] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":"fb62ea7ea2e2e051f5cc0670223e06c5c05cc5cb1e33c432f909a0234bf0d14c","error":null,"id":"curltest"}
```


### <span id="sendmany">sendmany</span>
Send multiple times. Amounts are double-precision floating point numbers.
Requires wallet passphrase to be set with walletpassphrase call.
#### Parameters
```
Arguments:
1. "fromaccount"         (string, required) DEPRECATED. The account to send the funds from. Should be "" for the default account
2. "amounts"             (string, required) A json object with addresses and amounts
    {
      "address":amount   (numeric or string) The bitcoin address is the key, the numeric amount (can be string) in BTC is the value
      ,...
    }
3. minconf                 (numeric, optional, default=1) Only use the balance confirmed at least this many times.
4. "comment"             (string, optional) A comment
5. subtractfeefrom         (array, optional) A json array with addresses.
                           The fee will be equally deducted from the amount of each selected address.
                           Those recipients will receive less bitcoins than you enter in their corresponding amount field.
                           If no addresses are specified here, the sender pays the fee.
    [
      "address"          (string) Subtract fee from this address
      ,...
    ]
6. replaceable            (boolean, optional) Allow this transaction to be replaced by a transaction with higher fees via BIP 125
7. conf_target            (numeric, optional) Confirmation target (in blocks)
8. "estimate_mode"      (string, optional, default=UNSET) The fee estimate mode, must be one of:
       "UNSET"
       "ECONOMICAL"
       "CONSERVATIVE"
```
#### Returns
```
Result:
"txid"                   (string) The transaction id for the send. Only 1 transaction is created regardless of 
                                    the number of addresses.
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendmany", "params": ["", {"2N6BjhgkJANxpcb5DFJdsQmsXGTS12wPkJs":0.01,"2NEXR8XNgjhy3ZZPi1CxHSnEWL7qzNiy3ob":0.02}, 6, "testing"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":"9794b0438c0d3586cecd74c3a89d1e5aa2c9fff8a7caab2d40a33d5db6b03348","error":null,"id":"curltest"}
```

### <span id="sendtoaddress">sendtoaddress</span>
Send an amount to a given address.

Requires wallet passphrase to be set with walletpassphrase call.
#### Parameters
```
Arguments:
1. "address"            (string, required) The bitcoin address to send to.
2. "amount"             (numeric or string, required) The amount in BTC to send. eg 0.1
3. "comment"            (string, optional) A comment used to store what the transaction is for. 
                             This is not part of the transaction, just kept in your wallet.
4. "comment_to"         (string, optional) A comment to store the name of the person or organization 
                             to which you're sending the transaction. This is not part of the 
                             transaction, just kept in your wallet.
5. subtractfeefromamount  (boolean, optional, default=false) The fee will be deducted from the amount being sent.
                             The recipient will receive less bitcoins than you enter in the amount field.
6. replaceable            (boolean, optional) Allow this transaction to be replaced by a transaction with higher fees via BIP 125
7. conf_target            (numeric, optional) Confirmation target (in blocks)
8. "estimate_mode"      (string, optional, default=UNSET) The fee estimate mode, must be one of:
       "UNSET"
       "ECONOMICAL"
       "CONSERVATIVE"
```
#### Returns
```
Result:
"txid"                  (string) The transaction id.
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendtoaddress", "params": ["2N6BjhgkJANxpcb5DFJdsQmsXGTS12wPkJs", 0.1] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":"22c0cef6035a0556958ded565afa12a70a569e29d56fe37e88fd3f8a816dfe52","error":null,"id":"curltest"}
```

### <span id="setaccount">setaccount</span>
DEPRECATED. Sets the account associated with the given address.
#### Parameters
```
Arguments:
1. "address"         (string, required) The bitcoin address to be associated with an account.
2. "account"         (string, required) The account to assign the address to.
```
#### Returns
```
none
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setaccount", "params": ["2N6BjhgkJANxpcb5DFJdsQmsXGTS12wPkJs", "xxx"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="settxfee">settxfee</span>
Set the transaction fee per kB. Overwrites the paytxfee parameter.
#### Parameters
```
Arguments:
1. amount         (numeric or string, required) The transaction fee in BTC/kB
```
#### Returns
```
Result
true|false        (boolean) Returns true if successful
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "settxfee", "params": [0.00001] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":true,"error":null,"id":"curltest"}
```

### <span id="signmessage">signmessage</span>
Sign a message with the private key of an address
Requires wallet passphrase to be set with walletpassphrase call.
#### Parameters
```
Arguments:
1. "address"         (string, required) The bitcoin address to use for the private key.
2. "message"         (string, required) The message to create a signature of.
```
#### Returns
```
Result:
"signature"          (string) The signature of the message encoded in base 64
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signmessage", "params": ["2N6BjhgkJANxpcb5DFJdsQmsXGTS12wPkJs", "hello world"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":"ILypRih424AWRYXK1goB6mskx99aelWcVCTEKolaW7U4VPnwj6Khf+vJSED7pMtPQd3KnXuqq1JvavrQdPMFFB0=","error":null,"id":"curltest"}
```

### <span id="walletlock">walletlock</span>
Removes the wallet encryption key from memory, locking the wallet.
After calling this method, you will need to call walletpassphrase again
before being able to call any methods which require the wallet to be unlocked.
#### Parameters
```
none
```
#### Returns
```
none
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "walletlock", "params": [] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
成功，没有打印
```

### <span id="walletpassphrase">walletpassphrase</span>
Stores the wallet decryption key in memory for 'timeout' seconds.
This is needed prior to performing transactions related to private keys such as sending bitcoins
#### Parameters
```
Arguments:
1. "passphrase"     (string, required) The wallet passphrase
2. timeout            (numeric, required) The time to keep the decryption key in seconds. Limited to at most 1073741824 (2^30) seconds.
                                          Any value greater than 1073741824 seconds will be set to 1073741824 seconds.
```
#### Returns
```
none
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "walletpassphrase", "params": ["123456", 30] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":null,"error":null,"id":"curltest"}
```

### <span id="walletpassphrasechange">walletpassphrasechange</span>
Changes the wallet passphrase from 'oldpassphrase' to 'newpassphrase'.
#### Parameters
```
Arguments:
1. "oldpassphrase"      (string) The current passphrase
2. "newpassphrase"      (string) The new passphrase
```
#### Returns
```
null
```
#### Example
```
//request
curl --user test-bitcoinrpc --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "walletpassphrasechange", "params": ["123456", "12345678"] }' -H 'content-type: text/plain;' http://10.20.11.27:18332/

//result
{"result":null,"error":null,"id":"curltest"}
```
