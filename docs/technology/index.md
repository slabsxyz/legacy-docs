# Introduction

Let's start with a one line definition for our protocol:

!!! info "Security Labs Key Management Protocol"
    Security Labs Key Management Protocol (sLabs KMP) is a **Permission-less peer-to-peer network protocol for key management.**

**Key management** refers to the additional set of responsibilities users are given as a cost of managing their identity themselves: an unavoidable side effect of decentralization in Web3. This set of responsibilities are attached to not losing some **cryptographic token**, about which we talk more [here](overview.md#cryptographic-token), but in a nutshell is any data that allows someone to have identity inside some set of agents and access-control and operation over some set of resources shared among.

### **Permission-less**
To be a _permission-less_ network means to be open for everyone to participate as a node, by just following the specifications to be one; there is no central authority who can modify the state and operations of the network, nor it is necessary to "ask for permission" to (i.e. get approved by) said central authority.

This property is important since managing cryptographic tokens ourselves is a core desirable property of web3 systems: to preserve users' autonomy over their identity, data and operations.

### **Key Management Abstraction**
Key Management Abstraction (KMA) let anyone store cryptographic tokens for later retrieval through simple and intuitive authentication interface to mitigate risk currently associated to private keys:

1. **Loss risk**: Risk of losing your private key, losing in the process access to all associated assets.
2. **Theft risk**: Risk of your private key being held by another unintended person/agent, which could imply loss of assets or inappropriate use of identity, even if you still hold access to them yourself.
3. **Unavailability risk**: Risk of private key not being available in some specific dApp context, commonly when choosing a different browser or device.
4. **Usability risk**: Risk of getting users stuck on the dApp user-flow due to export/import or other managing aspects of the private key, commonly encountered when trying to use different devices or dApps with what could be interpreted by the user as "the same account", but really being subtly more complicated under-the-hood due to Web3's nature.

We abstract key management operations like private key storage and retrieval by expressing users' identities over a decentralized and permission-less infrastructure as a map between **intuitive authentication methods** (i.e. traditional web2 authentication, preferably biometrics, behavior-based and hardware-based) to **cryptographic tokens**.

!!! tip "Next Steps: [State Observing Network](state_observing_network#state-observing-network)"
    Key management abstraction is achieved by our [State Observing Network](state_observing_network#state-observing-network), an ephemeral mix network strategy to over a peer-to-peer infrastructure which coordinates securely the storage for [state change authentication](overview#state-change-authentication-scheme) to map intuitive and familiar authentication methods to secure decentralized and cryptographic methods. Read more on this [high-level view](state_observing_network#state-observing-network), or in our [whitepaper](https://docsend.com/view/dbk48wukd3ivd3ad)
