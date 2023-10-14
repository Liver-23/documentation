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

# Installation

**Step 1: Install lz4, if needed.**

```
sudo apt update
sudo apt install snapd -y
sudo snap install lz4
```

\
**Step 2: Download the snapshot.**

{% code overflow="wrap" %}
```
wget -O cascadia_latest.tar.lz4 https://snapshot.cascadia.foundation/$(curl -s https://snapshot.cascadia.foundation/info.txt | jq -r .filename) --inet4-only
```
{% endcode %}



**Step 3: Stop your node.**

```
sudo systemctl stop cascadiad
```

\
**Step 4: Reset your node.**

{% code overflow="wrap" %}
```
cascadiad tendermint unsafe-reset-all --home $HOME/.cascadiad --keep-addr-book
```
{% endcode %}

{% hint style="info" %}
**Warning:** This will erase your node database. If you are already running a validator, be sure you backed up your `priv_validator_key.json` before running the command. The command does not wipe the file. However, you should already have a backup of it in a safe location.
{% endhint %}



**Step 5: Decompress the snapshot to your database location.**

Your database location will be something to the effect of `~/.cascadiad` depending on your node implementation.

{% code overflow="wrap" %}
```
lz4 -c -d cascadia_latest.tar.lz4 | tar -x -C $HOME/.cascadiad data
```
{% endcode %}



**Step 6: Restart your node.**

```
sudo systemctl start cascadiad
```



**Step 7: Remove the downloaded snapshot to free up space.**

```
rm -v cascadia_latest.tar.lz4
```



**Step 8: Make sure that your node is running.**

```
sudo systemctl status cascadiad
sudo journalctl -u cascadiad -f
```

{% hint style="info" %}
The above solution requires you to download the compressed file, uncompress it and then delete the original file. This requires extra storage space on your server.&#x20;
{% endhint %}

Run the following combo command to stream the snapshot into your database location.  This is for advanced users only:

{% code overflow="wrap" %}
```
curl -o - -L https://snapshot.cascadia.foundation/$(curl -s https://snapshot.cascadia.foundation/info.txt | jq -r .filename) | lz4 -c -d - | tar -x -C $HOME/.cascadiad data
```
{% endcode %}
