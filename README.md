# -graphprotocol-testnet-range



<strong>Allocation</strong>
(https://github.com/StakeSquid/graphprotocol-testnet-docker/blob/master/docs/pre-requisites.md)


![photo_2022-10-06_15-46-50](https://user-images.githubusercontent.com/100018176/194316382-de3deeac-f3c0-4463-95be-be76f2770cdc.jpg)

<strong>Operator's wallet</strong>

![photo_2022-10-06_15-46-46](https://user-images.githubusercontent.com/100018176/194316532-f0e3941d-2af8-4ba4-ba25-410bdceb04c3.jpg)


both wallets are replenished with goerli eth
to make an allocation, we request test GST in the discord 



<br>
<strong>Installation</strong>

On a fresh Ubuntu server login via ssh and execute the following commands:

```
apt update -y && apt upgrade -y && apt autoremove -y
```
```
apt install docker.io docker-compose golang-go build-essential bc git curl httpie jq nano wget bsdmainutils base58 netcat net-tools libsecret-1-dev python2.7 clang cmake -y
```
```
go get github.com/a8m/envsubst/cmd/envsubst
```

NPM (through Node Version Manager)
Uncomplicated Firewall (ufw)
pino-pretty
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

# restart or open a new shell/terminal

nvm install node

# restart or open a new shell/terminal

npm install -g pino-pretty

apt install ufw
```

Install from scratch
Run the following commands to clone the repository and set everything up:

```
git clone git@github.com:StakeSquid/graphprotocol-testnet-docker.git
cd graphprotocol-testnet-docker
git submodule init
git submodule update
git config --global user.email "you@example.com"
git config --global user.name "Example User"
git branch --set-upstream-to=origin
```
Creating four domain names

Configure the environment variables
Edit the file called .env and add your values to the following envs:
Filling in the file (by lines):

1. Your email

2. INDEX_HOST, QUERY_HOST, GRAFANA_HOST, PROMETHEUS_HOST

3. we write the name and password (I used the same)

4. CHAIN_0_NAME "gnosis"

5. CHAIN_0_RPC - gnosis rpc

6. TXN_RPC - goerli rpc

7. OPERATOR_SEED_PHRASE - mnemonic phrase of the operator's wallet

8. STAKING_WALLET - the address of the wallet from which GRT is delegated

9. GEO_COORDINATES - server coordinates

```
EMAIL=email@sld.tld
INDEX_HOST=index.sld.tld
QUERY_HOST=query.sld.tld
GRAFANA_HOST=dashboard.sld.tld
ADMIN_USER=your_user
ADMIN_PASSWORD=your_password
DB_USER=your_db_user
DB_PASS=your_db_password
GRAPH_NODE_DB_NAME=your_graphnode_db_name
AGENT_DB_NAME=your_agent_db_name
CHAIN_0_NAME="network-name"
CHAIN_0_RPC="http://ip:port"
TXN_RPC="http://ip:port"
OPERATOR_SEED_PHRASE="12 or 15 word mnemonic"
STAKING_WALLET_ADDRESS=0xAdDreSs
GEO_COORDINATES='69.420 69.420'
INDEXER_AGENT_OFFCHAIN_SUBGRAPHS=""


#The following ENV vars are optional
#they need to be added above the last line

#QUERY_FEE_REBATE_CLAIM_THRESHOLD=number-in-grt \
#REBATE_CLAIM_BATCH_THRESHOLD=number-in-grt \
#NETWORK_SUBGRAPH_DEPLOYMENT=QmTePWCvPedmVxAvPnDFmFVxxYNW73z6xisyKCL2xa5P6e \
#INDEXER_AGENT_OFFCHAIN_SUBGRAPHS="Qm,Qm,Qm" \
#GRAPHNODE_LOGLEVEL=warn \
#ETHEREUM_TRACE_STREAM_STEP_SIZE=100 \
#ETHEREUM_BLOCK_BATCH_SIZE=50 \
#ETHEREUM_RPC_MAX_PARALLEL_REQUESTS=128 \
#GRAPH_ETHEREUM_MAX_BLOCK_RANGE_SIZE=1000 \
#GRAPH_ETHEREUM_TARGET_TRIGGERS_PER_BLOCK_RANGE=500 \
#INDEXER_AGENT_GAS_PRICE_MAX=gas-price-in-gwei \
```

My .env

![Screenshot_8](https://user-images.githubusercontent.com/100018176/194326600-874fee81-0028-4751-b4bc-2a29c90b4598.png)




<strong>Changing the version of Docker from 0.20.3 to 0.19.3</strong>

![Screenshot_4](https://user-images.githubusercontent.com/100018176/194321795-222fe19c-8c27-4e47-8288-3d96a70638c1.png)


<strong>Start</strong>

```
bash start
```

We are waiting for 20 synchronization steps...

In case something goes wrong
```
bash start --force-recreate
```
Further commands
```
curl --location --request POST 'index-node-0:8020' \
--header 'Content-Type: application/json' \
--data-raw '{"method":"subgraph_create","jsonrpc":"2.0","params":{"name":"Sushiswap-Gnosis"},"id":""}'
```
```
curl --location --request POST 'index-node-0:8020' \
--header 'Content-Type: application/json' \
--data-raw '{"method":"subgraph_deploy","jsonrpc":"2.0","params":{"name":"Sushiswap-Gnosis","ipfs_hash":"QmW8Cbb2R4ZHWGsrYjNJKRjoKKcPeDTNK6rdipfQQaAhd6"},"id":""}'
```
```
curl --location --request POST 'index-node-0:8020' \
--header 'Content-Type: application/json' \
--data-raw '{"method":"subgraph_create","jsonrpc":"2.0","params":{"name":"Connext-NXTPv1-Gnosis"},"id":""}'
```
```
curl --location --request POST 'index-node-0:8020' \
--header 'Content-Type: application/json' \
--data-raw '{"method":"subgraph_deploy","jsonrpc":"2.0","params":{"name":"Connext-NXTPv1-Gnosis","ipfs_hash":"QmWq1pmnhEvx25qxpYYj9Yp6E1xMKMVoUjXVQBxUJmreSe"},"id":""}'
```
```
curl --location --request POST 'index-node-0:8020' \
--header 'Content-Type: application/json' \
--data-raw '{"method":"subgraph_create","jsonrpc":"2.0","params":{"name":"1Hive-GardenGC"},"id":""}'
```
```
curl --location --request POST 'index-node-0:8020' \
--header 'Content-Type: application/json' \
--data-raw '{"method":"subgraph_deploy","jsonrpc":"2.0","params":{"name":"1Hive-GardenGC","ipfs_hash":"QmSqJEGHp1PcgvBYKFF2u8vhJZt8JTq18EV7mCuuZZiutX"},"id":""}'
```
```
curl --location --request POST 'index-node-0:8020' \
--header 'Content-Type: application/json' \
--data-raw '{"method":"subgraph_create","jsonrpc":"2.0","params":{"name":"Giveth-Economy-Gnosis"},"id":""}'
```
```
curl --location --request POST 'index-node-0:8020' \
--header 'Content-Type: application/json' \
--data-raw '{"method":"subgraph_deploy","jsonrpc":"2.0","params":{"name":"Giveth-Economy-Gnosis","ipfs_hash":"QmeVXKzGKSyfEQib4MzeZveJgDYJCYDMMHc1pPevWeSbsq"},"id":""}'
```

```
graph indexer rules set QmW8Cbb2R4ZHWGsrYjNJKRjoKKcPeDTNK6rdipfQQaAhd6 allocationAmount 300 parallelAllocations 1 decisionBasis always
```
```
graph indexer rules set QmeVXKzGKSyfEQib4MzeZveJgDYJCYDMMHc1pPevWeSbsq allocationAmount 300 parallelAllocations 1 decisionBasis always
```
```
graph indexer rules set QmWq1pmnhEvx25qxpYYj9Yp6E1xMKMVoUjXVQBxUJmreSe allocationAmount 300 parallelAllocations 1 decisionBasis always
```
```
graph indexer rules set QmSqJEGHp1PcgvBYKFF2u8vhJZt8JTq18EV7mCuuZZiutX allocationAmount 300 parallelAllocations 1 decisionBasis always
```

After that, everything should work.


In my case, I get an error. My allocation is not displayed.

![photo_2022-10-06_16-21-03](https://user-images.githubusercontent.com/100018176/194323841-c11a750f-2ff8-4047-b025-9d0b6b366a32.jpg)

Transactions on my operator's wallet do not pass.

Status Graph Indexer 

![Screenshot_5](https://user-images.githubusercontent.com/100018176/194324317-dcd6ce93-6603-492e-9394-201ef76471ab.png)

logs -f indexer-agent

![Screenshot_6](https://user-images.githubusercontent.com/100018176/194324727-bbcc9adb-f62e-4eeb-8e33-97a120f7d43e.png)

 docker logs -f indexer-service

![Screenshot_7](https://user-images.githubusercontent.com/100018176/194324985-94ae1a5f-52e5-4116-993f-b3d14a085488.png)

I need to understand the next steps. In my case, there were several reinstallations to different servers. The server is used by Hetzner AX-41

Here is the proposed solution! Thank you for your help!

```
SUBGRAPH_ENDPOINT="https://api.thegraph.com/subgraphs/name/graphprotocol/graph-network-goerli"
INDEXER_SERVICE_NETWORK_SUBGRAPH_ENDPOINT="https://api.thegraph.com/subgraphs/name/graphprotocol/graph-network-goerli"
INDEXER_AGENT_NETWORK_SUBGRAPH_ENDPOINT="https://api.thegraph.com/subgraphs/name/graphprotocol/graph-network-goerli"
```
