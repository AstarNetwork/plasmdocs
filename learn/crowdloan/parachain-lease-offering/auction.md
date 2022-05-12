# Auction

Parachain slot auctions follow a modified [candle auction](https://wiki.polkadot.network/docs/en/learn-auction#mechanics-of-a-candle-auction) format.&#x20;

{% hint style="info" %}
**If you would like to know more about candle auctions, please visit** [**the official Polkadot wiki**](https://wiki.polkadot.network/docs/en/learn-auction#mechanics-of-a-candle-auction)**.**&#x20;
{% endhint %}

Generally speaking, the exact endpoint of an auction is determined. However, the Polkadot  Parachain auctions don't have the exact endpoint. The endpoint is randomly chosen after the auction and the winning Parachain at the specific point wins the auction. Hence, the best strategy is to encourage contributors to lock KSM as early as possible.

Polkadot and Kusama Network have the same auction mechanism as described below.

**Step1: Choose the lease period**\
We bid for the longest periods and the amount of KSM/DOT we are willing to lock up for the duration of the chosen range.

{% hint style="info" %}
KSM: The lease periods are 1-8 (each lease period is 6 weeks)\
DOT: The lease periods are 1-4 (each lease period is 4 months)
{% endhint %}

&#x20;**Step2: Open bidding** \
****Open bidding and accept KSM/DOT tokens from our community for the duration of the auction.&#x20;

**Step3: The endpoint was randomly chosen**\
****At the end of the auction, the precise moment of the auction’s close is randomly determined by a verifiable random function.

**Step4: Become a Parachain**\
****The winning Parachain is automatically becoming a Parachain. KSM/DOT tokens remain locked for the duration of the lease.

**Step5: Bid another slot**\
****Before expiring the lease period, we will bid another slot to become a Parachain again.

### Sources:

{% embed url="https://kusama.network/auctions" %}

