---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Hardhat

These are the steps for verifying smart contracts via [Hardhat](https://hardhat.org/). Hardhat is a comprehensive development environment that facilitates contract compilation, deployment, and authentication.



**Step 1: Install Hardhat.**

{% hint style="info" %}
If creating a new npm project from scratch, navigate to an empty directory and execute the command `npm init`. Follow the instructions provided, and it is recommended to use npm 7 or a later version. Once the project is ready, use either the `npm` or `yarn` command below.
{% endhint %}

npm instructions:

{% code overflow="wrap" %}
```javascript
npm install --save-dev hardhat
```
{% endcode %}

yarn instructions:

{% code overflow="wrap" %}
```javascript
yarn add --dev hardhat
```
{% endcode %}



**Step 2:** Install the [Hardhat plugin](https://hardhat.org/hardhat-runner/plugins/nomiclabs-hardhat-etherscan) (requires v3.0.0+). Use either the `npm` or `yarn` commands:

npm instructions:

{% code overflow="wrap" %}
```javascript
npm install --save-dev @nomiclabs/hardhat-etherscan
```
{% endcode %}

yarn instructions:

{% code overflow="wrap" %}
```javascript
yarn add --dev @nomiclabs/hardhat-etherscan
```
{% endcode %}



#### **Step 3: For `hardhat.config.js`, add the following statement:**

{% code overflow="wrap" %}
```js
require("@nomiclabs/hardhat-etherscan");
```
{% endcode %}

For TypeScript, add the following line to `hardhat.config.ts`:

{% code overflow="wrap" %}
```javascript
import "@nomiclabs/hardhat-etherscan";
```
{% endcode %}



**Step 4: Add Cascadia to `hardhat.config.js`.**

{% code overflow="wrap" %}
```js
etherscan: {
  apiKey: {
    cascadia: "abc"
  },
  customChains: [
    {
      network: "cascadia",
      chainId: 6102,
      urls: {
        apiURL: "https://explorer.cascadia.foundation/api",
        browserURL: "https://explorer.cascadia.foundation",
      }
    }
  ]
}

```
{% endcode %}

`apiKey`: Refers to the unique API key associated with the block explorer account.

`network`: Specifies the name of the network, which must match the name of the apiKey.

`browserURL`: Indicates the URL for accessing the block explorer interface.

`chainID`: Identifies the unique identifier for the network chain being accessed.

`apiURL`: Specifies the URL used for accessing the block explorer's API service.

The entire code should appear as follows:

{% code overflow="wrap" %}
```js
require("@nomicfoundation/hardhat-toolbox");
require("@nomiclabs/hardhat-etherscan");
require('dotenv').config()
const private_key = process.env.PRIVATE_KEY
module.exports = {
  solidity: "0.8.17",
  networks: {
    cascadia: {
      url: "https://testnet.cascadia.foundation",
      accounts: [private_key]
    }
  },
  etherscan: {
    apiKey: {
      cascadia: "abc"
    },
    customChains: [
      {
        network: "cascadia",
        chainId: 6102,
        urls: {
          apiURL: "https://explorer.cascadia.foundation/api",
          browserURL: "https://explorer.cascadia.foundation",
        }
      }
    ]
  }
};
```
{% endcode %}



**Step 5: Check if Cascadia is successfully supported:**

{% code overflow="wrap" %}
```javascript
npx hardhat verify --list-networks
```
{% endcode %}



**Step 6: To verify the contract, constructor arguments can be included with the verify task.**

{% code overflow="wrap" %}
```javascript
npx hardhat verify --network <network_name> DEPLOYED_CONTRACT_ADDRESS “Constructor argument 1”
```
{% endcode %}

**For example:**

{% code overflow="wrap" %}
```javascript
npx hardhat verify –network Cascadia 0x856C336cD8eBDCE7B5Bb3F2DEB1bf3160B176880 31536000
```
{% endcode %}



**Step 7: Contract verification can be confirmed via the console:**

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>
