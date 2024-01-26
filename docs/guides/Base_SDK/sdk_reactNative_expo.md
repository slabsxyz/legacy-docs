---
title: "SDK + React Native + Expo"
date: 2023-08-11T15:31:44-06:00
draft: false
ShowToc: true
# cover: 
#     image: "/img/wall.jpg"
#     alt: "This is a photo."
#     caption: "This is the caption."
---

<!-- # Documentation ReactNative + Expo: Dippi Sign-in -->
## Introduction

This document aims to explain the provided React Native code that implements Dippi sign-in functionality for mobile applications. The code utilizes various libraries and APIs, including React Native, Expo, and the Dippi SDK, to enable users to sign in using their Dippi accounts.

## Code Overview

### Imports

```js
import React, { useState } from 'react';
import { TouchableOpacity, Text, Button, View, Image, StyleSheet } from 'react-native';
import * as WebBrowser from 'expo-web-browser';
import * as Linking from 'expo-linking';
```

The code begins with importing the required modules and libraries:

- `React` and `useState` from React: Used for creating functional components and managing component state.
- `TouchableOpacity`, `Text`, `Button`, `View`, `Image`, and `StyleSheet` from `react-native`: UI components and styles for building the user interface.
- `WebBrowser` and `Linking` from `expo`: Libraries for opening web browser sessions and handling URLs.

### Dippi SDK Initialization

```js
const Dippi = require('@dippixyz/base');

function DippiSignin() {
    const DippiClient = new Dippi({
        appToken: '...',  // Dippi app token
        appId: '...',     // Dippi app ID
        url: '...',       // Dippi API base URL
        urlReturn: Linking.createURL("")  // Return URL after authentication
    });
}
```

- The Dippi SDK is imported and initialized with necessary parameters: `appToken`, `appId`, `url`, and `urlReturn`.
- `appToken`: Authentication token for the Dippi application.
- `appId`: Identifier for the Dippi application.
- `url`: Base URL for the Dippi API.
- `urlReturn`: The URL where the user will be redirected after authentication.

### Dippi SDK Initialization Function

```js
initClientDippi = async () => {
    const { accessToken } = await DippiClient.auth.login();
    DippiClient.setAuthToken(accessToken);
    const { url } = await DippiClient.auth.getUrl();
    return url;
};
```

- `initClientDippi`: An asynchronous function that initiates the Dippi SDK client.
- The function performs the following steps:
    1. Calls the `login` method of the Dippi authentication module to get an access token.
    2. Sets the obtained access token using the `setAuthToken` method of the Dippi client.
    3. Calls the `getUrl` method of the Dippi authentication module to obtain an authentication URL.
    4. Returns the authentication URL.

### State Management

```js
const [result, setResult] = useState(null);
```

- A component state variable `result` is initialized using the `useState` hook.

### Authentication Session Function

```js
_openAuthSessionAsync = async () => {
    const url = await initClientDippi();

    try {
        let result = await WebBrowser.openAuthSessionAsync(
            url,
        );
        const walletAddress = result.url.split('/')[4];
        const userId = result.url.split('/')[5];

        const user = await DippiClient.user.getProfile(userId);
        setResult(user);
    } catch (error) {
        console.log(error);
    }
};
```

- `_openAuthSessionAsync`: An asynchronous function that initiates the authentication session.
- The function does the following:
    1. Calls the `initClientDippi` function to get the authentication URL.
    2. Uses `WebBrowser.openAuthSessionAsync` to open a browser session with the authentication URL.
    3. Parses the returned URL to extract `walletAddress` and `userId`.
    4. Calls `DippiClient.user.getProfile` with the extracted `userId` to retrieve the user's profile.
    5. Sets the retrieved user profile in the component state using `setResult`.

### Component Rendering

```js
return (
    <>
        <View>
            <Text>Redirect Example</Text>
            <Button
                onPress={this._openAuthSessionAsync}
                title="Continue with Dippi"
            />
            <Text>Result: {JSON.stringify(result)}</Text>
        </View>
    </>
);
```

- The `DippiSignin` component's rendering logic.
- Renders a `View` container with the following components:
    - A `Text` component displaying "Redirect Example".
    - A `Button` component with the text "Continue with Dippi", which triggers the `_openAuthSessionAsync` function when pressed.
    - A `Text` component displaying the result as a JSON stringified version of the `result` state variable.

## Conclusion

The provided React Native code demonstrates how to integrate Dippi sign-in functionality into a mobile application. It uses the Dippi SDK to authenticate users, open an authentication session in a web browser, and retrieve user information after successful authentication. This code can serve as a foundation for building a Dippi sign-in feature in a React Native mobile app.