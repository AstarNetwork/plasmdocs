# About Plasm Constitution

Plasm is a library for handling Plasma chains in Substrate. Plasm initially only envisaged the development of SRML (Substrate Runtime Module Library). However, we decided to change the policy and divide the Plasm library into multiple components to make it easier for users to deploy Plasma applications. Accordingly, Plasma adopted the Plasma Group Spec (PGSpec) as the standard implementation standard for Plasma. However, PGSpec is supposed to have Ethereum as the parent chain. Therefore, Plasm modifies PGSpec to a design suitable for Substrate. The following is the overall structure of Plasm PGSpec.

| <img width="688" alt="pgspec_all" src="https://user-images.githubusercontent.com/6259384/64493951-a2997d80-d2c1-11e9-816d-08041010169b.png"> |
|:--:| 
| *Plasma Group Spec optimized for Substrate(refer to https://docs.plasma.group/projects/spec/en/latest/src/05-client-architecture/introduction.html)* |


We decided to develop the Plasma specification and default implementation using ink !, a smart contract on Substrate. This is called **Plasm Contract**.

Plasm also handles child chain databases. This assumes the following content. Use Substrate to implement a child chain database and its endpoints. This is called **Plasm Childchain**.

Operators and user roles are implemented as client applications that hit the endpoints of the child chain appropriately. The client application that hits SubstrateNode is called ** Plasm Client **.