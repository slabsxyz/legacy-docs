## Introduction
A threat model involves describing the following aspects:

1. **System objective**: All threat models must begin with an understanding of what the system is intended to do. Most commonly, said intended purpose is to support agents interacting with the system, and the threats come from the possible actions the agents are allowed to do <u>over some set of *assets*</u>, constrained by system rules.
2. **Security definition**: We need to define what we *exactly* mean when we say "we are a *secure* network", preferably in a measurable way. This is done by defining the resources we are trying to protect and properties we are trying to ensure, the ways and extend in which these are being endangered, with respect to the previously stated system objective.
3. **Adversary objectives**: Given the guarantees defined in our security concept, we then must describe the adversary objectives. This may be acquiring some total information (e.g. stealing either a specific target private key, or any private key), or partial information (like progressively learning the locations of specific shards); or may be affecting some network services (the storage, retrieval and/or mixing), either by stopping them, only interrupting them, or spoofing them.
4. **Computational resources assumptions for the adversary**: The adversary is defined by their goals, and hence their incentives, but also their computational resources that will imply some cost of seeking their objective. If this cost, given their computational resources, is too high compared with the incentives, we can assume a lower number (in practice) of adversaries matching that specific attack. Keeping consideration of this number may be specially important when analyzing [decentralization-driven security](../overview#decentralization-driven-security).

## Threat model
### System Objective

The State Observing Network's objective is simple: 

!!! info "State Observing Network objective"
    Store [Cryptographic tokens](../overview#cryptographic-token) (e.g. private keys) in a decentralized, permission-less, trust-less and highly available way, keeping them retrievable through familiar, but flexibly more robust, authentication methods.

In many complex and hierarchical system, we can pinpoint many agent types: Administrators, read-only user, differently limited operators, etc. 

Luckily, in peer-to-peer systems, agent interactions tends to be more symmetric. In the case of Security Labs, we have a few roles one node can be acting in, but symmetry still exists in the sense that each role can be attained by any node without preference in an unpredictable (and thus uncontrollable) way. 

We have the following table explaining them:

| Role | Task |
|:-----|:-----|
| Storage Node | Stores SCAT securely and in a uncorrelated way. | 
| Challenger Node | Challenge making, with MPC within share-state groups and independent challenge verification over homomorphically encrypted data. |
| Entrypoint Node | Receive storage and retrieval requests and acts accordingly updating and broadcasting global network state (by consensus procedure) and re-send data packets through the currently valid mixnet. |
| Mixnet Node | In charge of receiving and re-sending onion messages, "peeling" onion layers by decrypting them before re-sending to the appropriate next node. |
| Pseudo-storage Node | Acts as a storage node to add entropy by noise in the network operations, being unable themselves to know if they are participating in a true storing procedure or not. | 

<!-- These roles interact differently with the relevant system resources. These resources are:

| Resource |  -->

### Security Definition and Adversary Objectives

Let's define specific threats and their associated property at risk:

| Threat | What is it threatening? | Explanation and adversary objective | 
|:-------|:------------------------|:------------|
| [Spoofing](https://en.wikipedia.org/wiki/Spoofing_attack) | Authenticity | Your private key should not be retrievable by no one else. | 
| [Tampering](https://en.wikipedia.org/wiki/Tampering_(crime))| Integrity | Your private key should be available even against unreliable and adversarial nodes. |
| [Data leak](https://en.wikipedia.org/wiki/Data_leak) | Confidentiality | Key shards should be impossible to intercept and extract information from during traffic and when stored. This includes even partial statistical information, with enough significance to make tractable a short to middle term (~100 years) expected reconstruction of the key. |
| [Denial of service](https://en.wikipedia.org/wiki/Denial-of-service_attack) | Availability | We are requiring specific availability assumptions about the following network services: <br><br> 1. **Storage requests**: Storage should be resistant to being forced to stop, however we are allowing slowing down of storage requests inside some reasonable (from the UX perspective) threshold, since slowing down may come not only from direct attacks, but as fluctuations on supply & demand, which are natural. <br><br> 2. **Retrieval requests**: As the main mechanism for private key availability, we require a stricter threshold for allowed slowing than storage requests, but otherwise, the same applies as before. <br><br> 3. **Mixing**: Since mixing ensures decentralization-driven security, we expect not only for it to always fully work, but to be immune to spoofing attacks in the sense that a big enough entity should not be able to impersonate enough nodes in the network such that the whole network operation becomes faulty.|

<!-- Here we have  -->

#### General countermeasures

The following describes point-by-point security countermeasures for the mentioned risks:

- **Spoofing:** The [SCAT](../overview#state-change-authentication-token) leverages Shamir secret sharing (SSS) to introduce threshold security/redundancy with perfect (information theoretic) security guarantees. That means that, even when *some* shards (less than the total) are in hands of the adversary, it is impossible to recover the original key (except, of course, by a brute force search in the complete key space, which is always possible anyway).
- **Tempering:** As explained on several security-related theorems in our [whitepaper](https://docsend.com/view/dbk48wukd3ivd3ad), there is network scale beyond which the network is always resistant (equivalently to a 256-resistance in traditional cryptography) to collusion attacks even of 99% of the network, ensuring resistance against directly adversarial parties. Now, for passive adversaries like unreliable nodes, there is a dynamic measure of redundancy, where the number of redundant nodes for each SCAT is increased (or decreased) in proportion to the success rate of retrieval and storage requests.
- **Data Leak:** The SCATs' batch preparation and mixing during the storage flow ensures data is not leaked during data traffic and the whole storage lifetime. 
- **Denial of Service:** General availability guarantees are protected by the staking and rating mechanisms, based on several global metrics of past successful behavior of the network. The spoofing during mixing is protected again by the scale of the network (past 6k nodes to ensure 256-bit strength against 99%-sized collusion attacks)

<!-- ### Computational resources assumptions TODO-->


