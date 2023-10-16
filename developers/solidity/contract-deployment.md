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

# Deployment

#### Step 1: Install Hardhat.

```javascript
npm install -g hardhat
```



**Step 2: Create `Example` smart contract project.**

```javascript
mkdir example-project
cd example-project
npx hardhat init
```



**Step 3: Make `.env` and input your private key.**

```javascript
PRIVATE_KEY=<your_private_key>
```



**Step 4: Install `dotenv` module.**

```javascript
npm install dotenv
```



**Step 5: Import environmental variables to `hardhat.config.js`.**

{% code overflow="wrap" %}
```javascript
require('dotenv').config()
const private_key = process.env.PRIVATE_KEY
```
{% endcode %}



**Step 6: Establish endpoint settings.**

By default, the script will be using your local host `"127.0.0.1"` - If you are not running a localhost, you may leverage the public endpoint `https://testnet.cascadia.foundation/` by making changes to `networks` in `hardhat-config.js`, for example:

{% code overflow="wrap" %}
```javascript
networks: {
    cascadia: {
      url: "https://testnet.cascadia.foundation",
      accounts: [private_key]
    }
  },
```
{% endcode %}

The total result code in hardhat.config.js is the following:

{% code overflow="wrap" %}
```javascript
require('dotenv').config()
const private_key = process.env.PRIVATE_KEY
/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.17",
  networks: {
    cascadia: {
      url: "https://testnet.cascadia.foundation",
      accounts: [private_key]
    }
  }
};
```
{% endcode %}



**Step 7: Deploy Contract.**

{% code overflow="wrap" %}
```javascript
npx hardhat run -netork cascadia scripts/deploy.js
```
{% endcode %}



**Step 8: Obtain contract address from console.**

{% code overflow="wrap" %}
```javascript
~/deploy-doc$ npx hardhat run --network cascadia scripts/deploy.js
Lock with 1 CC and unlock timestamp 1706489110deployed to 0xA32C3d322b9e35071c42D03237176D53e15D464
```
{% endcode %}



**Step 9: Confirm successful deployment on Cascadia's** [**block explorer**](https://explorer.cascadia.foundation)**.**

Type your deployed contract address into the block explorer search bar or [https://explorer.cascadia.foundation/address/\<your\_contract\_deployed\_address>](https://explorer.cascadia.foundation/address/%3Cyour\_contract\_deployed\_address) to confirm successful deployment.
