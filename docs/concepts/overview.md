# Basic concepts

Dippi is a **Permission-less peer-to-peer network for cryptographic tokens**. Let's unpack word by word:

### **Cryptographic token**
by _cryptographic_ token we mean any piece of _organized data_ which serves the purpose of singling out some _property_ to just one entity (person, agent, etc; depending on the context). For example, a private key in a [public-key cryptosystem](https://en.wikipedia.org/wiki/Public-key_cryptography) attributes the keyholder a unique identity by differentiating messages signed by said key, as well as producing secret communication (encrypted) communication, giving them agency over what they communicate to whom, while providing their identity.  

Another example is simple username and password pairs on a centralized database, since they give access control based on the central authority's backend rules. In general, we called them "cryptographic" since their structure _hides information_ that allow asymmetric capabilities to the holders.

### **Permission-less**
To be a _permission-less_ network means to be open for everyone to participate as a node, by just following the specifications to be one; there is no central authority who can 

### **Usability**
It's common to say that Web3 has an "onboarding" problem, referring to the process of bringing new users into some specific user experience, but frequently leaving aside the fact that, even if onboarded, dApps' user experience by itself is lacking proper polish. When we talk about _good usability_ on Dippi, we refer to the property of a dApp to allow its users to operate without any special knowledge (about private keys, blockchain, tokens, etc.) with web2-like UX.

### **Key Management Abstraction**
Key Management Abstraction (KMA) let anyone store cryptographic secrets for later retrieval through simple and intuitive authentication to mitigate risk currently associated to private keys: 

1. **Loss risk**: Risk of losing your private key, losing in the process access to all associated assets.
2. **Theft risk**: Risk of your private key being held by another unintended person/agent, which could imply loss of assets or inappropriate use of identity, even if you still hold access to them yourself.
3. **Unavailability risk**: Risk of private key not being available in some specific dApp context, commonly when choosing a different browser or device.
4. **Usability risk**: Risk of getting users stuck on the dApp user-flow due to export/import or other managing aspects of the private key, commonly encountered when trying to use different devices or dApps with what could be interpreted by the user as "the same account", but really being subtly more complicated under-the-hood due to Web3's nature.

We abstract key management operations like private key storage and retrieval by expressing users' identities over a decentralized and permission-less infrastructure as a map between **intuitive authentication methods** (i.e. traditional web2 authentication, preferably biometrics, behavior-based and hardware-based) to **cryptographic tokens**.


### **State-Change Authentication Token**
Our own **cryptographic data-structure** in charge of holding **shares of cryptographic tokens** to be secured along with enough **authentication information** for observers (our network nodes) to authenticate users through a challenge-response procedure, verified distributively across several of them, **without jeopardizing** its contents.

Apart from the cryptographic token share, coming from a perfect-security splitting procedure and further secured, it contains standardized information about the authentication token (e.g. biometric data, hardware key, etc.) as a dynamical system's state space being evolved uniquely by said token, providing a general framework for time-distributed authentication methods (e.g. behavioral biometrics, on-chain identity, etc.). 