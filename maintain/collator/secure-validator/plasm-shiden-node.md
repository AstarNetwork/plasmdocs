# Building Collator node

## Let's get started

Let's start with updating our server. Connect to your server and update:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y adduser libfontconfig1
```

## Build the node

To build a collator node, you have 3 different options

* [From source](plasm-shiden-node.md#build-from-source)
* [From binary](plasm-shiden-node.md#build-from-binaries)
* [Run a Docker container](plasm-shiden-node.md#run-a-docker-container)

### Build from source

Building a node from source code is the most complicated path, but will also provide the best optimized node version for your server.

Make sure your server is ready to build a collator:

```
## Install Rust
##
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly

## Compilation required software
##
bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"
sudo apt install cmake 
sudo apt install git 
sudo apt install build-essential
sudo apt update
sudo apt install clang
```

Clone the Astar repository:

```
git clone https://github.com/AstarNetwork/Astar.git
cd Astar
```

Make sure you have the latest commit in place:

```
git checkout
git pull
```

Compile the node binary:

```
CARGO_PROFILE_RELEASE_LTO=true RUSTFLAGS="-C codegen-units=1" cargo build --release
```

### Build from binaries

The easiest way to install an Astar node is to download the binaries. You can find them here:&#x20;

{% embed url="https://github.com/AstarNetwork/Astar" %}
Astar releases
{% endembed %}

Get the file and extract:

```
wget $(curl -s https://api.github.com/repos/AstarNetwork/Astar/releases/latest | grep "tag_name" | awk '{print "https://github.com/PlasmNetwork/Plasm/releases/download/" substr($2, 2, length($2)-3) "/astar-collator-" substr($2, 3, length($2)-4) "-ubuntu-x86_64.tar.gz"}')
```

```
tar -xvf astar-collator*.tar.gz
```

### Run a Docker container

You can find here the [Astar Docker hub](https://hub.docker.com/r/staketechnologies/astar-collator).

Pull the latest Docker version

```
docker pull staketechnologies/astar-collator:latest
```

## Start node

{% hint style="warning" %}
The following steps are suitable for **binary** usage (built from source or downloaded).&#x20;

In case you want to run a Docker container, you will have to adapt those.
{% endhint %}

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

Let's first go to our binary directory and start the node manually:

{% tabs %}
{% tab title="Astar" %}
```
cd /usr/local/bin
./astar-collator --validator --chain astar --parachain-id 2006 --name ${COLLATOR_NAME} --rpc-cors all --base-path /var/lib/astar --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --execution wasm --state-cache-size 1
```
{% endtab %}

{% tab title="Shiden" %}
```
cd /usr/local/bin
./astar-collator --validator --chain shiden --name ${COLLATOR_NAME} --rpc-cors all --base-path /var/lib/astar --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --execution wasm --state-cache-size 1
```
{% endtab %}

{% tab title="Shibuya" %}
```
cd /usr/local/bin
./astar-collator --validator --chain shibuya --parachain-id 1000 --name ${COLLATOR_NAME} --rpc-cors all --base-path /var/lib/astar --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --execution wasm --state-cache-size 1
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Type in the place of **${COLLATOR\_NAME}**, how you would like to call your node.
{% endhint %}

Check on [https://telemetry.polkadot.io/](https://telemetry.polkadot.io/#/Dusty) to see your node syncing.

{% hint style="info" %}
Useful commands to be used in screen:\
_`ctrl+a+d` (detach actual session)_\
_`screen ls` (this will list all running screens)_\
_`screen -r` (restore a screen session)_
{% endhint %}

Stop the manual node and kill the screen session:

```
ctrl+c
ctrl+a+k
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
Description=Astar Collator

[Service]
User=astar
Group=astar
  
ExecStart=/usr/local/bin/astar-collator \
  --validator \
  --rpc-cors all \
  --name ${COLLATOR_NAME} \
  --chain astar \
  --parachain-id 2006 \
  --base-path /var/lib/astar \
  --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
  --execution wasm\
  --state-cache-size 1
  
Restart=always
RestartSec=120

[Install]
WantedBy=multi-user.target
```
{% endtab %}

{% tab title="Shiden" %}
```
[Unit]
Description=Shiden Collator

[Service]
User=astar
Group=astar

ExecStart=/usr/local/bin/astar-collator \
  --validator \
  --rpc-cors all \
  --name ${COLLATOR_NAME} \
  --chain shiden \
  --base-path /var/lib/astar \
  --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
  --execution wasm\
  --state-cache-size 1

Restart=always
RestartSec=120

[Install]
WantedBy=multi-user.target
```
{% endtab %}

{% tab title="Shibuya" %}
```
[Unit]
Description=Shibuya Collator

[Service]
User=astar
Group=astar

ExecStart=/usr/local/bin/astar \
  --validator \
  --rpc-cors all \
  --name ${COLLATOR_NAME} \
  --chain shibuya \
  --parachain-id 1000 \
  --base-path /var/lib/astar \
  --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
  --execution wasm\
  --state-cache-size 1

Restart=always
RestartSec=120

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

## Relay Chain snapshot

If you run your collator it not only needs to sync the **mainnet** chain but also the complete relay chain from **Kusama / Polkadot**. This can take up to 3-4 days. You can also use a snapshot of Kusama/Polkadot. You can download this [here](https://polkashots.io) and will save a lot of time.

{% hint style="danger" %}
**NOTE**: know what you are doing when using snapshots!
{% endhint %}

## Finalizing

To finalize your collator you need to:

* Setup an account
* Author your session key
* Set up your session key
* Verify your identity
* Bond tokens

All these steps can be found here:

{% content-ref url="../shibuya-network/" %}
[shibuya-network](../shibuya-network/)
{% endcontent-ref %}

{% content-ref url="../shiden-collator-guide/" %}
[shiden-collator-guide](../shiden-collator-guide/)
{% endcontent-ref %}
