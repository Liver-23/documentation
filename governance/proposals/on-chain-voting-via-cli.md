# On-Chain Voting via CLI

CascadiaFarms offers an on-chain voting mechanism. Follow the instructions below:



**Step 1: Open your Command Line Interface (CLI)**



**Step 2: Input the following command:**

{% code overflow="wrap" %}
```
cascadiad tx gov vote <proposal_number> <your_vote_choice> --gas-prices 7aCC --from <your_key_name> --node https://rpc.cascadia.foundation:443
```
{% endcode %}

* Replace `<proposal_number>` with the actual number of the proposal you wish to vote on (e.g., 23).
* Replace `<your_vote_choice>` with your desired vote choice (e.g., yes, no, abstain).
* Replace `<your_key_name>` with the name of your key.



For users who wish to automatically adjust the gas price, you can add the following at the end of the previous command. This allows the system to determine the best gas price for your transaction and adjust it by a factor of 2.

```
--gas auto --gas-adjustment 2
```

{% hint style="info" %}
Always ensure you're voting on the correct proposal number and double-check your choices before confirming.
{% endhint %}

{% hint style="info" %}
Make sure your CLI environment is set up correctly and that you have sufficient funds to cover any transaction fees.
{% endhint %}
