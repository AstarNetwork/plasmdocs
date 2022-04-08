# Auction

## Parachain Slot Auctions

Parachains connect to Polkadot by leasing a slot on the Relay Chain for up to 96 weeks at a time, with the option to renew. Parachain slots are assigned by an on-chain auction, with auction winners locking up a bond in DOT for the duration of the lease. Auctions and crowdloans raise the bar for blockchain projects, incentivizing them to demonstrate their technology and gain community support prior to launch.

## How Auctions Work

![](<../../.gitbook/assets/image (111) (1) (1) (1) (1) (1).png>)

### Bonding

To bid in an auction, parachain teams agree to lock up (or bond) a portion of DOT tokens for the duration of the lease. While bonded for a lease, the DOT cannot be used for other activities like staking or transfers.

### Auction Cost

After the lease, the full amount of DOT is unlocked, meaning auctions do not require anyone to “spend” DOT. The cost of the lease is best characterized as the opportunity cost of not being able to use the bonded DOT for other activities.

### Crowdloans

Astar will fund their auction bid with the help of a crowdloan campaign, which allows us to accept contributions from DOT holders. Crowdloan contributors get their DOT back at the end of the lease, and Astar choose to reward you in various ways: ASTR tokens + bonus!

### Auction Duration

Auctions on Polkadot have an open bidding period of approximately 1 week. At the end of the bidding period, the precise moment of the auction’s close is determined retroactively. This prevents last-minute “auction sniping” and promotes more accurate price discovery [(See the case for candle auctions)](https://polkadot.network/blog/research-update-the-case-for-candle-auctions/).

### Slot Duration & Lease Periods

Each slot on the Relay Chain can be leased for a maximum duration of 96 weeks. When bidding on a slot, parachains can choose the length of their desired lease by selecting a contiguous range of 12-week increments known as lease periods. Astar will aim for the max amount of 96 weeks!

## Auction Ending Period

Each auction has an ending period that begins approximately 1 day and 18 hours after the start of the auction and lasts until the end of the 1-week bidding period. The auction’s endpoint can be any time within the ending period and is automatically and randomly chosen by the VRF at the close of the 1-week bidding period.

![](<../../.gitbook/assets/image (112) (1) (1) (1).png>)
