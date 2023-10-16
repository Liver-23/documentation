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

# Cooldown Period

**Voting Mechanism and Rewards Distribution**

The smart contract introduces a voting mechanism, where each user's aCC balance plays a pivotal role. The quantity of rewards a user receives correlates directly with their aCC balance. After the cooldown period, a user's aCC balance is nullified, ending further rewards.

it's important to note that a user's voting power decreases over time. In addition, users need to re-align their stakes if they want to restore their initial voting power.

The contract operates around the "lock" mechanism, described by the amount of aligned CC and the duration until the lock's expiration.



**Cooldown and Re-Align**

The contract includes a cooldown function that adjusts the align duration from infinite to 365 days. The re-align function can reset the align duration back to infinite. Users can increase their amount anytime, regardless of their status.

A withdrawal or a re-align can be initiated at any point, providing flexibility in asset management. The balance adjustment occurs upon the cooldown activation.



**Contract Modifications**

The contract now defines a minimum and maximum align time of one year, eliminates non-cooldown aligns, and revises all test scenarios. There is a max limit of four years.



**Checkpointing**

To ensure the accuracy of ve-balances, Cascadia implements checkpointing, which calculates slope and bias via locked tokens and lock duration. To this end, a custom integration for new cooldown lock types has been created where the balance remains the same until the cooldown is triggered, as per the specifications below:



**Balance Calculations**

{% code overflow="wrap" fullWidth="false" %}
```javascript
(Amount of CC / MAXTIME) * (((Current Time + Cooldown) / WEEK) * WEEK - Current Time)
```
{% endcode %}

`MAXTIME` is a constant variable for maintaining the integrity of balance calculations.



**Withdrawal and Rewards Accrual**

An extra transaction is needed for fund withdrawal post-cooldown. Rewards accrue for users who have triggered cooldown but haven't withdrawn funds. Rewards stop when the cooldown time and aCC balance reach zero.



**Token Distribution**

The contract uses a fee distributor to allocate tokens to aCC holders proportionally to their holdings. The contract does not intrinsically produce any yield.
