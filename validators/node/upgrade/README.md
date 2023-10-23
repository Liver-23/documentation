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

# Upgrade

The following guide will help you manually upgrade `cascadiad`.



**Step 1: Initiate the upgrade proposal.**

On the chain side, the upgrade proposal will be initiated and pass through governance.



**Step 2: Stop the `cascadiad` service.**

```javascript
sudo systemctl stop cascadiad
```



**Step 3: Navigate to the home directory.**

```javascript
cd $HOME
```



**Step 4: Download the latest Cascadia release.**

{% code overflow="wrap" %}
```javascript
curl -L https://github.com/CascadiaFoundation/cascadia/releases/download/v0.1.7/cascadiad
```
{% endcode %}

{% hint style="info" %}
The latest `cascadiad` binary release can be found on [GitHub](https://github.com/cascadiafoundation/cascadia/releases).
{% endhint %}



**Step 4: Make the downloaded file executable.**

```javascript
chmod +x cascadiad
```



**Step 5: Replace the existing Cascadia binary with the latest version.**

```javascript
sudo mv cascadiad $(which cascadiad)
```

Alternatively, use the following command to replace the binary:

{% code overflow="wrap" %}
```
wget https://github.com/CascadiaFoundation/cascadia/releases/download/v0.1.7/cascadiad -O $(which cascadiad)
```
{% endcode %}



**Step 6: Restart the `cascadiad` service.**

```javascript
sudo systemctl restart cascadiad
```
