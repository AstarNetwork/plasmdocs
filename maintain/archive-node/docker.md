# Docker

## Using Docker

Running a node on one of Astar’s chains allows you to connect to the network, sync with our parachain and relay chain, obtain access to RPC endpoints, and much more.

### Installation Instructions

A node can be spun up quickly using [Docker](https://docs.docker.com/get-docker/). When connecting to Shiden on Kusama or Astar on Polkadot, it will take a few days to completely sync the relay chain. If you want to move faster you can use Kusama or Polkadot snapshots. ([How to install Docker on Ubuntu](https://linuxize.com/post/how-to-install-and-use-docker-on-ubuntu-20-04/))

Create a local directory to store the chain data:

{% tabs %}
{% tab title="Astar" %}
```
mkdir /var/lib/astar/astar-db
```
{% endtab %}

{% tab title="Shiden" %}
```
mkdir /var/lib/astar/shiden-db
```
{% endtab %}

{% tab title="Shibuya" %}
```
mkdir /var/lib/astar/shibuya-db
```
{% endtab %}
{% endtabs %}

Make sure you set the ownership and permissions accordingly. In this case, set the necessary permissions for a specific **or** current user (replace `USER` for the actual user that will run the `docker` command):

{% tabs %}
{% tab title="Astar" %}
```
# chown to a specific user
chown USER /var/lib/astar/astar-db

# chown to current user
sudo chown -R $(id -u):$(id -g) /var/lib/astar/astar-db
```
{% endtab %}

{% tab title="Shiden" %}
```
# chown to a specific user
chown USER /var/lib/astar/shiden-db

# chown to current user
sudo chown -R $(id -u):$(id -g) /var/lib/astar/shiden-db
```
{% endtab %}

{% tab title="Untitled" %}
```
# chown to a specific user
chown USER /var/lib/astar/shibuya-db

# chown to current user
sudo chown -R $(id -u):$(id -g) /var/lib/astar/shibuya-db
```
{% endtab %}
{% endtabs %}

### Prerequisites

* [Docker](https://docs.docker.com/get-docker/): Containerization platform for software solutions
* [Ngrok](https://ngrok.com): Ngrok is a tunnel service to securely expose your RPC service in the local computer. `auth-toke`n is required for a dedicated connection.

## Run an RPC node

### One-line startup script

If one wants to finish the process without explanation, here is the one-line script for you. if you face an error upon execution, the descriptions below will help you to find where it needs to be adjusted. This script supposes that the running computer has `docker` and `ngrok`installed.

{% tabs %}
{% tab title="Shiden use only!" %}
```
sudo curl -s https://raw.githubusercontent.com/AstarNetwork/Astar/rpc-script/scripts/rpc.sh > rpc.sh \
&& sudo bash ./rpc.sh \
-auth <your ngrok auth token>
```
{% endtab %}
{% endtabs %}

### Running RPC node

Run this docker command first to spin up our full node and for integration partners to access the data like The Graph / Chainlink. Start from running an archive node but add the flag

&#x20;`-l evm=debug,ethereum=debug,rpc=debug`

Replace `NAME` with your node name.

{% tabs %}
{% tab title="Astar" %}
```
# get container
sudo docker pull staketechnologies/astar-collator

# command to run RPC node - do not forget to change **NAME** to whatever you like
docker run -m 5G --name Shiden -p 30334:30334 -p 30333:30333 -p 9933:9933 -p 9944:9944 \
-v "/var/lib/astar/shiden-db:/data" \\
-u $(id -u ${USER}):$(id -g ${USER}) -d --network=host staketechnologies/astar-collator \
astar-collator --name NAME --chain astar --parachain-id 2006 --base-path /data --port 30333 --rpc-port 9933 --rpc-cors=all --unsafe-rpc-external --unsafe-ws-external --pruning archive \
--state-cache-size 1 --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
-l evm=debug,ethereum=debug,rpc=debug \
```
{% endtab %}

{% tab title="Shiden" %}
```
# get container
sudo docker pull staketechnologies/astar-collator

# command to run RPC node - do not forget to change **NAME** to whatever you like
docker run -m 5G --name Shiden -p 30334:30334 -p 30333:30333 -p 9933:9933 -p 9944:9944 \
-v "/var/lib/astar/shiden-db:/data" \
-u $(id -u ${USER}):$(id -g ${USER}) -d staketechnologies/astar-collator \
astar-collator --name NAME --base-path /data --port 30333 --rpc-port 9933 --rpc-cors=all --unsafe-rpc-external --unsafe-ws-external --pruning archive \
--state-cache-size 1 --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
-l evm=debug,ethereum=debug,rpc=debug \
```
{% endtab %}

{% tab title="Shibuya" %}
```
# get container
sudo docker pull staketechnologies/astar-collator

# command to run RPC node - do not forget to change **NAME** to whatever you like
docker run -m 5G --name Shiden -p 30334:30334 -p 30333:30333 -p 9933:9933 -p 9944:9944 \
-v "/var/lib/astar/shiden-db:/data" \
-u $(id -u ${USER}):$(id -g ${USER}) -d --network=host staketechnologies/astar-collator \
astar-collator --name NAME --chain shibuya --parachain-id 1000 --base-path /data --port 30333 --rpc-port 9933 --rpc-cors=all --unsafe-rpc-external --unsafe-ws-external --pruning archive \
--state-cache-size 1 --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
-l evm=debug,ethereum=debug,rpc=debug \
```
{% endtab %}
{% endtabs %}

### Syncing to the latest block

If the RPC node is successfully running the node should be registered in telemetry. You will be able to see an RPC node syncing to the latest block with the **NAME** specified in the command.

![Shiden Telemetry](<../../.gitbook/assets/image (107) (1).png>)

During the syncing process, you will see messages from both the relay chain and the parachain in your logs. These messages display a target block (live network state) and the best block (local node synced state).

{% hint style="info" %}
Make sure for the RPC node an HTTP connection is available.
{% endhint %}

### Exposing to public

After checking the RPC node running locally, it can be connected to other clients that need access to the blockchain data such as The Graph node, Chainlink, and Blockscout. To expose an RPC node to the public requires a secure connection to the RPC. A tunnel is required for this. This can be achieved from `[ngrok](<https://ngrok.com/>)` . Run these commands to expose your web server port to the public. This will create a secure HTTPS connection without self-signed certificates.

```bash
snap install ngrok
/// after installation
ngrok http 9933
```

After running the command, the terminal shows a screen like this.

![Ngrok view](<../../.gitbook/assets/image (114) (1) (1) (1) (1).png>)

Ngrok default setting has an expiring session for 2 hours. To have persistent RPC exposure, sign up to their service, and set up auth token with the command:

```bash
ngrok authtoken <your ngrok auth token> 
```

### Checking connections with ethers.js

If the node is running right, try this script to check if the connection is available.

```bash
const { ethers } = require("ethers");

const provider = new ethers.providers.JsonRpcProvider("https://<IP or domain name>");

async function checkBlocks() {
// Get block height of the network
const blocks = await provider.getBlockNumber();
console.log(blocks) 
}

checkBlocks();
// prints current block height
```

If the node is exposed, it should display the block height of the network.

![](<../../.gitbook/assets/image (111) (1) (1) (1) (1).png>)

## Using Relaychain Snapshot

Running an Astar node can take days before it’s synced to the Kusama or Polkadot relay chain. You can speed up this process by using Polkashots:

{% embed url="https://polkashots.io" %}

This is the example for Shiden!

```bash
# navigate to ksmcc3
cd /var/lib/astar/shiden-db/polkadot/chains/ksmcc3

# if folder doesn't excist create and go navigate to the folder
sudo mkdir /var/lib/astar/shiden-db/polkadot/chains/ksmcc3 && cd /var/lib/astar/shiden-db/polkadot/chains/ksmcc3

# download the latest snapshot
wget https://ksm-rocksdb.polkashots.io/snapshot -O kusama.RocksDb.tar.lz4

# extract snapshot (this can take some time) - make sure you have permission in the directory
sudo lz4 -c -d kusama.RocksDb.tar.lz4 | tar -x -C /var/lib/astar/shiden-db/polkadot/chains/ksmcc3

# remove file
rm -v kusama.RocksDb.tar.lz4
```

## How to update your node

As our development continues, it will sometimes be necessary to upgrade your node. Node operators will be notified [i](https://discord.gg/PfpUATX)n our [Discord](https://discord.gg/Z3nC9U4) and Element group when upgrades are available and priority. The upgrade process is straightforward and is the same for all kinds of nodes.

1.  Stop the docker container:

    `sudo docker stop CONTAINER_ID`

    If you don’t know the `container_id`, find it here `sudo docker ps`
2. Pull the latest version of Astar
3. Use the latest version to spin up your node.

Once your node is running again, you should see logs in your terminal.

### Purge your node

If you need a fresh instance of your node, you can purge your node by removing the associated data directory.

You'll first need to stop the Docker container:

`sudo docker stop CONTAINER_ID`

{% tabs %}
{% tab title="Astar" %}
```
sudo rm -rf /var/lib/astar/aster-db/*
```
{% endtab %}

{% tab title="Shiden" %}
```
sudo rm -rf /var/lib/astar/shiden-db/*
```
{% endtab %}

{% tab title="Shibuya" %}
```
sudo rm -rf /var/lib/astar/shibuya-db/*
```
{% endtab %}
{% endtabs %}

