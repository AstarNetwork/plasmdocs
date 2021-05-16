# ERC721
Example contract for https://docs.plasmnet.io/build/smart-contracts/examples/wasm-create-an-nft

## NFT
This is an ERC721 Token implementation.
This contract demonstrates how to build non-fungible or unique tokens using ink!.

## Warning
This contract is an *example*. It is neither audited nor endorsed for production use.
Do **not** rely on it to keep anything of value secure.

## Error Handling
Any function that modifies the state returns a Result type and does not changes the state if the Error occurs.
The errors are defined as an Enum type. Any other error or invariant violation triggers a panic and therefore rolls back the transaction.

## Token Management
After creating a new token, the function caller becomes the owner.
A token can be created, transferred, or destroyed.

Token owners can assign other accounts for transferring specific tokens on their behalf.
It is also possible to authorize an operator (higher rights) for another account to handle tokens.

## Token Creation
Token creation start by calling the `mint(&mut self, id: u32)` function.
The token owner becomes the function caller. The Token ID needs to be specified as the argument on this function call.

### Token Transfer
Transfers may be initiated by:
- The owner of a token
- The approved address of a token
- An authorized operator of the current owner of a token

The token owner can transfer a token by calling the `transfer` or `transfer_from` functions.
An approved address can make a token transfer by calling the `transfer_from` funtion.
Operators can transfer tokens on another account's behalf or can approve a token transfer
for a different account.

### Token Removal
Tokens can be destroyed by burning them. Only the token owner is allowed to burn a token.
