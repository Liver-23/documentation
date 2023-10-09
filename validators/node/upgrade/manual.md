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

This guide will help you manually upgrade the `cascadiad` binary.



**Step 1: Initiate the upgrade proposal.**

On the chain side, the upgrade proposal will be initiated and pass through the governance voting process.



**Step 2: Stop the node.**

Stop the node using the following command:

```javascript
sudo systemctl stop cascadiad
```



**Step 3: Download and replace the new binary.**

The latest `cascadiad` binary release can be found on [GitHub](https://github.com/cascadiafoundation/cascadia/releases).  Download it, and replace the binary with this command:

{% code overflow="wrap" %}
```javascript
wget https://github.com/CascadiaFoundation/cascadia/releases/download/v0.1.6/cascadiad -O $(which cascadiad)
```
{% endcode %}



**Step 4: Restart the cascadiad service.**

Finally, restart the cascadiad service using the command:

```javascript
sudo systemctl restart cascadiad
```
