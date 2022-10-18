---
meta:
  - name: description
    content: eth_getBlockByNumber JSON-RPC method details and code examples.
  - name: keywords
    content: json rpc methods curl api web3.py web3.js eth.rb javascript python ruby ethereum
---

# Ethereum eth_getBlockByNumber RPC method

Ethereum API method that returns information about the block matching the given block number.

**Parameters:**

* `quantity or tag` - Integer block number, or the string:
    * `latest` — the latest block that is to be validated. The Beacon Chain may reorg and the latest block can become orphaned.
    * `safe` — the block that is equal to the tip of the chain and is very unlikely to be orphaned.
    * `finalized` — the block that is accepted by the two thirds of the Ethereum validators.
    * `earliest` — the genesis block.
    * `pending` — the pending state and transactions block.
* `boolean` - If `True`, it returns the full transaction objects. If `False`, only the hashes of the transactions.

**Returns:**

* `object` - A block object, or `null` when no block was found.
  * `number` - The block number of the requested block. Encoded as hexadecimal. `null` if pending.
  * `hash` - The block hash of the requested block. `null` if pending.
  * `parenthash` - Hash of the parent block.
  * `nonce` - Hash of the generated proof-of-work. `null` if pending.
  * `sha3uncles` - SHA3 of the uncles' data in the block.
  * `logsbloom` - The bloom filter for the logs of the block. `null` if pending.
  * `transactionsroot` - The root of the transaction trie of the block.
  * `stateroot` - The root of the final state trie of the block.
  * `receiptsroot` - The root of the receipts trie of the block.
  * `miner` - The address to whom the mining rewards were given.
  * `difficulty` - Integer of the difficulty for this block, encoded as hexadecimal.
  * `totaldifficulty` - Integer of the total difficulty of the chain until this block, encoded as hexadecimal.
  * `extradata` - The “extra data” field of this block.
  * `size` - The size of this block in bytes as an Integer value, encoded as hexadecimal.
  * `gaslimit` - The maximum gas allowed in this block, encoded as hexadecimal.
  * `gasused` - The total used gas by all transactions in this block. Encoded as hexadecimal.
  * `timestamp` - The UNIX timestamp for when the block was collated.
  * `transactions` - Array of transaction objects - please see [eth_getTransactionByHash](/api/ethereum/eth_gettransactionbyhash) for exact shape.
  * `uncles` - Array of uncle hashes.

**Example:**

::: tip
cURL needs a `HEX String` starting with `0x` to identify the block if you want to use a hex integer block number as a parameter.
For example, block number `14000000` will be `0xD59F80`.
:::

<CodeSwitcher :languages="{js:'web3.js', py:'web3.py', rb:'eth.rb', cr:'cURL'}">
<template v-slot:js>

```js
const Web3 = require("web3");
const node_url = "CHAINSTACK_NODE_URL";
const web3 = new Web3(node_url);
web3.eth.getBlock("latest", "False", (err, block) => {
  console.log(block);
});
```

</template>
<template v-slot:py>

```py
from web3 import Web3
node_url = "CHAINSTACK_NODE_URL"
web3 = Web3(Web3.HTTPProvider(node_url))
print(web3.eth.get_block("latest", False))
```

</template>
<template v-slot:rb>

```rb
require "eth"
client = Eth::Client.create "CHAINSTACK_NODE_URL"
response = client.eth_get_block_by_number("latest",false)
puts response["result"]
```

</template>
<template v-slot:cr>

```sh
curl -X POST "CHAINSTACK_NODE_URL" \
  -H "Content-Type: application/json" \
  --data '{"method":"eth_getBlockByNumber","params":["latest",false],"id":1,"jsonrpc":"2.0"}'
```

</template>
</CodeSwitcher>