---
description: How to integrate SubWallet in your dApp
---

# Integrate SubWallet

## Overview

SubWallet, Polkadot{.js} and Talisman extension allow DApp to connect with them by public their interaction in object `injectedWeb3` of window browser.

* SubWallet (public with properties `subwallet-js`)
* Polkadot{.js} (public with properties `polkadot-js`)
* Talisman (public with properties `talisman`)

![SubConnect](https://github.com/Koniverse/SubConnect/wiki/images/SubConnect.png)

You can open `injectedWeb3` object in chrome devtools

![InjectWeb3DevTools](https://github.com/Koniverse/SubConnect/wiki/images/InjectWeb3DevTools.png)

## How to integrate with your dApp

* Check the activation of the extension:
  * When a wallet extension is active in a browser it will modify `window.injectedWeb3` by adding its interaction with specifying the name.
  * For example: check the SubWallet extension by this code: `window.injectedWeb3 && window.injectedWeb3['subwallet-js']`
*   Enable intergration with your dApp by the method `enable()` of extension interaction object

    ```
    const SubWalletExtension = window.injectedWeb3['subwallet-js']
    const extension = await SubWalletExtension.enable()
    ```

    After running this code extension, it will show a popup confirmation to confirm the integration with your dApp.
* After enabling, the `extension` variable can contain these object
  * `accounts`: Allow getting accounts data with 2 methods `get` `subscribe`.
  * `signer`: Allow to sign data with 2 methods: `signPayload`, `signRaw`.
  * `metadata`: Allow getting additional metadata list with method `get` and add/update with  `provide`.

## Use with Typescript

If your dApp is written with typescript you need to add `@polkadot/extension-inject` to your package.json to get the extension interfaces.
