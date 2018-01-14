# Section 3

- go-ethereum (geth)
  - Connect to other nodes, start to download blocks
    - Full sync (Block Headers + Block bodies and All historical transactions) ~ 35 GB => Days to Finish
    - Fast sync (Block Headers + Block bodies, Last 1024 transactions, Downloads all blocks) => Hours to Finish
    - Light sync (Only Headers, takes the latest "snapshot"), less secure but mush faster => Minutes to Finish
  - JavaScript JSON RPC(IPC or RPC over HTTP)
  - Web3.js, truffle, Testrpc, Mist, Truffle Console, Remix

## Install Geth

- `sudo apt-get install software-properties-common`
- `sudo add-apt-repository -y ppa:ethereum/ethereum`
- `sudo apt-get update`
- `sudo apt-get install ethereum`

## Runnning Ethereum

- Run `geth` first time start to download blocks in Fast Syn,x after that start in Full Sync
- After installing, run `geth account new` to create an account on your node.
- Default folder `~/.ethereum`, `~/Library/Ethereum` or `~/AppData/Roaming/Ethereum`
  - /geth
    - /chaindata
    - /nodes
  - /keystore
  - /rinkeby
    - /geth
    - /keystore

PrivateKey File: UTC--2018-01-14T02-34-55.551298829Z--f01f18d192c46c486418ed577501e2bc9d8c926b

```bash
WARN [01-13|23:58:06] No etherbase set and no accounts found as default
INFO [01-13|23:58:06] Starting peer-to-peer node               instance=Geth/v1.7.3-stable-4bb3c89d/linux-amd64/go1.9.1
INFO [01-13|23:58:06] Allocated cache and file handles         database=/home/andre/.ethereum/geth/chaindata cache=128 handles=1024
INFO [01-13|23:58:06] Initialised chain configuration          config="{ChainID: 1 Homestead: 1150000 DAO: 1920000 DAOSupport: true EIP150: 2463000 EIP155: 2675000 EIP158: 2675000 Byzantium: 4370000 Engine: ethash}"
INFO [01-13|23:58:06] Disk storage enabled for ethash caches   dir=/home/andre/.ethereum/geth/ethash count=3
INFO [01-13|23:58:06] Disk storage enabled for ethash DAGs     dir=/home/andre/.ethash               count=2
INFO [01-13|23:58:06] Initialising Ethereum protocol           versions="[63 62]" network=1
INFO [01-13|23:58:06] Loaded most recent local header          number=169298 hash=3cce7f…207d5d td=536683266077988324
INFO [01-13|23:58:06] Loaded most recent local full block      number=0      hash=d4e567…cb8fa3 td=17179869184
INFO [01-13|23:58:06] Loaded most recent local fast block      number=164598 hash=be0021…6c8b8c td=503567053387950506
INFO [01-13|23:58:06] Upgrading chain index                    type=bloombits percentage=48
INFO [01-13|23:58:06] Loaded local transaction journal         transactions=0 dropped=0
INFO [01-13|23:58:06] Regenerated local transaction journal    transactions=0 accounts=0
INFO [01-13|23:58:06] Starting P2P networking
```

- ChainID 1, 2 and 3 are reserved for Main and Test Networks
- IPC file

## JavaScript JSON-API

- [https://github.com/ethereum/go-ethereum/wiki/Management-APIs](https://github.com/ethereum/go-ethereum/wiki/Management-APIs)
- [https://github.com/ethereum/wiki/wiki/JSON-RPC](https://github.com/ethereum/wiki/wiki/JSON-RPC)

- `geth attach`
- `geth attach /home/andre/.ethereum/geth.ipc`
- `personal.newAccount()`
- `eth.syncing`

## Types of Blockchains

- Public Blockchains
  - Everybody can participate, mine, read data, send transactions
  - Equally
  - (Main Net): Cost money
  - (Test Net): Don't cost money, for testing

- Consortium Blockchains
  - Everybody can participate
  - Only few are miners
  - Limited authority in the network

- Private Blockchains
  - You are the only one
  - Nobody else gets access

## Genesis File

```json
{
  "config": {
    "chainId": 15,
    "homesteadBlock": 0,
    "eip155Block": 0,
    "eip158Block": 0
  },
  "difficulty": "0x20000",
  "gasLimit": "0x8000000",
  "alloc": {}
}
```

## Creating a Private Network

- `geth init genesis.json --datadir chaindata`
- `geth --datadir chaindata`
- `geth --datadir chaindata --nodiscover`
- `geth attach ipc:/home/andre/studies/udemy/ethereum-blockchain-developer/section-03/chaindata/geth.ipc`

- `eth.accounts`
- `personal.newAccount()`

## Start mining on Private Network

- `eth.coinbase`
- `miner`
- `miner.setEtherbase(eth.accounts[0])`
- `miner.start(1)`
- `web3.eth.getBalance(eth.accounts[0])`
- `web3.fromWei(eth.getBalance(eth.accounts[0]), "ether")`
- `web3.fromWei(eth.getBalance(eth.accounts[0]), "finney")`
- `geth --datadir chaindata --nodiscover --unlock 0 --mine 1`