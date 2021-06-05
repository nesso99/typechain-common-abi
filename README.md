# typechain common abi

common smart contracts in typechain

## Typescript!

_note: example is copied from [docs](https://github.com/UMAprotocol/protocol/blob/master/packages/core/README.md)_

In addition to the above import styles, you can import typescript types for truffle, ethers, and web3. Because of existing
limitations in typechain the import style for each of these is slightly different.

Note: this is a work in progress and the typescript API will likely change and improve in the future.

### Ethers

The best support is for Ethers contract types. To construct an Ethers contract in node, simply import from the ethers factories:

```ts
import { EthersContracts } from "typechain-common-abi"
const provider = new ethers.providers.JsonRpcProvider(RPC_HOST)
const tokenInstance = EthersContracts.WETH9_factory.connect(TOKEN_ADDRESS, provider)

// Raw type rather than the factory.
import type { EthersContracts } from "typechain-common-abi"
const { WETH9 } = EthersContracts
```

### Truffle

Truffle has well-defined contract types as well, but there are no built-in truffle factories.

```ts
import type { TruffleContracts } from "@uma/core/contract-types/truffle"
import * as Web3 from 'web3'
const contract = require("@truffle/contract");

const { WETH9Instance, WETH9Contract } = TruffleContracts
const provider = new Web3.providers.HttpProvider("http://localhost:8545")

const WETH9 = contract({
  abi: ...,
  unlinked_binary: ...,
  address: ..., // optional
  // many more
}).setProvider(provider) as WETH9Contract
const weth9 = WETH9.deployed() // Should be a WETH9Instance.
```

### Web3

Web3 types can't be imported directly from the index file. However, if you are able to import via path, you can import
this way:

```ts
import type { WETH9 } from "typechain-common-abi/contract-types/web3/WETH9"

const weth9 = new web3.eth.Contract(WETH9_ABI, WETH9_ADDRESS) as WETH9
```