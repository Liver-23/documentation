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

# Manual

To manually delegate tokens using **`cascadiad`**, follow the instructions below:

{% code overflow="wrap" %}
```javascript
cascadiad tx staking delegate <validator_address> <amount> --from <wallet_name> --chain-id cascadia_6102-1 --gas auto --gas-adjustment=1.2 --gas-prices 7aCC -y
```
{% endcode %}

**For example:**

{% code overflow="wrap" %}
```javascript
cascadiad tx staking delegate cascadiavaloper1zec8f7faf880q7l9s8dehz2054lnavfsuuf3gt 25000000000000000000000aCC --from ubuntu --chain-id cascadia_6102-1 --gas auto --gas-adjustment=1.2 --gas-prices 7aCC -y
```
{% endcode %}

<table data-header-hidden><thead><tr><th width="260">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>&#x3C;validator_address></code></td><td>The address of the validator you want to delegate tokens.</td></tr><tr><td><code>&#x3C;amount></code></td><td>The amount of tokens you want to delegate.</td></tr><tr><td><code>--from &#x3C;wallet_name></code></td><td>Specifies the wallet you want to use for delegation.</td></tr><tr><td><code>--gas-prices</code></td><td>Sets the gas price for the transaction.</td></tr></tbody></table>



Get more information by running the following command:

{% code overflow="wrap" %}
```javascript
cascadiad tx staking delegate --help
```
{% endcode %}
