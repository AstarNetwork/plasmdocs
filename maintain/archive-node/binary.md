# Binary

In this guide, we will use the binary provided in [Astar release](https://github.com/AstarNetwork/Astar).\
If you have experience with rust compilation, you can still [compile the binary](https://docs.astar.network/maintain/collator/secure-validator/plasm-shiden-node#build-from-binaries) on your machine.

## Let's get started

Let's start with updating our server. Connect to your server and update:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y adduser libfontconfig1
```

## Create dedicated user and directory

Create a dedicated user for the node and move the **node binary**:

```
sudo useradd --no-create-home --shell /usr/sbin/nologin astar
sudo cp ./astar-collator /usr/local/bin
chmod +x astar-collator*.tar.gz
```

Create a dedicated directory for the **chain storage data**:

```
sudo mkdir /var/lib/astar
sudo chown astar:astar /var/lib/astar
```



## Set systemd service

To run a stable collator node, a **systemd service** has to be set and activated. This will ensure that the node is restarting even after a server reboot.

Create a service file

```
sudo nano /etc/systemd/system/astar.service
```

Add service parameters:

{% tabs %}
{% tab title="Astar" %}
```
[Unit]
Description=Astar Archive node

[Service]
User=astar
Group=astar
  
ExecStart=/usr/local/bin/astar-collator \
  --pruning archive \
  --rpc-cors all \
  --name ${COLLATOR_NAME} \
  --chain astar \
  --parachain-id 2006 \
  --base-path /var/lib/astar \
  --execution wasm\
  --state-cache-size 1
  
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```
{% endtab %}

{% tab title="Shiden" %}
```
[Unit]
Description=Shiden Archive node

[Service]
User=astar
Group=astar
  
ExecStart=/usr/local/bin/astar-collator \
  --pruning archive \
  --rpc-cors all \
  --name ${COLLATOR_NAME} \
  --chain shiden \
  --base-path /var/lib/astar \
  --execution wasm\
  --state-cache-size 1
  
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```
{% endtab %}

{% tab title="Shibuya" %}
```
[Unit]
Description=Shibuya Archive node

[Service]
User=astar
Group=astar
  
ExecStart=/usr/local/bin/astar-collator \
  --pruning archive \
  --rpc-cors all \
  --name ${COLLATOR_NAME} \
  --chain shibuya \
  --parachain-id 1000 \
  --base-path /var/lib/astar \
  --execution wasm\
  --state-cache-size 1
  
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Do not forget to change **${COLLATOR\_NAME}**
{% endhint %}

Start the service:

```
sudo systemctl start astar.service
```

Check the node log and that everything is syncing fine:

```
journalctl -f -u astar.service -n100
```

Enable the service:

```
sudo systemctl enable astar.service
```

## And then?

It all depends about what you plan to do with your archive node.

* In most cases, you will want to access node from outside. In this case, you need to set up a nginx server.
* If you run your dapp on the same server than the node (recommended for testing purpose only), you can access it directly with the `localhost` address.
* If you run the node locally for testing purpose, you can for example switch network into [Polkadot.js portal](https://polkadot.js.org/apps) and explore the chain:

![Switch to local node](<../../.gitbook/assets/image (119).png>)
