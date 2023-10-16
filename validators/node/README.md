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

# Joining Testnet

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



**Step 7: Sync your node to the network.**

There are three main ways to sync a node to the network:

1. [Sync from Snapshot](sync-from-snapshot.md)
2. [Sync with State-Sync](state-sync.md)
3. [Upgrade](upgrade/) your current node if you're running one already

After completing one of the above, continue with Step 8.



**Step 8: Create `systemd` service file.**

{% code overflow="wrap" %}
```javascript
sudo nano /etc/systemd/system/cascadiad.service
```
{% endcode %}



**Step 9: Copy/paste the following configuration, save, and exit.**

Replace `<username>` with your own account name.

{% code overflow="wrap" %}
```javascript
[Unit]
Description=Cascadia Node
After=network.target
 
[Service]
Type=simple
User=<username>
WorkingDirectory=/usr/local/bin
ExecStart=/usr/local/bin/cascadiad start --trace --log_level info --json-rpc.api eth,txpool,personal,net,debug,web3 --api.enable
Restart=on-failure
StartLimitInterval=0
RestartSec=3
LimitNOFILE=65535
LimitMEMLOCK=209715200
 
[Install]
WantedBy=multi-user.target
```
{% endcode %}

In the following example, our `<username>` is `ubuntu`:

{% code overflow="wrap" %}
```javascript
[Unit]
Description=Cascadia Node
After=network.target
 
[Service]
Type=simple
User=ubuntu
WorkingDirectory=/usr/local/bin
ExecStart=/usr/local/bin/cascadiad start --trace --log_level info --json-rpc.api eth,txpool,personal,net,debug,web3 --api.enable
Restart=on-failure
StartLimitInterval=0
RestartSec=3
LimitNOFILE=65535
LimitMEMLOCK=209715200
 
[Install]
WantedBy=multi-user.target
```
{% endcode %}

{% hint style="info" %}
Press ctrl + s to save, then ctrl + x to exit.
{% endhint %}



**Step 10: Start your Node.**

```javascript
# reload service files
sudo systemctl daemon-reload
```

```javascript
# create the symlink
sudo systemctl enable cascadiad.service
```

```javascript
# start the node
sudo systemctl start cascadiad.service
```

```javascript
# show logs
journalctl -u cascadiad -f
```
