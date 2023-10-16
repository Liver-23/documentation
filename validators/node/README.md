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



Congratulations, you've successfully set up a Cascadia node!

Next, we'll move on to installing a [validator](../installation.md).
