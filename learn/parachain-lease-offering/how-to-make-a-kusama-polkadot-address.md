# How to Create a Kusama/Polkadot Address

## Kusama / Polkadot Accounts <a id="__docusaurus"></a>

### Address Format

The address format used in Substrate-based chains is SS58. SS58 is a modification of Base-58-check from Bitcoin with some minor modifications. Notably, the format contains an _address type_ prefix that identifies an address as belonging to a specific network.

For example:

* Polkadot addresses always start with the number 1.
* Kusama addresses always start with a capital letter like C, D, F, G, H, J...
* Generic Substrate addresses start with 5.

## Recommend: Polkadot{.js} Browser Plugin

The Polkadot{.js} plugin provides a reasonable balance of security and usability. It provides a separate local mechanism to generate your address and interact with Polkadot and Kusama.

It is still running on the same computer you use to connect to the internet and thus is less secure than using [Parity Signer](https://www.parity.io/signer/). 

### Install the Browser Plugin

The browser plugin is available for both [Google Chrome](https://chrome.google.com/webstore/detail/polkadot%7Bjs%7D-extension/mopnmbcafieddcagagdcbnhejhlodfdd?hl=en) \(and Chromium-based browsers like Brave\) and [FireFox](https://addons.mozilla.org/en-US/firefox/addon/polkadot-js-extension). After installing the plugin, you should see the orange and white Polkadot{.js} logo in your browser menu bar.

![ Polkadot{.js} extension](../../.gitbook/assets/image%20%2842%29.png)

![ Polkadot{.js} logo](../../.gitbook/assets/image%20%2845%29.png)

### Create Account

Open the Polkadot{.js} browser extension by clicking the logo on the top bar of your browser. You will see a browser popup.

![Account menu Polkadot{.js}](../../.gitbook/assets/image%20%2841%29.png)

Click the big plus button - "Create new account". The Polkadot{.js} plugin will then use system randomness to make a new seed for you and display it to you in the form of twelve words.

![Create an account with Polkadot{.js}](../../.gitbook/assets/image%20%2840%29.png)

You should back up these words. Please, store the seed somewhere safe, secret, and secure. If you cannot access your account via Polkadot{.js} for some reason, you can re-enter your seed through the "Add account menu" by selecting "Import account from pre-existing seed".

![Create an account with Polkadot{.js}](../../.gitbook/assets/image%20%2843%29.png)

Best to create an account that is allowed on any chain in the Polkadot ecosystem. This account can then be used for Polkadot and Kusama. Your account will automatically change format when connected to a chain. 

**A descriptive name** is arbitrary and for your use only. It is not stored on the blockchain and will not be visible to other users who look at your address via a block explorer. If you're juggling multiple accounts, it helps to make this as descriptive and detailed as needed.

**The password** will be used to encrypt this account's information. You will need to re-enter it when using the account for any kind of outgoing transaction or when using it to cryptographically sign a message.

{% hint style="info" %}
Note that this password does NOT protect your seed phrase. If someone knows the twelve words in your mnemonic seed, they still have control over your account even if they do not know the password.
{% endhint %}

After clicking on "Add the account with the generated seed", your account is created. You copy your address by clicking on the icon. You can easily see your address for a chain if you click on the dots and select your desire chain.

![](../../.gitbook/assets/image%20%2844%29.png)

