# FAQ

To begin this FAQ, it's very important for all users to DYOR (Do Your Own Research). We will help provide all the information you need to know. It's still your responsibility when locking up funds. **Make sure you only get information from official channels!**

{% embed url="https://wiki.polkadot.network/docs/learn-scams" %}
Learn how to protect yourself from scams
{% endembed %}

## Crowdloan

#### What is a parachain slot crowdloan and how can I participate?

Astar choose to use Polkadot’s [crowdloan](https://wiki.polkadot.network/docs/en/learn-crowdloans#docsNav) mechanism to help back their parachain slot lease bid. To participate in a crowdloan, users agree to lock up a portion of DOT for the duration of the parachain slot lease period, after which they can be unlocked. To participate in a crowdloan, you must have a transferable balance of DOT, so if your tokens are currently locked due to staking, you’ll need to unbond them in advance of the crowdloan campaign. The unbonding period on Polkadot is currently 28 days.&#x20;

#### What are the benefits of participating in a crowdloan campaign?

Read more about the benefits of our Polkaot Parachain Auction strategy.

#### Is there a minimum contribution amount to participate in a crowdloan?

Yes, the current minimum crowdloan contribution is 5 DOT. A minimum contribution amount is necessary to prevent spam and to facilitate the smooth operation of the crowdloan mechanism.

#### Why do crowdloan campaigns have a maximum amount of total allowed contributions?

Setting a maximum contribution amount allows teams to place a cap on the rewards that they are willing to offer crowdloan contributors. For example, if a team decides to award contributors with a certain distribution of their native token for every DOT contributed, this allows them to cap the maximum distribution they are willing to make.&#x20;

## Auction

#### What happens to the DOT locked up for the duration of the lease?&#x20;

DOT locked for the duration of the parachain’s lease period remains in the index for the campaign, and it is reserved and unavailable for other uses such as staking. At the conclusion of the slot lease, the full amount of DOT is unlocked, after which it is once again free to be used for activities such as transfers, withdrawals, and staking. For crowdloans, contributed DOT is locked from the moment the contribution is made until the end of the lease, unless the crowdloan campaign is unsuccessful in securing a slot via auction, in which case contributed DOT is unlocked at the end of the campaign as specified by the parachain team.

#### What does a slot lease cost?&#x20;

The cost of leasing a parachain slot will purely be a function of market supply and demand, so it’s difficult to give any meaningful estimate as to what the bid requirement will be. However, it's important to realize that the actual cost of a parachain slot is not the same as the size of the parachain bid. Since parachain bonds are returned at the conclusion of the slot lease, the actual cost of running a parachain is best characterized as the opportunity cost of not staking those DOT for the duration of the lease. The need to run collators is an additional but relatively minor cost.&#x20;

#### What is the duration of a slot lease?&#x20;

Do parachains have to bid for the full duration? Parachain teams can bid for leases in contiguous increments of 1 to 8 12-week periods (from a minimum of 12 weeks to a maximum of 96 weeks). After the lease is over, the slot will go up for auction again and the team will need to bid again if they wish to retain a slot (or connect as a parathread once that feature has launched). Parachain slots are fungible, so to avoid any downtime in connectivity and minimize the risk of losing a subsequent auction, teams can bid on and secure an adjacent slot before their current lease ends.

#### What happens if a parachain team loses a slot auction?&#x20;

They will need to join a subsequent auction and bid again. Once parathread functionality is delivered (expected some months after parachains launch), parachain teams will have the option of connecting to Polkadot as a parathread while they attempt to secure a dedicated slot. In the case of crowdloan campaigns, a campaign can be set up to last for several auctions to increase the chances of winning a slot. If a team does not win a slot by the end of their set crowdloan campaign endpoint, the total amount of contributed DOT is once again unlocked and the team will need to initiate a new campaign if they wish to continue participating in auctions.

#### Why were these lease periods/limits chosen?&#x20;

The method for dividing the parachain slot leases into 12-week periods was partly inspired by the desire to allow for a greater amount of parachain diversity, and to prevent particularly large and well-funded parachains from hoarding slots. By making each lease period 12 weeks but the total slot deployment period 96 weeks, the mechanism can cope with well-funded parachains that will ensure they secure a slot at the end of their lease, while gradually allowing other parachains to enter the ecosystem to occupy the 12-week durations that are not filled.&#x20;

#### Are there other ways of securing a parachain slot besides the candle auction?&#x20;

Parachains considered a common-good for the entire network can be added to a slot via governance vote. Common-good chains are parachains viewed as a common-good, in the sense that they will benefit the entire network, for example a bridge that apps on Polkadot could use to connect to an external network like Bitcoin or Ethereum. Chains are designated as a common-good parachain by network governance, which can vote to allocate the chain an empty slot on the Relay Chain, thereby bypassing the auction process. Common-good chains can be thought of as system-level and public utility chains that provide functions and benefits to the network that builders can tap into.
