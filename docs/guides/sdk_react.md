---
title: "SDK + React: Quickstart guide"
date: 2023-08-12T15:31:44-06:00
draft: false
ShowToc: true
---

Welcome to your friendly guide to using [`@dippixyz/base`](#steps-using-dippixyzbase) and [`@dippixyz/react-sdk`](#steps-using-dippixyzreact-sdk) 🚀. Please [contact us](mail:hello@dippi.xyz) if you face any problems implementing!

**Please note the following frequent issues before you begin:**

1. This SDK is written in JS —you’ll need to run this on Node version ≥ 18. This SDK uses fetch as a request manager.
2. The [`@dippixyz/base`](#steps-using-dippixyzbase) SDK can be used both in your backend or your frontend!
3. Need to keep users in the main site while they signup/sign in? We understand! To enable this for your site and your users we recommend you use the iFrame code provided ahead. Keep in mind you can always choose how to display our site.
4. We have developed a suite of components that are included in [`@dippixyz/react-sdk`](#steps-using-dippixyzreact-sdk) to help you set up your web3 enabled website: sign up, login, reset password, change password, and signing and sending token transactions (More functionalities coming soon!). *The components in [`@dippixyz/react-sdk`](#steps-using-dippixyzreact-sdk) are only usable on the frontend.*

### **Steps using `@dippixyz/base`:**

### Step 1: Getting your API token and Application ID

Go to our site: [client.dippi.xyz](http://client.dippi.xyz/). Once there you must create a project. That project will be loaded with all the necessary configurations to be used as rules when creating wallets for your users.

<!-- ![Create Project](/static/img/site1.png) -->
<!-- Show img /static/img/site1.png -->
  <!-- <img src="/static/img/site1.jpg" alt="Site1" /> -->
<!-- [![Site1](../../static/img/site1.jpg)](../../static/img/site1.jpg) -->
![Site 1](site1.jpg)

You’ll find the following form next:

![Site 2](site2.png)

Here’s what you need to know about each of the fields:

1. **App name**: Choose any name to identify the application you are registering.
2. **Environments**: Decide if the user wallets will be generated in test net or main net.
3. **Assigned to:**  Define the desired chain in which the wallet will be created.
4. **Authentication Type**: Define the type of authentication that will be shown to your users when they signup/sign in with Dippi. They’ll have two options:
    1. Email: the user will receive a confirmation email
    2. SMS : the user will receive a OTP via SMS to confirm their account.
5. **Generate API Token** : This will automatically generate an API Token for your app. You’ll use this API Token in the SDK as the requested credentials.

Example:

![Site 3](site3.png)

> ⚠️ IMPORTANT: Once your project is created you’ll obtain an API Token and Application ID: make sure to store these safely —back them up and don’t lose them!

Note: The `API Token`  can’t be recovered if lost. If you ever lose this, you’ll need to generate a new one. To create a new Token follow this guide: {{link}}

### Step 2: Installation and the button component

Once your `API Token` and `Application ID` are ready you can start using our SDK.

The example provided below assumes that you are using **`React + Typescript`** as a framework for your frontend. ***As mentioned earlier the methods provided by the SDK can also be used in your backend***.

1. Install the SDK. If you want to view the package in npm, click below: 
    
    [npm: @dippixyz/base](https://www.npmjs.com/package/@dippixyz/base)
    
    Open your project’s terminal and run this command: 
    
    ```sh
    npm i @dippixyz/base
    ```
    
    1. Once the SDK is installed you can import it this way:
    
    ```js
    const Dippi = require('@dippixyz/base');
    ```
    
    1. We recommend creating an environment variable in your project (`.env`) or a separate file where you can store your credentials without exposing them in your code.
        
        *Assuming you have created a new .env file, you should get the following parameters:*
        
        ```js
        DIPPI_API_TOKEN = <*YOUR_API_TOKEN*>
        DIPPI_APPLICATION_ID = <*YOUR_APPLICATION_ID*>
        DIPPI_URL = https://api.dippi.xyz 
        ```
        
    
    ***The `DIPPI_URL` parameter should always be the one in the example above.***
    
    1. Next we’ll create a new component which will contain the **‘Sign-in with Dippi’** button.
    
    *Example: create a new file in your components folder—*
    
    `/components/dippi.tsx`
    
    ```js
    import React, { useState } from 'react';
    const Dippi = require('@dippixyz/base');
    
    function DippiSignin() {
        
        return (
            <div>
                <button style={{backgroundColor: 'white', borderRadius:5, borderColor:'white' , margin:4, padding:'5px 20px 5px 20px', border:1, boxShadow: '1px 2px 4px grey' }} >
                    <img src="https://client.dippi.xyz/assets/img/logo.png" alt="Dippi Icon" style={{width:30, marginRight:4}}/>
                    <span ><strong>Continue with Dippi</strong></span>
                </button>        
            </div>
        );
    }
    
    export default DippiSignin;
    ```
    
    Hooray! Your button should look like this:
    
    ![Site 4](site4.png)
    
    ***Bear in mind that this is just the basic component. You can build it up and enhance it with what you learn throughout this tutorial.***
    
    1. Once the SDK is imported you can create the `DippiClient` with the following settings:
        
        
        ```js
        const DippiClient = new Dippi({
            appToken: process.env.DIPPI_API_TOKEN,
            appId: process.env.DIPPI_APPLICATION_ID,
            url: process.env.DIPPI_URL,
            urlReturn: 'http://localhost:3002/dippi'
        });
        ```
        
        ***The `urlReturn` parameter is the URL of your project where the DippiClient will  return the responses to your requests.***
        
    
    1. Create an asynchronous function called `initClientDippi()` that will be used to initialize the `DippiClient`:
    
    ```js
    const initClientDippi = async () => {
        const { accessToken } = await DippiClient.auth.login();
        DippiClient.setAuthToken(accessToken);
    }
    ```
    
     - The **`login()`** function returns an object containing an **`accessToken`** that is assigned to the **`accessToken`** variable. This is achieved by de-structuring the returned object.
    
    - Next, **`DippiClient.setAuthToken(accessToken)`** is used to set the access token on the Dippi client. This will allow the client to perform authenticated operations later on.
    
    1. Declare a function called `openIframeDippi()` which will set parameters of the iFrame  displayed to the user —such as size, margins, and other options:
    
    ```js
    const openIframeDippi = async () => {
        await initClientDippi();
        const { url } = await DippiClient.auth.getUrl();
        const left = (window.innerWidth - 500) / 2;
        const top = (window.innerHeight - 650) / 2;
        const options = `toolbar=0,scrollbars=1,status=1,resizable=1,location=1,menuBar=0,width=500,height=650,top=${top},left=${left}`;
        window.open(url, 'childWindow', options);
        localStorage.removeItem('registration_complete');
     };
    ```
    
    ***Note that  `initClientDippi()` is implicit in this method and it will initialize the `DippiClient`. You will then obtain the URL to be displayed in the iFrame through the `getUrl()` method.***
    
    1. Let’s add the `openIframeDippi()` to the button in the previously created component. This will be executed with the onClick event.
    
    ```js
    <button onClick={openIframeDippi} style={{backgroundColor: 'white', borderRadius:5, borderColor:'white' , margin:4, padding:'5px 20px 5px 20px', border:1, boxShadow: '1px 2px 4px grey' }} >
        <img src="https://client.dippi.xyz/assets/img/logo.png" alt="Dippi Icon" style={{width:30, marginRight:4}}/>
        <span ><strong>Continue with Dippi</strong></span>
    </button>
    ```
    
    Great work! Let’s test the button and check for the modal. It should look like this:
    
    ![Site 5](site5.png)
    
    From this point forward everything becomes user experience: your site/app is ready to onboard and log in users through Dippi 🙌
    
    > ⚠️ IMPORTANT: The credentials used in this modal ***are NOT*** the ones you used when registering on [client.dippi.xyz](http://client.dippi.xyz/) to create your project. *Again: these are credentials created by the user to be interact with your site.*
    
    Please refer to the users’ side of the process in this guide: {{A user’s guide to Dippi}}
    

### Step 3: Managing Component's response

Now that the component is ready, you’ll manage the response obtained from Dippi once the user is done with the process:

1. Are you using the code we provided earlier to set up an iFrame or floating window? Then you must define a `window.addEventListener`  which will expect the `window.opener.postMessage` message sent by Dippi
    
    
    ```js
    window.addEventListener('message', async (event) => {
            
        const registration_complete = localStorage.getItem('registration_complete');       
        const legit_registration_event_completed = 
            event.data.type == 'registration_complete' && 
            !registration_complete && 
            event.origin == 'https://client.dippi.xyz'; // (1)
    
        if (legit_registration_event_completed) {
            // Verify that the origin of the event is from our official site.
            localStorage.setItem('registration_complete', 'true'); 
    
            const { redirectUrl, userId, walletAddress } = event.data;
        }
    
    });
    ```

    1. :rocket: This verifies that the origin of the event is from our official site. 
    

In `event.data` you should expect an object like this:

```js
{ 
	redirectUrl : "http://localhost:3002/dippi/success/0x7A61081Afd7354385CbE97c718djnflasb2Bd/cljrqklo0983nrp1bf9zzr1j5"
	type : "registration_complete"
	userId : "cljrqklo0983nrp1bf9zzr1j5"
	walletAddress : "0x7A61081Afd7354385CbE97c718djnflasb2Bd"
}
```

> ⚠️ IMPORTANT: If you are not using the iFrame (instead obtaining a URL through the `DippiClient.auth.getUrl()` method) and get directed to our site, ***the action you will receive in response will be a redirection to a URL with the following structure:***

`${returnUrl}/success/${wallet.address}/${userId}`

Where `returnUrl` is the established parameter in the `DippiClient`, followed by `/success` —indicating that everything worked to spec: `wallet.address` will be the address for the generated wallet, and  `userId` the registered user identifier.

Here’s how something like that would look like: 

```sh
http://localhost:3002/dippi/success/0xa0c903C2756e7ceA093246346C249194701d7805/cljrp5uh30005rp1b3wifc4wr
```

*If an error occurs and you want to handle it, the URL will have the following structure:*

`*${returnUrl}/error/${error}*`

Ready? Extract the second parameter in this case and proceed.

1. You can now obtain the complete user information to register it in your database and assume that their session has been initiated. To do this, define a new asynchronous method called `getUser()` which will obtain the users’ information:
    
    
    ```js
    const getUser = async (userId : string) => {
        await initClientDippi();
        const user = await DippiClient.user.getProfile(userId);
        console.log('user :::: >>>', user)
    }
    ```
    
    In the `window.addEventListener` one must add the call for the `getUser()` function after the `const { redirectUrl, userId, walletAddress } = event.data;` line.
    
    ***The complete method would look like this:***
    
    ```js
    window.addEventListener('message', async (event) => {
            
        const registration_complete = localStorage.getItem('registration_complete');       
    
        if (event.data.type == 'registration_complete' && !registration_complete && event.origin == 'https://client.dippi.xyz') {
            // Verify that the origin of the event is from our official site.
            // Save in local storage registration_complete = true
            localStorage.setItem('registration_complete', 'true');
    
            const { redirectUrl, userId, walletAddress } = event.data;
            await getUser(userId); // Add getUser function
        }
    
    });
    ```
    
    The `await DippiClient.user.getProfile(userId)` method returns a response like this:
    
    ```js
    {
    	applicationId : "clj68i4fs0001qx1bxyb7abks"
    	createdAt : "2023-07-06T17:30:00.277Z"
    	email : "victor@dippi.xyz"
    	id : "cljrfawno0009rp1bznxl8k2h"
    	isActive : true
    	isVerified : true
    	lastLogin : null
    	name : "victor+kjnasdlk2"
    	password : "$argon2id$v=19$m=65536,t=3,p=4$Q3Nrs3SWfCIYoLOnj6fY3Q$or1LYlbWgf3uDfWW+7WrKP9r5D4/43U28eVWhQvS35w"
    	phone : ""
    	refreshToken : null
    	updatedAt : "2023-07-06T17:30:21.794Z"
    }
    ```
    

***Once this information is received, you can use it as necessary in your application to start the users’ session.***

1. The final component would look like this:

```js
import React, { useState } from 'react';
const Dippi = require('@dippixyz/base');

function DippiSignin() {

    const DippiClient = new Dippi({
        appToken: process.env.DIPPI_API_TOKEN,
        appId: process.env.DIPPI_APPLICATION_ID,
        url: process.env.DIPPI_URL,
        urlReturn: 'http://localhost:3002/dippi'
    });

    const initClientDippi = async () => {
        const { accessToken } = await DippiClient.auth.login();
        DippiClient.setAuthToken(accessToken);
    }

    const openIframeDippi = async () => {
        await initClientDippi();
        const { url } = await DippiClient.auth.getUrl();
        const left = (window.innerWidth - 500) / 2;
        const top = (window.innerHeight - 650) / 2;
        const options = `toolbar=0,scrollbars=1,status=1,resizable=1,location=1,menuBar=0,width=500,height=650,top=${top},left=${left}`;
        window.open(url, 'childWindow', options);
        localStorage.removeItem('registration_complete');
    };

    window.addEventListener('message', async (event) => {
        
        const registration_complete = localStorage.getItem('registration_complete');
        
        if (event.data.type == 'registration_complete' && !registration_complete && event.origin == 'https://client.dippi.xyz') {
            // Verify that the origin of the event is from our official site.
            // Save in local storage registration_complete = true
            localStorage.setItem('registration_complete', 'true');

            const { redirectUrl, userId, walletAddress } = event.data;
            await getUser(userId);            
        }

    });

    const getUser = async (userId : string) => {
        await initClientDippi();
        const user = await DippiClient.user.getProfile(userId);
        console.log('user :::: >>>', user)
    }

    return (
        <div>
            <button style={{backgroundColor: 'white', borderRadius:5, borderColor:'white' , margin:4, padding:'5px 20px 5px 20px', border:1, boxShadow: '1px 2px 4px grey' }} onClick={openIframeDippi}>
                <img src="https://client.dippi.xyz/assets/img/logo.png" alt="Dippi Icon" style={{width:30, marginRight:4}}/>
                <span ><strong>Continue with Dippi</strong></span>
            </button>
        </div>
        
    );
}

export default DippiSignin;
```

### **Steps using `@dippixyz/react-sdk`:**

### Step 1: Get your API token and Application ID as mentioned [previously](#step-1-getting-your-api-token-and-application-id)

### Step 2: Create a simple React app

1. Create a simple React app using your favorite React app creation command, for the sake of this example we're using vite. So go to your terminal and run
```bash
npm create vite@latest
```
*Note: This tutorial was made using Vite v5.0.12, so if the flow for creating your project is different from the instructions you find in this tutorial you can do ```npm create vite@5.0.12``` instead.*
2. Type your *project_name*. We're using `dippi-react` as our project name.
3. Select React as your framework.
4. Select TypeScript + SWC as your variant.
5. Go into the `dippi-react` folder and run `npm install`.
```bash
cd dippi-react; npm install;
```
6. Install our frontend SDK `@dippixyz/react-sdk`
```bash
npm install @dippixyz/react-sdk
```
7. Go to `src/main.tsx` and import the `@dippixyz/react-sdk` `DippiProvider`. This is used to handle communication with the Dippi Backend infrastructure.
```typescript
import { DippiProvider} from '@dippixyz/react-sdk';
```
8. Once you've imported the `DippiProvider` you have to initialize it using the `API Token` and `Application Id` that you got during [Step 1](#step-1-getting-your-api-token-and-application-id). We will do this by declaring a constant named `DippiConfig` and replacing the `API Token` and `Application Id` values.
```typescript
const dippiConfig = {
    appToken: [API Token],
    appId: [Application Id]
    url: 'https://api.dippi.xyz'
};
```
Then we will proceed to add the DippiProvider component as a wrapper that will help keep your entire application secured and the `Dippi Context` data available at all times to perform operations using our suite of components. This is how your `src/main.tsx` should look once you've added the `DippiProvider` with its corresponding `dippiConfig` prop.
```typescript
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App.tsx';
import './index.css';
import { DippiProvider} from '@dippixyz/react-sdk';

const dippiConfig = {
    appToken: [API Token], // remember to replace with API Token value
    appId: [Application Id] // remember to replace with Application Id value
    url: 'https://api.dippi.xyz'
};

ReactDOM.createRoot(document.getElementById('root')!).render(
    <React.StrictMode>
        <DippiProvider config={dippiConfig}>
            <App />
        <DippiProvider />
    </React.StrictMode>,
)
```
Now you're ready to start implementing our suite of frontend components!
9. Next, we're going to set up our login and sign up functionality. Go to `src/App.tsx` and import the `ButtonSignin` component and the CSS styles from `@dippixyz/react-sdk`
```typescript
import { ButtonSignIn } from '@dippixyz/react-sdk';
import '@dippixyz/react-sdk/dist/index.css';
```
10. Now replace the code on lines 9 - 34 with the following:
```typescript
    return (
        <>
            <div className='card'>
                <ButtonSignIn />
            </div>
        </>
    )
```
Your `src/App.tsx` should look like this now:
```typescript
import { useState } from 'react';
import reactLogo from './assets/react.svg';
import viteLogo from '/vite.svg';
import './App.css';
import { ButtonSignIn } from '@dippixyz/react-sdk';
import '@dippixyz/react-sdk/dist/index.css';

function App() {
    return (
        <>
            <div className='card'>
                <ButtonSignIn />
            </div>
        </>
    )
};

export default App;
```
11. Remove unused imports on lines 1 through 3 from `src.App.tsx`. Your code should look like this now:
```typescript
import './App.css';
import { ButtonSignIn } from '@dippixyz/react-sdk';
import '@dippixyz/react-sdk/dist/index.css';

function App() {
    return (
        <>
            <div className='card'>
                <ButtonSignIn />
            </div>
        </>
    )
};

export default App;
```
12. Run your application by typing the following in your terminal:
```bash
npm run dev
```
You should see the Dippi Sign in button on the screen. Test out the functionality, sign up, create a wallet, encrypt the private key and login to your application.
13. Once you've got the login setup, you can use the rest of our components and take advantage of the Dippi context to protect your application. We're going to add the sign and send transaction functionality to your application. First, you need to import the `TransactionForm` component into `src/App.tsx`.
```typescript
import { TransactionForm } from '@dippixyz/react-sdk';
```
The TransactionForm receives props that can vary according to the Web3 provider that you selected. For the time being we are supporting all providers currently supported by Ethers v6: [Alchemy](https://www.alchemy.com/), [Ankr](https://www.ankr.com/), [Cloudflare](https://www.cloudflare.com/application-services/products/web3/), [Etherscan](https://etherscan.io/register), [Infura](https://www.infura.io/), [Pocket](https://www.pokt.network/), [QuickNode](https://www.quicknode.com/).
Click on any of the providers to get your API key and project id which should be passed as a prop to the provider of your choice. For the sake of this guide we will be using [Alchemy](https://www.alchemy.com/).
Add the `TransactionForm` component to `src/App.tsx` on line 10 and send the `_network` (can be the chain id or the name of the network eg.: `1` or `Mainnet`), `provider` (eg.: `Alchemy`) and `apiKey`.
```typescript
<TransactionForm _network={1} provider={'Alchemy'} apiKey='Your API key' />
```
*Note: The apiKey may also be called `_apiKey`, `projectSecret`, or `applicationSecret` according to the provider you selected and can also be paired with an `applicationId` or `projectId`.*

### Voilá! Dippi and your app should work like magic now! 

Thanks for following this tutorial. Got suggestions? Don’t hesitate and let us know 🤓