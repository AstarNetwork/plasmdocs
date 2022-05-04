# How to set On-Chain Identity

## Overview

What is on-chain identity and why we will use this on the Astar ecosystem? \
You can see on-chain identity more like having an on-chain reputation. An on-chain identity is a good way to build up your reputation and let the community know more about you if you plan on running a validator, being part of the council, and in a later phase ask for funds from our treasury. This pallet is very important on our road to becoming a DAO.

With on-chain identity, nothing is attached to your real-world identity so you don't get personally doxed, but it’s more like a brand the community can trust and come to rely on. It’s more like a social KYC, a name or brand the community can trust.&#x20;

We provide a registrar service in the Astar and Shiden networks that only charges a small fee (10 SDN) in Shiden, but this can change on Astar. However, you will of course need to reserve some SDN in your account while you have an identity, no matter which registrar you use. For details on the amount necessary to reserve, as well as the identity system as a whole, see the identity section.

## **Setting an identity**

Go to [the Accounts](https://polkadot.js.org/apps/#/accounts) page in Polkadot-JS Apps, make sure you are connected to the chain you want to set your identity. The easiest way to add the built-in fields is to click the vertical three dots next to one's account and select "Set on-chain identity".

![Set on-chain identity in account menu](<../../.gitbook/assets/image (11).png>)

A popup will appear, offering the default fields. Following fields are mandatory to have to be approved as Collator:

* Display Name (use the same name here as your node on Telemetry)
* Email (This will be verified)
* Twitter
* Element (formerly known as Riot)

![Required fields for on-chain identity](<../../.gitbook/assets/image (56).png>)

### **Invoke transaction to set identity**

Once you have filled in the information you would like to store on-chain, click Set Identity to submit the transaction. Now you have set the identity information on-chain, but that is not verified yet, so you should see a little grey icon beside your name. It is the time to interact with the Astar registrar by submitting the judgment request, to verify your account.

### **Request Judgement**

Go to [Developer->Extrinics](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.polkadot.io#/extrinsics) and select your account to submit the identity **** `requestJudgement(reg_index, max_fee)` transaction. This will request the registrar to validate the information you set on-chain earlier.

![Request Judgement](<../../.gitbook/assets/image (64).png>)

The `reg_index` is the position of the registrar. For Astar and Shiden, use **0**. Maarten, VP of Growth, is set as registrar for Astar ecosystem.

The `max_fee` is the amount of ASN or SDN to pay the registrar. For Shiden use 1 SDN and for Astar use 0 ASN. Note that in the future, a fee may be charged for the Astar registrar.

### **Verification**

If everything has been verified successfully, you will see that your account verification status has been marked with a green tick icon on the [Accounts](https://polkadot.js.org/apps/#/accounts) page. Congratulations! Your identity should now show as a green "verified" checkmark on Polkadot-JS Apps.

## Registrars

Registrars can set a fee for their services and limit their attestation to certain fields. For example, a registrar could charge 1 SDN to verify one's legal name, email, and Discord username. When a user requests judgement, they will pay this fee to the registrar who provides the judgement on those claims. Users set a maximum fee they are willing to pay and only registrars below this amount would provide judgement.

### Judgements

After a user injects their information on-chain, they can request judgement from a registrar. Users declare a maximum fee that they are willing to pay for judgement, and registrars whose fee is below that amount can provide a judgement.

When a registrar provides judgement, they can select up to six levels of confidence in their attestation:

* **Unknown**: The default value, no judgement made yet.
* **Reasonable**: The data appears reasonable, but no in-depth checks (e.g. formal KYC process) were performed.
* **Known Good**: The registrar has certified that the information is correct.
* **Out of Date**: The information used to be good, but is now out of date.
* **Low Quality**: The information is low quality or imprecise, but can be fixed with an update.
* **Erroneous**: The information is erroneous and may indicate malicious intent.

A seventh state, "fee paid", is for when a user has requested judgement and it is in progress. Information that is in this state or "erroneous" is "sticky" and cannot be modified; it can only be removed by the complete removal of the identity.

Registrars gain trust by performing proper due diligence and would presumably be replaced for issuing faulty judgements. To be judged after submitting your identity information, go to the ["Extrinsics UI"](https://polkadot.js.org/apps/#/extrinsics) and select the identity pallet, then `requestJudgement`. For the `reg_index` put the index of the registrar you want to be judged by, and for the max\_fee put the maximum you're willing to pay for these confirmations.

If you don't know which registrar to pick, first check the available registrars by going to ["Chain State UI"](https://wiki.polkadot.network/docs/learn-identity#) and selecting `identity.registrars()` to get the full list.

### **Canceling Judgements**

You may decide that you do not want to be judged by a registrar (for instance, because you realize you entered incorrect data or selected the wrong registrar). In this case, after submitting the request for judgement but before your identity has been judged, you can issue a call to cancel the judgement using an extrinsic.

To do this, first, go to the ["Extrinsics UI"](https://polkadot.js.org/apps/#/extrinsics) and select the identity pallet, then `cancelRequest`. Ensure that you are calling this from the correct account (the one for which you initially requested judgement). For the `reg_index`, put the index of the registrar from which you requested judgement.

Submit the transaction, and the requested judgement will be canceled.

## **Sub Accounts**

Users can also link accounts by setting "`sub accounts`", each with its own identity, under a primary account. The system reserves a bond for each `sub account`. An example of how you might use this would be a validation company running multiple validators. A single entity, "My Staking Company", could register multiple `sub accounts` that represent the [Stash accounts](https://wiki.polkadot.network/docs/learn-keys) of each of their validators.

{% hint style="info" %}
An account can have a maximum of 100 sub-accounts.
{% endhint %}

To register a `sub-account` on an existing account, you must currently use the [Extrinsics UI](https://polkadot.js.org/apps/#/extrinsics). There, select the identity pallet, then `setSubs` as the function to use. Click "`Add Item`" for every child account you want to add to the parent sender account. The value to put into the Data field of each parent is the optional name of the sub-account. If omitted, the sub-account will inherit the parent's name and be displayed as parent/parent instead of parent/child. **Note that a deposit of a certain amount is required for every sub-account.**

****\
****You can use [polkadot.js/apps](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.polkadot.io#/chainstate/constants) again to verify this amount by querying the `identity.subAccountDeposit` constant.

## **Clearing and Killing an Identity**

**Clearing:** Users can clear their identity information and have their deposit returned. Clearing an identity also clears all `sub accounts` and returns their deposits.

To clear an identity:

1. Navigate to the [Accounts UI](https://polkadot.js.org/apps/#/accounts).
2. Click the three dots corresponding to the account you want to clear and select 'Set on-chain identity'.
3. Select 'Clear Identity', and sign and submit the transaction.

![](<../../.gitbook/assets/image (72).png>)

{% hint style="info" %}
Killing: The Council can kill an identity that it deems erroneous. This results in a slash of the deposit.
{% endhint %}

