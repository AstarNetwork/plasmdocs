# Import Ethereum Seed to Plasm Network

This is a guide for importing your ECDSA key (notably Ethereum wallets) into Plasm Network to use it within the network.
Any Ethereum private keys can be used within Plasm Network, however, this guide will be most helpful for Etherum lockdrop participants to access their tokens.

> **Disclaimer**
Please be cautious when handling Ethereum Private key, as it may potentially compromise your Ethereum wallet when it is leaked.

## Plasm Network Portal

The first step for importing your Ethereum wallet to Plasm Network is to access the Plasm Network Portal.
You can use the following IPFS link.

* [IPFS Link](https://ipfs.io/ipfs/QmZQBwe4DeW6aruayemGXA5ysexsqJVRzF6YHHeNPzKi7d)

> IPFS as content-oriented distributed storage is a most safe place for sensitive code. Any changes in code will change URI and makes this code unavailable.

For better performance, we recommend to use local installed [IPFS node](https://github.com/ipfs-shipyard/ipfs-desktop). And IPFS Companion extension for your browser:

* Chrome: https://chrome.google.com/webstore/detail/ipfs-companion/nibjojkomfdiaoajekhjakgkdhaomnch
* FireFox: https://addons.mozilla.org/ru/firefox/addon/ipfs-companion/

You should be able to see the following page.

![Local Plasm Portal](../img/local_plasm_portal.png)

## Importing Ethereum Seed

Now prepare your Ethereum private key that you wish to import to Plasm Network.
For lockdrop participants, it *must* be the private key of a wallet that made the lockdrop transaction.
It can either be a hex-string, or mnemonic.

> How to export your keys from [Metamask guide](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key).

When you have finished exporting the keys from your Ethereum wallet, you are ready to import then to Plasm  Network.
Go to **Accounts** -> **Add account** from the side tab.

![Create account](../img/create_ecdsa_account.png)

Now copy and paste your hex-string private keys or mnemonics iin the seed input field.

Please choose **ECDSA** type of keypair and hex-string for seed (if you export Metamask key by [guide](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key)).

![Put ECDSA seed](../img/ecdsa_seed.png)

Fill another fields including password as save account.

![Check balance](../img/check_account_balance.png)

If everything went well, you should be able to see a new wallet with the type of ECDSA being imported.
Additionally, for lockdrop participants, you should see that the imported address contains the PLM that you've received from the lockdrop.
