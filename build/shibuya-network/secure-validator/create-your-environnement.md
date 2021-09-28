# Create Your Environnement

Stake Technologies, one of the core companies behind Plasm Network, has been selected for [Microsoft for Startup](https://startups.microsoft.com/en-us/) program. Together with Microsoft, we are going to start **Shiden Azure Validator Program** by using Microsoft Azure when Shiden becomes a Kusama Parachain. Therefore, this setup will be based on Azure but is also possible with other providers.

### System requirements

A validator usually deploys nodes on cloud servers. You can choose your preferred VPS service provider and operating system. We recommend Ubuntu 18.04 and Azure.

### Hardware requirements

We will provide a basic configuration for reference, which guarantees that all blocks can process in time. If the hardware is inferior to that, there will be malfunctions.

#### Basic configuration:

* System: Linux or MacOS, Ubuntu 18.04 is recommended
* CPU: at least 2 cores, Intel Core
* Memory: at least 8 GB
* Hard disk: at least 80 GB, regularly evaluated

#### Recommended configuration:

* System: Linux or MacOS, Ubuntu18.04
* CPU: 4 cores, Intel Core
* Memory: 8 GB
* Hard Disk: 250 GB

### Installation

For the users who are selected to join the Azure Validator Program, please follow these instructions. This the modified version of [pathrock](https://pathrock-70243.medium.com/plasm-azure-validator-program-758205408117) guide.

1. First, you need to go to [https://portal.azure.com/](https://portal.azure.com/#home) and login with your credentials. This should take you to the _Default Directory_.
2. Create your virtual machine

![](https://miro.medium.com/max/1418/1*so7BR5fvwBcSqsNO4-oXYg.png)

![](https://miro.medium.com/max/1489/1*x7vxcDNI5nijJcFKEFCzjg.png)

![](https://miro.medium.com/max/768/1*9ltiplbqkLyfR7Wjyd4BFw.png)

* Resource group: ...
* Virtual machine name: &lt;YOURNAME&gt;
* Region: Choose a region
* Image: Ubuntu Server 18.04 LTS — Gen1

![](../../../.gitbook/assets/01a.png)

* Size: See our recommendations

{% hint style="info" %}
Later in the tutorial, we will add ECDH SSH key security over Curve25519 with SHA2 and change the SSH port.
{% endhint %}

![](../../../.gitbook/assets/02a.png)

**Next**: 

* Networking \(no changes\)
* Management \(no changes\)
* Advanced \(no changes\)
* Tags \(no changes\)
* Preview + Create

![](../../../.gitbook/assets/image%20%2814%29.png)

### Resize disk space

Now that our server is created we have to finetune our setup. First, stop your server!

![](../../../.gitbook/assets/05.png)

The default disk size at the moment is 30 GiB, this is not enough for our validator. You need to increase the size to 128 GiB:

* In the menu left, click on _Disks_
* Click on the disk name
* In the menu left, click on _Size + performance_
* Choose 128 GiB and click on resize

{% hint style="info" %}
Not possible to resize? Did you stop your server?
{% endhint %}

* Start your virtual machine

