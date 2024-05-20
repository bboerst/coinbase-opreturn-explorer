# coinbase `OP_RETURN` explorer
View this at: https://opreturn.live/

Bitcoin miners can sometimes include data within the coinbase transaction of a block by using an `OP_RETURN` transaction output. You can see this data yourself by:
1. Visi any block explorer (ex: https://mempool.space/)
1. Click on a recently mined block
1. Look at the first transaction in the block, which is also known as the `coinbase` transaction.
1. Click on the transaction ID for the coinbase transaction and look at the transaction outputs. Most (not all) transactiions will have 1 or more `OP_RETURN` outputs.

Sometimes, you'll see an `OP_RETURN` that looks like `RSKBLOCK:1r%^ *2#2  *^$` or `CORE#2( ^aa`. These _look_ unreadable because it's typical in block explorers to convert the script (hex) into ASCII. But each of these `OP_RETURN`s actually follow a spec and can be decoded into something that makes sense rather than ASCII text. For example, `OP_RETURN`s that start with `RSKBLOCK` are for Rootstock merged mining and it's a way for a miner to perform work against two block chains at once.

The overall goal of this project is to decode and display `OP_RETURN` data so that anyone can understand what other entities are associated with a block being mined by a pool.

![image](https://github.com/bboerst/merged-mining-explorer/assets/1393271/a713e796-967c-4576-8d78-c1c73cfdf508)

Currently being tracked:
## `CORE`
- Link: https://coredao.org/
- Spec: https://github.com/coredao-org/docs/blob/main/docs/become-a-delegator/delegators/delegating-hash.md#implementation

### Summary
If anyone can explain this, please open a PR with details.

## `RSKBLOCK`
- Link: https://rootstock.io/
- Spec: https://dev.rootstock.io/rsk/architecture/mining/implementation-guide/

### Summary
If anyone can explain this, please open a PR with details.

## Witness data
- Spec: https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/ts_src/block.ts#L106-L109

### Summary
The merkle root for the witness data is in an OP_RETURN output.

https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/ts_src/block.ts#L106-L109
