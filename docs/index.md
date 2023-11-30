# Welcome to Dippi's documentation

## Quickstart

You can start by looking at our guides:

- Guide for using our [SDK with React](guides/sdk_react.md).
- Guide for using our [SDK with React Native and Expo](guides/sdk_reactNative_expo.md).
- Guide for using our [SDK with node and express](guides/sdk_node_express.md).
- Guide for using [TBAs (Token Bound Accounts) through our SDK with express](guides/sdk_tba_express.md).

Or have a deeper look with our [whitepaper](https://docsend.com/view/dbk48wukd3ivd3ad).

## What's Dippi? A little bit of history...

??? abstract "TL;DR for those in a hurry"
    1. Dippi abstracts **private key management** with a permission-less peer-to-peer network, allowing users to use private keys **across several devices and dApps**. 
    2. Solving the private-key management problem (in a **non-custodial way**) is an unavoidable obstacle to Web3 widespread adoption: An expected, but still non-trivial, infrastructure revolution we are leading.
    3. We have over a year of research on distributed secure storage for sensitive data and have developed our own **general framework, SCAS (State-change authentication schemes)**, for authentication methods compatible with our protocol, which include all usual authentication pipelines which don't require users to remember a password or seedphrase (biometrics, hardware-based, behavior-based authentications).
    4. **Token Bound Accounts (TBAs)**, which are NFTs which are also smart contract accounts, has allowed us to study wallet-usage pain points further, as well as showing an **even bigger need for better private key management**, since they present a large and rich set of use cases as **"portable digital profiles"**, making losing private keys even a bigger issue for the future of on-chain identity and NFT ecosystems.
    5. Dippi is **leader** on the TBA market, representing **more than 60% of the deployed and used TBAs on Polygon mainnet**, with more than **160k TBA wallets**.
 
Dippi is a **permission-less peer-to-peer network for cryptographic tokens** (more on our [concepts overview](technology/overview.md)), which is a really specific way of saying: <u>We protect and retrieve private keys without having them, by using a decentralized network</u>. This not only allows users to mitigate **wallet-loss** and **theft risk**, but also provide a seamless dApp experience across devices and platforms without even knowing what a private key is.

A simplified version of _how_ we do it can be summarized as: 

> MPC-based multisig without the burden of finding where store the shards, by **storing them distributively** on a **permission-less** and **trust-less** network whose security scales as it becomes more **decentralized**, by leveraging unpredictable traffic mixing with ephemeral time-based mix networks with entropy injection.

Further details can be explored on our [whitepaper](https://docsend.com/view/dbk48wukd3ivd3ad), which gives the theoretical foundations of our research to create a general enough authentication framework with [decentralization-driven security](technology/overview.md#decentralization-driven-security) as a core property; that is one of the results of our first year of research about the topic.

Our initial interest in tackling the private key retrieval problem stems from experiencing (a little too much...) the classic and obvious web3 infrastructure problem: 

> [Usability](technology/overview.md#usability) (not only onboarding) suffers from **complex message signing** and **high risk to lose your assets** if not mindful enough. 

Both of these problems originate from expecting the user to know "_basic_" key management practices (or accepting a custodial solution...), limiting in the process Web3 ecosystem's capacity to scale to widespread adoption. Even what could be considered _basic_ knowledge on Web3 ecosystems, should not be a requirement for the general audience to know before using a Web3-based product and being burdened by it only shows how Web3 still is in its infancy; albeit not for much longer.

Technology infrastructure revolutions have almost always come in the form of improving ease-of-use for some underlying powerful but complex technology by abstracting it to not require specialized expertise (web browsers, DNS servers, cloud storage syncing, etc.). Web3 is not exception. [Key management abstraction](technology/overview.md#key-management-abstraction) is a natural cornerstone to achieve usability in dApps, and it **MUST** be permission-less and trust-less for it to be usable and general enough for any future dApp and still preserve decentralization benefits (autonomy of data, privacy, etc.)

To study the impact and market demand for our product, as well as to test hypotheses after our initial research, we embarked into the newest emerging technologies in the space, and found a perfect fit for one of our core objects we have been researching: On-chain identity/personality, through [Token Bound Accounts](technology/overview.md#token-bound-accounts) (TBAs). 

TBAs have deep expressivity capabilities, as briefly discussed on our [concepts' page](technology/overview.md#token-bound-accounts), and additionally, represent on-chain personalities (*smart profiles*, as we named them) which would be great to link with an intuitive decentralized identity, ideally managed with "web2-like" authentication. This is exactly what we do.

After entering the TBAs market, we have already captured more than 60% market share on Polygon Mainnet, with more than 160k TBA wallets within just 6 weeks, proving not only the massive interest of the ecosystem around TBAs' capabilities, but also their interest in our project. 

Today, Dippi still is innovating and building to lead the infrastructure revolution we all need to make Web3 truly usable, accessible and scalable.

<!-- ## Why integrate with Dippi?

??? abstract "TL;DR for those in a hurry"
    placeholder

placeholder -->