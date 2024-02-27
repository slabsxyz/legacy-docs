---
title: "SDK + React: Quickstart guide"
date: 2023-08-12T15:31:44-06:00
draft: false
ShowToc: true
---

!!! note "Brand change"
    Currently, several endpoints and libraries have the name **Dippi** which is now Security Labs (sLabs), and may be read as such, although libraries and endpoints still need to be called as the former.

### Step 1: Get your API token and Application ID as mentioned [previously](../Base_SDK/sdk_react.md#step-1-getting-your-api-token-and-application-id)

### Step 2: Create a simple React app

!!! note

    This tutorial was made using Vite v5.0.12, so if the flow for creating your project is different from the instructions you find in this tutorial you can do `npm create vite@5.0.12` instead.

1. Create a simple React app using your favorite React app creation command, for the sake of this example we're using vite. So go to your terminal and run
  ```bash
  npm create vite@latest
  ```
2. Type your _project_name_. We're using `dippi-react` as our project name. 
3. Select React as your framework. 
4. Select TypeScript + SWC as your variant. 
5. Go into the `dippi-react` folder and run `npm install`.
```bash
cd dippi-react; npm install
```
6. Install our frontend SDK `@dippixyz/react-sdk`
  ```bash
  npm install @dippixyz/react-sdk
  ```

### Step 3: Implement the Dippi component

1. Go to `src/main.tsx` and import the `@dippixyz/react-sdk` `DippiProvider`. This is used to handle communication with the Dippi Backend infrastructure.
  ```typescript
  import { DippiProvider } from "@dippixyz/react-sdk";
  ```
2. Once you've imported the `DippiProvider` you have to initialize it using the `API Token` and `Application Id` that you got during [Step 1](#step-1-getting-your-api-token-and-application-id). We will do this by declaring a constant named `DippiConfig` and replacing the `API Token` and `Application Id` values.
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
  Now you're ready to start implementing our suite of frontend components! 9. Next, we're going to set up our login and sign up functionality. Go to `src/App.tsx` and import the `ButtonSignin` component and the CSS styles from `@dippixyz/react-sdk`
  ```typescript
  import { ButtonSignIn } from "@dippixyz/react-sdk";
  import "@dippixyz/react-sdk/index.css";
  ```
3. Now replace the code on lines 9 - 34 with the following:
  ```typescript
  return (
    <>
      <div className="card">
        <ButtonSignIn />
      </div>
    </>
  );
  ```
  Your `src/App.tsx` should look like this now:
  ```typescript
  import { useState } from "react";
  import reactLogo from "./assets/react.svg";
  import viteLogo from "/vite.svg";
  import "./App.css";
  import { ButtonSignIn } from "@dippixyz/react-sdk";
  import "@dippixyz/react-sdk/index.css";

  function App() {
    return (
      <>
        <div className="card">
          <ButtonSignIn />
        </div>
      </>
    );
  }

  export default App;
  ```
4. Remove unused imports on lines 1 through 3 from `src.App.tsx`. Your code should look like this now:
  ```typescript
  import "./App.css";
  import { ButtonSignIn } from "@dippixyz/react-sdk";
  import "@dippixyz/react-sdk/index.css";

  function App() {
    return (
      <>
        <div className="card">
          <ButtonSignIn />
        </div>
      </>
    );
  }

  export default App;
  ```
5. Run your application by typing the following in your terminal:
  ```bash
  npm run dev
  ```
  You should see the Dippi Sign in button on the screen. Test out the functionality, sign up, create a wallet, encrypt the private key and login to your application. 13. Once you've got the login setup, you can use the rest of our components and take advantage of the Dippi context to protect your application. We're going to add the sign and send transaction functionality to your application. First, you need to import the `TransactionForm` component into `src/App.tsx`.
  ```typescript
  import { TransactionForm } from "@dippixyz/react-sdk";
  ```
  The `TransactionForm` receives props that can vary according to the Web3 provider that you selected. For the time being we are supporting all providers currently supported by Ethers v6: [Alchemy](https://www.alchemy.com/), [Ankr](https://www.ankr.com/), [Cloudflare](https://www.cloudflare.com/application-services/products/web3/), [Etherscan](https://etherscan.io/register), [Infura](https://www.infura.io/), [Pocket](https://www.pokt.network/), [QuickNode](https://www.quicknode.com/).
  Click on any of the providers to get your API key and project id which should be passed as a prop to the provider of your choice. For the sake of this guide we will be using [Alchemy](https://www.alchemy.com/).
  Add the `TransactionForm` component to `src/App.tsx` on line 10 and send the `_network` (can be the chain id or the name of the network eg.: `1` or `Mainnet`), `provider` (e.g.: `Alchemy`) and `apiKey`.
  ```typescript
  <TransactionForm _network={1} provider={"Alchemy"} apiKey="Your API key" />
  ```
!!! note 

    The `apiKey` may also be called `_apiKey`, `projectSecret`, or `applicationSecret` according to the provider you selected and can also be paired with an `applicationId` or `projectId`.

### Voilá! Dippi and your app should work like magic now!

Thanks for following this tutorial. Got suggestions? Don’t hesitate and [let us know](mail:hello@dippi.xyz) 🤓
