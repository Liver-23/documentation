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

# Sync from Snapshot

**Step 1: Download a binary file.**

{% code overflow="wrap" %}
```javascript
curl -L https://github.com/CascadiaFoundation/cascadia/releases/download/v0.1.7/cascadiad -o cascadiad
```
{% endcode %}

{% hint style="info" %}
The latest `cascadiad` binary release can also be found on [GitHub](https://github.com/cascadiafoundation/cascadia/releases).
{% endhint %}

```javascript
sudo chmod u+x cascadiad
```

{% code overflow="wrap" %}
```javascript
sudo cp cascadiad /usr/local/bin/cascadiad
```
{% endcode %}

Below, replace `<username>` with your own account name.

{% code overflow="wrap" %}
```javascript
sudo chown <username> /usr/local/bin/cascadiad
```
{% endcode %}

For example, we use the name `ubuntu`.  If you're using Google Cloud, replace the name `ubuntu` with your account name.

{% code overflow="wrap" %}
```javascript
sudo chown ubuntu /usr/local/bin/cascadiad
```
{% endcode %}

####

**Step 2: To confirm that the installation has succeeded, run:**

```javascript
cascadiad version
```



**Step 3: Initialize the chain.**

Replace \[moniker] with your own name and initialize `cascadiad`.

{% code overflow="wrap" %}
```javascript
cascadiad init [moniker] --chain-id cascadia_6102-1
```
{% endcode %}

Moniker will be the displayed id of your node when connected to Cascadia.  When providing a moniker name, drop the square brackets.

For example:

{% code overflow="wrap" %}
```javascript
cascadiad init mynode --chain-id cascadia_6102-1
```
{% endcode %}



**Step 4: Download the genesis file.**

Download and replace the Cascadia Testnet `genesis.json` by:

{% code overflow="wrap" %}
```javascript
curl -LO https://github.com/CascadiaFoundation/chain-configuration/raw/master/testnet/genesis.json.gz
gunzip genesis.json.gz
cp genesis.json ~/.cascadiad/config/
```
{% endcode %}



**Step 5: Set persistent peers.**

Persistent peers allow your node to connect to other nodes and join the network.

{% code overflow="wrap" %}
```javascript
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$(curl  https://raw.githubusercontent.com/CascadiaFoundation/chain-configuration/master/testnet/persistent_peers.txt)\"/" ~/.cascadiad/config/config.toml
```
{% endcode %}



**Step 6: Set minimum gas price.**

In `~/.cascadiad/config/app.toml`, update the min gas price to avoid transaction spam.

{% code overflow="wrap" %}
```javascript
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025aCC\"/" ~/.cascadiad/config/app.toml
```
{% endcode %}



**Download snapshot.**

{% code overflow="wrap" %}
```
curl -o - -L https://snapshot.cascadia.foundation/$(curl -s https://snapshot.cascadia.foundation/info.txt | jq -r .filename) | lz4 -c -d - | tar -x -C $HOME/.cascadiad data
```
{% endcode %}
