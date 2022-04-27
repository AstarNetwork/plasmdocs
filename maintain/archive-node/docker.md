# Docker

A **Docker container** allow you to run easily a node without depending on the platform it is running on. This method should be reserved for users who already have experience with Docker containers.

## Installation

If you don't already have, start by installing docker: [How to install Docker on Ubuntu](https://linuxize.com/post/how-to-install-and-use-docker-on-ubuntu-20-04/)

Create a local directory for the **chain storage data** and a dedicated user:

```
sudo mkdir /var/lib/astar
sudo useradd --no-create-home --shell /usr/sbin/nologin astar
sudo chown astar:astar /var/lib/astar
```

## Start Docker node

In this guide, we will start a container for both WS and RPC endpoints. If you want only one of those, just remove the unnecessary port and command.

Launch the docker node in detached mode:

{% tabs %}
{% tab title="Astar" %}
```
docker run -d \
--name astar-container \
-u $(id -u astar):$(id -g astar) \
-p 30333:30333 \
-p 9933:9933 \
-p 9944:9944 \
-v "/var/lib/astar/:/data" \
staketechnologies/astar-collator:latest \
astar-collator \
--pruning archive \
--name ${NODE_NAME} \
--chain astar \
--execution Native \
--pool-limit 65536 \
--base-path /data \
--rpc-cors=all \
--unsafe-rpc-external \
--ws-external \
--state-cache-size 1
```
{% endtab %}

{% tab title="Shiden" %}
```
docker run -d \
--name shiden-container \
-u $(id -u astar):$(id -g astar) \
-p 30333:30333 \
-p 9933:9933 \
-p 9944:9944 \
-v "/var/lib/astar/:/data" \
staketechnologies/astar-collator:latest \
astar-collator \
--pruning archive \
--name ${NODE_NAME} \
--chain shiden \
--execution Native \
--pool-limit 65536 \
--base-path /data \
--rpc-cors=all \
--unsafe-rpc-external \
--ws-external \
--state-cache-size 1
```
{% endtab %}

{% tab title="Shibuya" %}
```
docker run -d \
--name shibuya-container \
-u $(id -u astar):$(id -g astar) \
-p 30333:30333 \
-p 9933:9933 \
-p 9944:9944 \
-v "/var/lib/astar/:/data" \
staketechnologies/astar-collator:latest \
astar-collator \
--parachain-id 1000 \
--pruning archive \
--name ${NODE_NAME} \
--chain shibuya \
--execution Native \
--pool-limit 65536 \
--base-path /data \
--rpc-cors=all \
--unsafe-rpc-external \
--ws-external \
--state-cache-size 1
```
{% endtab %}
{% endtabs %}



{% hint style="info" %}
Do not forget to change **${NODE\_NAME}**
{% endhint %}

You can test the node health through RPC port with this command:

```
curl -H "Content-Type: application/json" --data '{ "jsonrpc":"2.0", "method":"system_health", "params":[],"id":1 }' localhost:9933
```

## And then? <a href="#and-then" id="and-then"></a>

For any usage, wait for the chain to be fully sync by checking the [node log](docker.md#get-node-logs).

Then, it all depends about what you plan to do with your archive node.

* In most cases, you will want to access node from outside. In this case, you need to set up a nginx server.
* If you run your dapp on the same server than the node (recommended for testing purpose only), you can access it directly with the `localhost` address.
* If you run the node locally for testing purpose, you can for example switch network into [Polkadot.js portal](https://polkadot.js.org/apps) and explore the chain:

![](<../../.gitbook/assets/image (119).png>)

## Extra operations

### Get node logs

To get the last 100 lines from the node logs, use the following command:

{% tabs %}
{% tab title="Astar" %}
docker logs -f -n 100 $(docker ps -aq --filter name="astar-container")
{% endtab %}

{% tab title="Shiden" %}
docker logs -f -n 100 $(docker ps -aq --filter name="shiden-container")
{% endtab %}

{% tab title="Shibuya" %}
docker logs -f -n 100 $(docker ps -aq --filter name="shibuya-container")
{% endtab %}
{% endtabs %}

### Indexers and oracles

To access data from indexers (lke The Graph) or Oracles (like Chainlink), you need to add the debug flags below to the node launch command, after the `astar-collator` line:

&#x20;`-l evm=debug,ethereum=debug,rpc=debug \`

### Upgrade node

When an upgrade is necessary, node operators are be notified in our [Discord](https://discord.gg/Z3nC9U4) and Element group.

To upgrade to the latest node version, stop and remove the actual container:

{% tabs %}
{% tab title="Astar" %}
docker stop $(docker ps -q --filter name="astar-container")

docker rm $(docker ps -a -q --filter name="astar-container")
{% endtab %}

{% tab title="Shiden" %}
docker stop $(docker ps -q --filter name="shiden-container")

docker rm $(docker ps -a -q --filter name="shiden-container")
{% endtab %}

{% tab title="Shibuya" %}
docker stop $(docker ps -q --filter name="shibuya-container")

docker rm $(docker ps -a -q --filter name="shibuya-container")
{% endtab %}
{% endtabs %}

Then start a new container with the [start command](docker.md#start-docker-node). Chain data will be kept on your machine under `var/lib/astar/.`

### Purge node

To start a new container from scratch without any chain data, just remove the container and wipe the chain data directory:

{% tabs %}
{% tab title="Astar" %}
```
docker rm -f $(docker ps -a -q --filter name="astar-container")
sudo rm -R /var/lib/astar/*
```
{% endtab %}

{% tab title="Shiden" %}
```
docker rm -f $(docker ps -a -q --filter name="shiden-container")
sudo rm -R /var/lib/astar/*
```
{% endtab %}

{% tab title="Shibuya" %}
```
docker rm -f $(docker ps -a -q --filter name="shibuya-container")
sudo rm -R /var/lib/astar/*
```
{% endtab %}
{% endtabs %}

Then start a new container with the [start command](docker.md#start-docker-node).

### Relay Chain snapshot

If you run your collator it not only needs to sync the **mainnet** chain but also the complete relay chain from **Kusama / Polkadot**. This can take up to 3-4 days. You can also use a snapshot of Kusama/Polkadot. You can download this [here](https://polkashots.io) and will save a lot of time.

{% hint style="warning" %}
**NOTE**: know what you are doing when using snapshots!
{% endhint %}
