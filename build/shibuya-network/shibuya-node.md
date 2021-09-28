# Build a Collator

{% hint style="info" %}
UNDER MAINTENANCE
{% endhint %}

Currently, Astar has 2 networks, [Shibuya Network](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.shibuya.astar.network#/accounts), and [Shiden Network](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fshiden.api.onfinality.io%2Fpublic-ws#/accounts).

Shibuya Network is our parachain testnet. In case you want to run a collator and want to deploy it in our testnet. Join our[ Discord](https://discord.gg/Z3nC9U4) to find out the latest news and support.  

### Building a collator \(validator\):

This documentation is based on:

{% embed url="https://app.subsocial.network/4907/shibuya-onboarding-collators-19840" %}

A tutorial was made by one of our community members during the Shibuya onboarding challenge.

{% hint style="info" %}
Make sure you always use the latest binary! This document is built with the `shiden-14` release. Please check if there is a new version, if yes, download that one! The old versions will not be accepted in the collator set! 

Always check here: [https://github.com/PlasmNetwork/Astar/releases](https://github.com/PlasmNetwork/Astar/releases)
{% endhint %}

1\) Install tools and download binary:

```text
sudo -s
apt update
apt upgrade -y
apt install -y curl
rm -f /usr/bin/astar-collator.bak
mv -f /usr/bin/astar-collator /usr/bin/astar-collator.bak
curl -sL https://github.com/PlasmNetwork/Plasm/releases/download/shiden-14/astar-collator-2.5.0-ubuntu-x86_64.tar.gz | tar -xzvf - -C /usr/bin
chmod +x /usr/bin/astar-collator
```

Let's check the version:

```text
# /usr/bin/astar-collator -V
```

You should see output like this:

```text
astar-collator 2.5.0-4791291-x86_64-linux-gnu
```

2\) Set your node name to whatever you want:

```text
export NODENAME="My_Shibuya_Node"
```

3\) Create an unprivileged user to run a node from:

```text
useradd -mU shibuya
```

4\) Create a systemd service for your collator node:

```text
cat > /etc/systemd/system/shibuya-node.service << EOF
[Unit]
Description=Shibuya Collator Node
After=network-online.target
Wants=network-online.target

[Service]
User=shibuya
Group=shibuya
WorkingDir=/home/shibuya/
ExecStart=/usr/bin/astar-collator --validator --name $NODENAME --chain shibuya --parachain-id 1000 --rpc-cors all --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --execution wasm
Restart=always
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```

5\) Enable and start a node as service and:

```text
systemctl enable shibuya-node
systemctl start shibuya-node
systemctl status shibuya-node
```

You should see output like this:

```text
● shibuya-node.service - Shibuya Collator Node
     Loaded: loaded (/etc/systemd/system/shibuya-node.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2021-09-11 16:09:13 UTC; 7min ago
   Main PID: 8018 (astar-collator)
      Tasks: 72 (limit: 154406)
     Memory: 483.2M
        CPU: 1min 17.590s
     CGroup: /system.slice/shibuya-node.service
             └─8018 /usr/local/bin/astar-collator --validator --name NODENAME --chain shibuya --parachain-id 1000 --rpc-cors all --telemetry-url wss://telemetry.polkadot.io/submit/ 0 --execution wasm

2021-09-11 15:28:24 [Relaychain] ⚙️  Syncing 57.5 bps, target=#1137284 (37 peers), best: #1125837 (0xbfb2…27a8), finalized #1125830 (0xede7…89c5), ⬇ 897.6kiB/s ⬆ 51.1kiB/s    
2021-09-11 15:28:26 [Parachain] 💤 Idle (42 peers), best: #24529 (0x0282…b13b), finalized #19619 (0x8d4a…85d1), ⬇ 0.5kiB/s ⬆ 0.8kiB/s    
2021-09-11 15:28:29 [Relaychain] ⚙️  Syncing 55.1 bps, target=#1137284 (37 peers), best: #1126113 (0xa43d…c2aa), finalized #1126110 (0x0d0a…6f4b), ⬇ 4.9kiB/s ⬆ 16.9kiB/s    
2021-09-11 15:28:31 [Parachain] 💤 Idle (42 peers), best: #24529 (0x0282…b13b), finalized #19748 (0x929d…065d), ⬇ 3.5kiB/s ⬆ 0.5kiB/s    
2021-09-11 15:28:34 [Relaychain] ⚙️  Syncing 56.5 bps, target=#1137285 (37 peers), best: #1126396 (0x78c0…c5aa), finalized #1126390 (0x2c6e…c30a), ⬇ 7.8kiB/s ⬆ 23.6kiB/s    
2021-09-11 15:28:36 [Parachain] 💤 Idle (42 peers), best: #24529 (0x0282…b13b), finalized #19887 (0xd0d6…0437), ⬇ 7.8kiB/s ⬆ 2.3kiB/s    
2021-09-11 15:28:39 [Relaychain] ⚙️  Syncing 52.7 bps, target=#1137286 (37 peers), best: #1126660 (0x64d5…1ba8), finalized #1126660 (0x64d5…1ba8), ⬇ 7.4kiB/s ⬆ 74.2kiB/s    
2021-09-11 15:28:41 [Parachain] 💤 Idle (42 peers), best: #24529 (0x0282…b13b), finalized #20020 (0xe3d3…8c64), ⬇ 2.4kiB/s ⬆ 41.1kiB/s    
2021-09-11 15:28:44 [Relaychain] ⚙️  Syncing 64.9 bps, target=#1137287 (37 peers), best: #1126985 (0xea6f…9da9), finalized #1126980 (0x5147…e586), ⬇ 7.8kiB/s ⬆ 40.1kiB/s    
2021-09-11 15:28:46 [Parachain] 💤 Idle (42 peers), best: #24529 (0x0282…b13b), finalized #20167 (0x8a1f…5994), ⬇ 0.3kiB/s ⬆ 0.3kiB/s    
```

If your node is up and running, you **should see** its NODENAME \(the name you configured\) on the [Telemetry page](https://telemetry.polkadot.io/#/0xddb89973361a170839f80f152d2e9e38a376a5a7eccefcade763f46a8e567019).

6\) Now you have to wait till your node is fully synchronized. This can some time. _Note, you must wait until both **Parachain** and **Relaychain** are synchronized._

You can periodically check the current synchronization status:

```text
journalctl -u shibuya-node -o cat -n 20
```

7\) When your node is in sync, you are ready to be onboard. But you need some SDY tokens to set up on-chain identity \(10 SBY\) and much more to become an active collator \(32000 SBY\).

