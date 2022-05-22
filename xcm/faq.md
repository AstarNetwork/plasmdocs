---
description: Frequently asked questions and answers related to XCM on Astar
---

# FAQ

### Q: Is there a way to see my DOT/SDN balance (on Astar/Shiden) on the Polkadot.js?

Yes. Go to Polkadot.js, connect with your wallet and go to Network > Balances and select the token you are interested in. Example below shows viewing SDN balance:

![Viewing KSM balance on Shiden Network](../.gitbook/assets/FAQ\_PolkadotJS\_AssetBalance1.png)

### Q: I used XCM to transfer 5 DOTs from Polkadot to Astar, but only received 4.999

Please note that the gas amount will be deducted from the amount entered. The transferred amount should be adjusted with the gas fee estimate. For more info, please look [here](using-xcm-on-astar/xcm-transactions.md#xcm-transfer-from-polkadot-to-astar).

### Q: My balance should be 1.00012 DOTs but the Portal is displaying 1 DOT, where are they?

Please note that the current version of Astar Portal is rounding balances to the 3rd decimal. If you have a similar issue please refer to the [previous FAQ entry ](faq.md#q-is-there-a-way-to-see-my-dot-sdn-balance-on-astar-shiden-on-the-polkadot.js)and instructions on how to use Polkadot.js to investigate exact balance of your tokens.

### Q: Can I send my DOT token to other Parachains?

Not at the moment.

### Q: How can I send my DOT token back to Polkadot?

This feature is in development and will be available soon for both EVM and native wallets.&#x20;

### Q: Why is XCM button for DOT/KSM disabled when I connect my wallet on the Astar Portal?

Please make sure you have non-zero balance of your native token as described in [this documentation section](using-xcm-on-astar/xcm-transactions.md#xcm-transfer-from-polkadot-to-astar).
