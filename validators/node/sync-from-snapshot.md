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

**Download snapshot.**

{% code overflow="wrap" %}
```
curl -o - -L https://snapshot.cascadia.foundation/$(curl -s https://snapshot.cascadia.foundation/info.txt | jq -r .filename) | lz4 -c -d - | tar -x -C $HOME/.cascadiad data
```
{% endcode %}
