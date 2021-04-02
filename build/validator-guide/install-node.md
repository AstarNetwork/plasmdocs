# Install Node

{% hint style="info" %}
Find out the IP address of your server and make sure ****you have your SSH \(port: 22\) and HTTPS port \(443\) open
{% endhint %}

### 1. Connect to your server:

Connect via client of your choice, e.g. [PuTTY](http://go.microsoft.com/fwlink/?LinkId=2116707) or [other clients](http://go.microsoft.com/fwlink/?LinkId=2116708).  
- Type IP address in the field ‘Host Name’  
- The terminal will open and you can log in with your username and password.

**Or** connect directly via terminal with your ssh keys:

```text
ssh -i .ssh/azureuser/dusty-validator_key.pem azureuser@11.22.33.44
```

### 2. Download Plasm node

The easiest way to install a Plasm node is to download the latest binaries. You can find them here: [https://github.com/staketechnologies/Plasm/releases](https://github.com/staketechnologies/Plasm/releases). Use this command in your server terminal:

```text
 wget https://github.com/PlasmNetwork/Plasm/releases/download/v1.9.0-dusty/plasm-1.9.0-ubuntu-x86_64.tar.gz
```

Extract the files:

```text
tar -xf plasm-1.9.0-ubuntu-x86_64.tar.gz 
```

Continue with Configure Node step.

