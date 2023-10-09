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

# Node

Once your instance is created on [Google Cloud](https://cascadia.gitbook.io/gitbook/validators/virtual-machine/google-cloud-setup), click the **"SSH"** button to open the terminal window.  For [AWS](https://cascadia.gitbook.io/gitbook/validators/virtual-machine/aws-setup), click the **"EC2 Instance Connect''** button.



**Step 1: Install prerequisites.**

Update the local package list and install available upgrades.

{% code overflow="wrap" %}
```javascript
sudo apt update && sudo apt upgrade -y
sudo apt install make build-essential gcc git
```
{% endcode %}

&#x20;

**Step 2: Install Go.**

{% code overflow="wrap" %}
```javascript
wget https://golang.org/dl/go1.19.2.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.19.2.linux-amd64.tar.gz
```
{% endcode %}

For non-standard configuration, utilize the `.profile` user's home folder (i.e. `~/`).

{% hint style="info" %}
Go can also be downloaded [here](https://golang.org/doc/install).  Please install **Go v1.19.2** or the latest version.
{% endhint %}

####

**Step 3: Export.**

```javascript
GOROOT=/usr/local/go
```

```javascript
GOPATH=$HOME/go
```

```javascript
GO111MODULE=on
```

{% code overflow="wrap" %}
```javascript
PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```
{% endcode %}



**Step 4: Update your `~/.profile`.**

```javascript
source ~/.profile
```



**Step 5: Build Cascadia from source.**

{% code overflow="wrap" %}
```javascript
curl -L https://github.com/CascadiaFoundation/cascadia/releases/download/v0.1.6/cascadiad -o cascadiad
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

**Step 6: To confirm that the installation has succeeded, run:**

```javascript
cascadiad version
```



**Step 7: Initialize the chain.**

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
cascadiad init ubuntu --chain-id cascadia_6102-1
```
{% endcode %}



**Step 8: Download the genesis file.**

Download and replace the Cascadia Testnet `genesis.json` by:

{% code overflow="wrap" %}
```javascript
curl -LO https://github.com/CascadiaFoundation/chain-configuration/raw/master/testnet/genesis.json.gz
gunzip genesis.json.gz
cp genesis.json ~/.cascadiad/config/
```
{% endcode %}



**Step 9: Set persistent peers.**

Persistent peers allow your node to connect to other nodes and join the network.

{% code overflow="wrap" %}
```javascript
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$(curl  https://raw.githubusercontent.com/CascadiaFoundation/chain-configuration/master/testnet/persistent_peers.txt)\"/" ~/.cascadiad/config/config.toml
```
{% endcode %}



**Step 10: Set minimum gas price.**

In `~/.cascadiad/config/app.toml`, update the min gas price to avoid transaction spam.

{% code overflow="wrap" %}
```javascript
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025aCC\"/" ~/.cascadiad/config/app.toml
```
{% endcode %}



**Step 11: Create `systemd` service file.**

{% code overflow="wrap" %}
```javascript
sudo nano /etc/systemd/system/cascadiad.service
```
{% endcode %}



**Step 12: Copy/paste the following configuration, save, and exit.**

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



**Step 13: Start your Node.**

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



Congratulations, you've successfully set up a Cascadia node!

Next, we'll move on to installing a [validator](../installation.md).
