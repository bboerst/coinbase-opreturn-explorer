# coinbase `OP_RETURN` explorer
View this at: https://opreturn.live/

## Overview
Bitcoin miners can sometimes include data within the coinbase transaction of a block by using an `OP_RETURN` transaction output.

The overall goal of this project is to decode and display `OP_RETURN` data so that anyone can understand what other entities are associated with a block being mined by a pool.

## What are we decoding?
Take a look at an example `coinbase` transaction: <a href="https://mempool.space/tx/bbc74341be5a5b89ef876540453fd97acd6bab414612a37364b359ca9aa9e677" target="_blank">https://mempool.space/tx/bbc74341be5a5b89ef876540453fd97acd6bab414612a37364b359ca9aa9e677</a>

Look at the Inputs & Outputs section and notice that there are some outputs called `OP_RETURN` with a `0` BTC amount.

In this case, you see 3 `OP_RETURN` outputs:

0. `OP_RETURN` `!D&'u39 q#me r/`
1. `OP_RETURN` `COREd$b-(N>,KT2+0`
2. `OP_RETURN` `RSKBLOCK:K__mu-^Y\Bua`

These _look_ like a bunch of gibberish because it's typical in block explorers to convert the actual script (stored in hex) into ASCII to make it readable by humans. But each of these `OP_RETURN`s actually _mean something_ and they typically follow a spec and they can be decoded into something that makes sense rather than ASCII text.

Go back to the mempool.space coinbase transaction page from above and click the "Details" button. Find the same 3 `OP_RETURN` outputs on the right and look at the `ScriptPubKey (HEX)` field. This is the actual script that the miner adds to the transaction that contains the data and this is what we decode in this project.

Here are the the decoded `OP_RETURN`s from the above transaction.

<img width="412" alt="image" src="https://github.com/bboerst/coinbase-opreturn-explorer/assets/1393271/abf9bfd3-440d-4d2e-8465-e0e1c4a3d35a">

Notice that `OP_RETURN` #1 contains the merkle root of some transaction witness data. `OP_RETURN` #2 is for merged mining with coredao.org and we're able to decode the details and see which validator they are staking with as well as the rewards address. `OP_RETURN` #3 is for merged mining with rootstock.io and the data includes the associated "Merged Mining" hash, which can be cross-referenced in the https://explorer.rootstock.io/ block explorer.

**Check out specific implementations details below to see how each of these are decoded.**

## Implementation Details

### `CORE`
- Link: https://coredao.org/
- Spec: https://github.com/coredao-org/docs/blob/main/docs/become-a-delegator/delegators/delegating-hash.md#implementation

#### Summary
If anyone can explain this, please open a PR with details.

---
### `RSKBLOCK`
- Link: https://rootstock.io/
- Spec: https://dev.rootstock.io/rsk/architecture/mining/implementation-guide/

#### Summary
If anyone can explain this, please open a PR with details.

---
### Witness data
- Spec: https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/ts_src/block.ts#L106-L109

#### Summary
The merkle root for the witness data is in an OP_RETURN output.
