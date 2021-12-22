# Astar/Shiden node

## Let's get started

This guide is a little different from our previous guides you can find in our documentation. We want to make sure when you follow this guide you are having the most secure validator possible.

Let's start with updating our server. Connect to your server with PuTTy and let's update:

```
sudo apt update
sudo apt upgrade
sudo apt install -y adduser libfontconfig1
```

![](<../../../.gitbook/assets/image (21).png>)

To install and run your validator you can use the `nohup`command or use `screen`. I prefer using `screen` and will use this in the guide.

### Screen

Screen or GNU Screen is a terminal multiplexer. In other words, it means that you can start a screen session and then open any number of windows (virtual terminals) inside that session. Processes running in `screen` will continue to run when their window is not visible even if you get disconnected.

To start a screen session, simply type `screen` in your console. This is already installed on Azure so no need to install the software. You will see a lot of text, just hit the _spacebar_ twice.&#x20;

```
screen
```

This will open a screen session, create a new window, and start a shell in that window. Now that you have opened a screen session let's get our node.

### Download node

This part is based on the [following guide](https://medium.com/plasm-network/become-a-plasm-network-validator-c212085cc72e) and modified for this guide.\
The easiest way to install a Plasm node is to download the binaries. You can find them here:&#x20;

{% embed url="https://github.com/staketechnologies/Plasm/releases" %}

Get the file and extract:

```
wget https://github.com/staketechnologies/Plasm/releases/download/v1.9.0-dusty/plasm-1.9.0-ubuntu-x86_64.tar.gz
```

```
tar -xf plasm-1.9.0-ubuntu-x86_64.tar.gz
```

The following part is different from the other guide. We will create a dedicated user for the node and moved the `plasm` folder to `/usr/local/bin/`

```
sudo useradd --no-create-home --shell /usr/sbin/nologin plasm
sudo cp ./plasm /usr/local/bin
sudo chown plasm:plasm /usr/local/bin/plasm
```

Create a **dedicated directory for the chain storage data**:

```
sudo mkdir /var/lib/plasm
sudo chown plasm:plasm /var/lib/plasm
```

### Start node

Let's first go to our new `plasm` directory and start the node.

```
cd /usr/local/bin
./plasm --validator --name YOURNAME --rpc-cors all
```

{% hint style="info" %}
&#x20;Typ in the place of **YOURNAME**, how you would like to call your node.
{% endhint %}

Check on [https://telemetry.polkadot.io/](https://telemetry.polkadot.io/#/Dusty) to see your node syncing.\
Let's detach ourselves from this session so we can continue with the other steps.&#x20;

`ctrl+a+d`

Other interesting commands to be used in screen:\
`screen ls` (this will list all running screens)\
`screen -r` (restore a screen session)

### Finalizing

To finalize your validator you need to:

* Setup an account
* Grab your session key
* Set up your session key
* Verify

All these steps can find here:

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

