# Kusama Parachain Lease Offering

Parachain Lease Offering a.k.a PLO consists of **Parachain Slots Auction** and **Parachain Crowdloans**. In this section, we are going to explain how to make a Kusama/Polkadot address, crowdloan, and auction.

{% content-ref url="../polkadot-plo/how-to-make-a-kusama-polkadot-address.md" %}
[how-to-make-a-kusama-polkadot-address.md](../polkadot-plo/how-to-make-a-kusama-polkadot-address.md)
{% endcontent-ref %}

{% content-ref url="crowdloan.md" %}
[crowdloan.md](crowdloan.md)
{% endcontent-ref %}

{% content-ref url="auction.md" %}
[auction.md](auction.md)
{% endcontent-ref %}

{% content-ref url="shiden-parachain-auction-strategy.md" %}
[shiden-parachain-auction-strategy.md](shiden-parachain-auction-strategy.md)
{% endcontent-ref %}

{% content-ref url="joining-from-polkadot.js.md" %}
[joining-from-polkadot.js.md](joining-from-polkadot.js.md)
{% endcontent-ref %}

{% content-ref url="joining-from-exchanges/" %}
[joining-from-exchanges](joining-from-exchanges/)
{% endcontent-ref %}

{% content-ref url="joining-from-fearless.md" %}
[joining-from-fearless.md](joining-from-fearless.md)
{% endcontent-ref %}

{% content-ref url="joining-from-mathwallet.md" %}
[joining-from-mathwallet.md](joining-from-mathwallet.md)
{% endcontent-ref %}

First of all, the following figure shows the timeline.

![](../../.gitbook/assets/9f850028b62217a3d21d482ff3d65c94d0d036e9\_2\_1380x374.png)

**Step1 Crowdloan:** A crowdloan campaign is started before the first auction. Crowdloan mechanism allows people to contribute by agreeing to lock up their own KSM until the end of the lease. We reward their contributors after winning the auction. Crowdloan participants can get more rewards than auction participants.

**Step2 Auction: **Parachain slot auctions follow a modified [candle auction](https://wiki.polkadot.network/docs/en/learn-auction#mechanics-of-a-candle-auction) format, where the exact endpoint of the auction is unknown by participants in order to prevent auction sniping for more accurate price discovery.

**Step3 Launch: **After winning the Parachain auction, we will launch Shiden/Astar Network as a Parachain.

### **Reference**:&#x20;

{% embed url="https://kusama.network/auctions" %}

{% embed url="https://wiki.polkadot.network/docs/en/learn-auction" %}

{% embed url="https://wiki.polkadot.network/docs/en/learn-crowdloans" %}

{% embed url="https://blog.coinlist.co/a-deep-dive-into-polkadots-parachain-auctions-and-crowdloans/" %}

