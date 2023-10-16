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

**Step 1: Download snapshot**

{% code overflow="wrap" %}
```
curl -o - -L https://snapshot.cascadia.foundation/$(curl -s https://snapshot.cascadia.foundation/info.txt | jq -r .filename) | lz4 -c -d - | tar -x -C $HOME/.cascadiad data
```
{% endcode %}

**Step 2: Create `systemd` service file.**

{% code overflow="wrap" %}
```javascript
sudo nano /etc/systemd/system/cascadiad.service
```
{% endcode %}



**Step 3: Copy/paste the following configuration, save, and exit.**

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



**Step 4: Start your Node.**

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
