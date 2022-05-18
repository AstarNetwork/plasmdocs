# How to send USDC from Polygon to Astar Network

In this tutorial, we will guide you through the process for making a cross-chain USDC transfer from Polygon to Astar.

## **Go to cBridge**

Visit our bridge from cBridge:

{% embed url="https://cbridge.celer.network/#/transfer" %}

## **Connect Your Wallet**

Before you explore the different features offered by cBridge, you will need to connect your wallet.

Click "Connect Wallet", and you will be prompted to select a wallet. (cBridge currently only supports MetaMask on desktop browsers, with more types of wallets supported on mobile).

![](<../../.gitbook/assets/image (125) (1) (1) (1).png>)

![](<../../.gitbook/assets/image (124) (1) (1) (1).png>)

Select MetaMask, and you should now see your wallet address and your current chain in the top right corner of the page.

![](<../../.gitbook/assets/image (110).png>)

![](<../../.gitbook/assets/image (120) (1) (1) (1).png>)

## **Transfer Tokens Across Chains**

Let’s say, you want to transfer 50 USDC from Polygon to Astar. The steps are made simple in cBridge:

Select "Polygon" in the dropbox next to "From" and "Astar" in the dropbox next to "To".

![](<../../.gitbook/assets/image (129) (1).png>)

You will be prompted to switch your wallet to Polygon if it's not already connected. Click “Approve” to add a network and then click “Switch network”.

![](<../../.gitbook/assets/image (115) (1) (1).png>)

![](<../../.gitbook/assets/image (119) (1) (1) (1) (1).png>)

Enter the amount you want to send under "Send". You should see the estimated amount you will receive under "Receive (estimated)".

![](<../../.gitbook/assets/image (118) (1) (1).png>)

You can adjust the Slippage Tolerance of the transfer. Your transfer may fail with a very low Slippage Tolerance. It’s usually between 0.1% and 0.5%.

![](<../../.gitbook/assets/image (112) (1) (1).png>)

Note that there will be a difference between the amount you send and the amount you receive, which is determined by the Bridge Rate and fees. For the exact definition of each item in the transaction, check the tooltips next to each of the terms.

![](<../../.gitbook/assets/image (123) (1) (1) (1) (1).png>)

Review your transfer details and click "Transfer". You will receive a popup to confirm transfer.

![](<../../.gitbook/assets/image (121) (1) (1) (1) (1) (1).png>)

![](<../../.gitbook/assets/image (127) (1) (1).png>)

Click "Confirm Transfer" and you will be prompted with a USDC spend confirmation on MetaMask. Click "Confirm", and your transaction will be finalized in a few minutes.

![](<../../.gitbook/assets/image (114) (1).png>)

After USDC is approved, you will be prompted on cBridge to confirm the cross-chain transfer. Review the transfer details and click "Confirm".

![](<../../.gitbook/assets/image (126) (1) (1).png>)

After confirming on MetaMask, you will receive a Transfer Submitted popup.

![](<../../.gitbook/assets/image (113) (1).png>)

You can also check the transaction status in “Pending” in the top right corner of the page.

![](<../../.gitbook/assets/image (117) (1).png>)

It takes some extra time for the funds to arrive at your wallet on the destination chain. On MetaMask, you can switch to the destination chain, which in our case is Astar, to check if you have received the funds.

![](<../../.gitbook/assets/image (122) (1) (1) (1) (1).png>)

Alternatively, you can also view your transaction status via the Polygon Explorer, which can be accessed via a link in your transaction history.

![](<../../.gitbook/assets/image (128) (1) (1).png>)

In cases where your transfer fails due to insufficient liquidity on the destination chain or an unfavorable slippage tolerance, you will receive a popup explaining the reason for the failure. You can click "Request Refund" in the transfer history.

And voila! Congratulations on completing a successful USDC transfer from Polygon to Astar on cBridge!
