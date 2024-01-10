---
title: "SDK + Node + Express"
date: 2023-08-10T15:31:44-06:00
draft: false
ShowToc: true
updated: 2023-08-24
# cover: 
#     image: "img/wall.jpg"
#     alt: "This is a photo."
#     caption: "This is the caption."
---
# Backend API Documentation

This document provides **technical** documentation for the backend API of your application and can go in-depth. In case of looking for a quickstart, look at our [SDK + React guide](sdk_react.md).

The backend is developed using Node.js and Express framework, and it comprises various routes that handle different functionalities such as user management, wallet operations, application handling, authentication, and more.

## **Introduction**

The backend API plays a pivotal role in the functionality and success of your application. It's designed to seamlessly handle various crucial tasks such as managing users, facilitating wallet operations, handling applications, enabling secure authentication, and more. To streamline these operations and provide enhanced features, your backend leverages the power of the **`@dippixyz/base`** library.

### **The Power of `@dippixyz/base`**

One of the core strengths of this backend lies in its integration with the **`@dippixyz/base`** library. This SDK offers a comprehensive set of tools and functionalities that empower your backend to interact seamlessly with the Dippi platform. By leveraging the capabilities of the **`@dippixyz/base`**, your backend gains access to a wealth of features that simplify application management, user authentication, wallet handling, and more.

The **`@dippixyz/base`** library serves as the bridge between your backend and the Dippi ecosystem. It encapsulates intricate processes, allowing you to focus on building an efficient and feature-rich backend without the need to handle intricate details manually. With the power of the SDK, your backend can execute actions smoothly and securely, offering a seamless experience to your users.

## Introduction

The backend API is responsible for handling various functionalities of your application. It is built using Node.js and Express, providing a set of routes that interact with different models to manage users, wallets, applications, authentication, and more.

## Routes

### Application Router

The `application-router.js` handles operations related to application management.

- `GET /dippi/application/list`: Retrieve a list of applications.
- `POST /dippi/application/create`: Create a new application.
- `GET /dippi/application/retrieve/:id`: Retrieve application details by ID.
- `PUT /dippi/application/update/:id`: Update application details by ID.

### Application Token Router

The `application-token-router.js` manages application tokens.

- `GET /dippi/application-token/retrieve/:id`: Retrieve application token details by ID.

### Auth Router

The `auth-router.js` is responsible for user authentication.

- `POST /dippi/auth/login`: User login to the application.

### User Router

The `user-router.js` handles user-related operations.

- `PUT /dippi/user/updateProfile`: Update user profile.
- `GET /dippi/user/getProfile`: Retrieve user profile.

### Wallet Router

The `wallet-router.js` manages wallet operations.

- `GET /dippi/wallet/list`: Retrieve a list of wallets.
- `GET /dippi/wallet/retrieve/:id`: Retrieve wallet details by ID.
- `PUT /dippi/wallet/update/:id`: Update wallet details by ID.
- `POST /dippi/wallet/recovery/:id`: Recover wallet by ID.
- `GET /dippi/wallet/balance/:id`: Get wallet balance by ID.
- `GET /dippi/wallet/nfts/:id`: Get NFTs associated with a wallet by ID.

### TokenBoundAccount Router

The `tokenBoundAccount-router.js` manages wallet operations.

- `POST /dippi/tokenBoundAccount/create/:data`: Recover TBA by ID.

## Models

### DippiClient Model

The `DippiClient` class encapsulates the initialization and configuration of the `@dippixyz/base` library. This module is essential for establishing a connection between your backend and the Dippi platform. It provides methods to authenticate, set up authentication tokens, and obtain a configured client instance for further interactions with the Dippi platform.

You can get `API KEYS` in **https://client.dippi.xyz** 

#### Constructor

```js
constructor()

```

The constructor of the `DippiClient` class is responsible for creating an instance of the Dippi SDK client with the provided configuration parameters.

- `appToken`: The Dippi application token obtained from the Dippi platform.
- `appId`: The Dippi application ID associated with your application.
- `url`: The URL pointing to the Dippi platform's API : https://api.dippi.xyz

##### Example

```js
const Dippi = require('@dippixyz/base');
require('dotenv').config();

class DippiClient {

    constructor() {
        this.client = new Dippi({
            appToken: process.env.APP_TOKEN,
            appId: process.env.APP_ID,
            url: process.env.CLIENT_URL,
        });
    }

    // ...
}

module.exports = new DippiClient();
```

#### Method: init

```js
async init()
```

The `init` method within the `DippiClient` class handles the authentication process using the Dippi SDK. It performs the login action using the configured client and sets the obtained access token for future API calls.

- It returns a configured Dippi SDK client instance ready to interact with the Dippi platform.

##### Example

```js
async init() {
    const { accessToken } = await this.client.auth.login();
    this.client.setAuthToken(accessToken);
    return this.client;
}
```

### Auth Model

The `auth.js` file defines methods related to user authentication using the Dippi SDK.

#### Method: login

```js
const dippiClient = require('./dippiClient');

const login = async () => {
    const dippi = await dippiClient.init();
    return await dippi.auth.login();
}

module.exports = {
    login,
};
```

### Application Model

The `application.js` file provides methods to interact with the application-related functionalities using the Dippi SDK.

#### Method: list

```js
const dippiClient = require('./dippiClient');

const list = async () => {
    const dippi = await dippiClient.init();
    return await dippi.application.list();
}

module.exports = {
    list,
};
```

#### Method: create

```js
const dippiClient = require('./dippiClient');

const create = async (data) => {
    const dippi = await dippiClient.init();
    return await dippi.application.create(data);
}

module.exports = {
    create,
};
```

#### Method: retrieve

```js
const dippiClient = require('./dippiClient');

const retrieve = async (id) => {
    const dippi = await dippiClient.init();
    return await dippi.application.retrieve(id);
}

module.exports = {
    retrieve,
};
```

#### Method: update

```js
const dippiClient = require('./dippiClient');

const update = async (id, data) => {
    const dippi = await dippiClient.init();
    return await dippi.application.update(id, data);
}

module.exports = {
    update,
};
```

### Application Token Model

The `application-token.js` file provides methods to retrieve application token details using the Dippi SDK.

#### Method: retrieve

```js
const dippiClient = require('./dippiClient');

const retrieve = async (id) => {
    const dippi = await dippiClient.init();
    return await dippi.applicationToken.retrieve(id);
}

module.exports = {
    retrieve,
};
```

### User Model

The `user.js` file defines methods to interact with user-related operations using the Dippi SDK.

#### Method: getProfile

```js
const dippiClient = require('./dippiClient');

const getProfile = async () => {
    const dippi = await dippiClient.init();
    return await dippi.user.getProfile();
}

module.exports = {
    getProfile,
};
```

#### Method: updateProfile

```js
const dippiClient = require('./dippiClient');

const updateProfile = async (data) => {
    const dippi = await dippiClient.init();
    return await dippi.user.updateProfile(data);
}

module.exports = {
    updateProfile,
};
```

### Wallet Model

The `wallet.js` file provides methods to interact with wallet-related operations using the Dippi SDK.

#### Method: list

```js
const dippiClient = require('./dippiClient');

const list = async () => {
    const dippi = await dippiClient.init();
    return await dippi.wallet.list();
}

module.exports = {
    list,
};
```

#### Method: retrieve

```js
const dippiClient = require('./dippiClient');

const retrieve = async (id) => {
    const dippi = await dippiClient.init();
    return await dippi.wallet.retrieve(id);
}

module.exports = {
    retrieve,
};
```

#### Method: update

```js
const dippiClient = require('./dippiClient');

const update = async (id, data) => {
    const dippi = await dippiClient.init();
    return await dippi.wallet.update(id, data);
}

module.exports = {
    update,
};
```

#### Method: recovery

```js
const dippiClient = require('./dippiClient');

const recovery = async (id, data) => {
    const dippi = await dippiClient.init();
    return await dippi.wallet.recovery(id, data);
}

module.exports = {
    recovery,
};
```

#### Method: balance

```js
const dippiClient = require('./dippiClient');

const balance = async (id) => {
    const dippi = await dippiClient.init();
    return await dippi.wallet.balance(id);
}

module.exports = {
    balance,
};
```

#### Method: nfts

```js
const dippiClient = require('./dippiClient');

const nfts = async (

id) => {
    const dippi = await dippiClient.init();
    return await dippi.wallet.nfts(id);
}

module.exports = {
    nfts,
};
```

<!-- ## Conclusion

This documentation provides an overview of the backend API routes and their corresponding functionalities, as well as the models responsible for handling various operations. Developers can refer to this documentation to understand how to interact with the backend API, manage users, applications, wallets, authentication, and more, while utilizing the `@dippixyz/base` library effectively.

This document provides technical documentation for the backend API of your application. The backend is developed using Node.js and Express framework, and it comprises various routes that handle different functionalities such as user management, wallet operations, application handling, authentication, and more. -->


### tokenBoundAccount Model

The `tokenBoundAccount.js` file provides methods to interact with tokenBoundAccount-related operations using the Dippi SDK.

#### Method: create

```js
const TBA = require('@dippixyz/base');

const create = async (data) => {
    const TBAClient = new TBA(paramsOauthSession);
    TBAClient.init(tbaCreateOptions)
    return await TBAClient.create();
}

module.exports = {
    create,
};
```