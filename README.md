# Polar-mempool

Adds mempool.space webapp to a local polar regtest environment

## Prerequisites

- install docker
- install docker-compose
- install https://github.com/jamaljsr/polar
- setup a local testnet with at least one bitcoin-node

Note
If you have more than one local testnets, you can specify the network by changing it in the docker-compose.yml file. By default the first polar-network-1_default ist used.

## Usage

```
git clone https://github.com/ngutech21/polar-mempool.git
cd polar-mempool
docker-compose up -d
open browser at http://localhost:8080

```

## Fix

### CORE_RPC_HOST
```
# ifconfig
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
```

### network
```
docker network create polar-network-1_default
```

### run
```
./restart_bitcoind
docker-compose up -f ./docker-compose-getumbrel:electrs.yml
```

## mempool + esplora
更换为支持 UTXO 查询的后端：

https://blockstream.info/ （`@mempool/mempool.js` 支持该hostname）

https://github.com/Blockstream/esplora

API: https://github.com/Blockstream/esplora/blob/master/API.md
```
rm -rf ./data_bitcoin_regtest # 如果你想清除旧区块链
docker rm -f btc
./esplora

./btc getblockcount
./rm_docker
docker-compose up
```

尝试访问:

http://127.0.0.1:8080/api/address/bcrt1q99ucxl2nnjcaw8vaet2vlzsyjvmhd5jj805587

http://127.0.0.1:8080/api/address/bcrt1q99ucxl2nnjcaw8vaet2vlzsyjvmhd5jj805587/utxo (404 Not Found)

http://127.0.0.1:8888/regtest/api/address/bcrt1q99ucxl2nnjcaw8vaet2vlzsyjvmhd5jj805587/utxo (esplora API)
