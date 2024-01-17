# Onion Tabo Blockchain Explorer


## JSON API


#### api/transaction/<tx_hash>

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/transaction/8310b17460112fcedd9191896dd88296371e2a143e006aeeb7098b76c54b0ca2"
```

#### api/transactions

Transactions in last 25 blocks


```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/transactions"
```

#### api/transactions?page=<page_no>&limit=<tx_per_page>


```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/transactions?page=2&limit=10"
```

Result analogical to the one above.

#### api/block/<block_number|block_hash>


```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/block/1293"
```

#### api/mempool

Return all txs in the mempool.

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/mempool"
```


Limit of 100000000 is just default value above to ensure that all mempool txs are fetched
if no specific limit given.

#### api/mempool?limit=<no_of_top_txs>

Return number of newest mempool txs, e.g., only 10.

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/mempool?limit=10"
```

Result analogical to the one above.

#### api/search/<block_number|tx_hash|block_hash>

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/search/1293"
```


#### api/outputs?txhash=<tx_hash>&address=<address>&viewkey=<viewkey>&txprove=<0|1>

For `txprove=0` we check which outputs belong to given address and corresponding viewkey.
For `txprove=1` we use to prove to the recipient that we sent them founds.
For this, we use recipient's address and our tx private key as a viewkey value,
 i.e., `viewkey=<tx_private_key>`

Checking outputs:

```bash

curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/outputs?txhash=4ff838682d9e47cb44b406f804251224ae1a6b1ac8ef71f3fa70928026c46e95&address=taboaddress&viewkey=taboviewkey&txprove=0"
```


Proving transfer:

We use recipient's address (i.e. not our address from which we sent tabo to recipient).
For the viewkey, we use `tx_private_key` (although the GET variable is still called `viewkey`) that we obtained by sending this txs.

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/outputs?txhash=4ff838682d9e47cb44b406f804251224ae1a6b1ac8ef71f3fa70928026c46e95&address=taboaddress&viewkey=taboviewkey&txprove=1"
```



Result analogical to the one above.

#### api/networkinfo

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/networkinfo"
```

#### api/outputsblocks

Search for our outputs in last few blocks (up to 5 blocks), using provided address and viewkey.


```bash
curl  -w "\n" -X GET https://explorer2.taboprotocol.tech/api/outputsblocks?address=taboaddress&viewkey=taboviewkey&limit=5&mempool=1
```



#### api/emission

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/emission"
```


#### api/version

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/version"
```

api number is store as `uint32_t`. In this case `65536` represents
major version 1 and minor version 0.
In JavaScript to get these numbers, one can do as follows:

```javascript
var api_major = response.data.api >> 16;
var api_minor = response.data.api & 0xffff;
```

#### api/rawblock/<block_number|block_hash>

Return raw json block data.

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/rawblock/1293"
```


#### api/rawtransaction/<tx_hash>

Return raw json tx data.

```bash
curl  -w "\n" -X GET "https://explorer2.taboprotocol.tech/api/rawtransaction/4ff838682d9e47cb44b406f804251224ae1a6b1ac8ef71f3fa70928026c46e95"
```
