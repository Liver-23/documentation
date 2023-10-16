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

# Proposals

Proposals are initiated to propose a potential modification to Cascadia via a Cascadia Improvement Proposal (CIP).  Discussions are started as a \[Temperature Check], then moved to \[CIP] and vote, after community feedback and discussion.  The progression from \[Temperature Check] to \[CIP] is a collaborative process.  CIPs are intended to provide a consistent pathway for proposing changes to Cascadia, ensuring that all stakeholders have an opportunity to be heard.



Each CIP must contain:

1. **Title:** This is the title, labelled either \[Temperature Check] or \[CIP].
2. **Author:** Who is proposing the idea?
3. **Summary:** This is a one-sentence summary of the proposal.&#x20;
4. **Background/Motivation:** This is the main body of the proposal.
5. **Specification:** This is what will be implemented should the proposal be approved.
6. **Key Performance Indicators (KPIs):** How is performance measured?
7. **Reversion**: For how long will this proposal be active before it is automatically reverted based on the stated KPIs?
8. **Voting:** This outlines the voting options.



**Sample:**

> **Title**
>
> \[CIP-XXX] Update Voting Period
>
>
>
> **Authors**
>
> Richard
>
>
>
> **Summary**
>
> This CIP seeks to update the voting period to 3 days.
>
> \
> **Background**
>
> This TCIP seeks to update the voting period from X days to 3 days to create a more streamlined governance process
>
>
>
> **Specification**
>
> If approved, the votiing\_period paramater in the governance module shall be changed from XXX to 259200000000000.
>
>
>
> **KPI**
>
> N/A
>
>
>
> **Reversion**
>
> N/A
>
>
>
> **Voting**
>
> This vote will be live for three days. We appreciate and encourage an open discussion on this subject. This vote will be a single-choice vote. You may vote “For” or “Against” this proposal or abstain from the vote. By voting “For” this proposal, you are voting in favour of implementing the changes in accordance with the specifications set out in this proposal.



### **Voting via CLI**

For users familiar with CLI, CascadiaFarms offers an on-chain voting mechanism. Follow the instructions below to cast your vote.



**Step 1: Open your Command Line Interface (CLI)**.



**Step 2: Input the following command to cast your vote.**

{% code overflow="wrap" %}
```javascript
cascadiad tx gov vote <proposal_number> <your_vote_choice> --gas-prices 7aCC --from <your_key_name> --node https://rpc.cascadia.foundation:443
```
{% endcode %}

* Replace `<proposal_number>` with the actual number of the proposal you wish to vote on (e.g., 23).
* Replace `<your_vote_choice>` with your desired vote choice (e.g., yes, no, abstain).
* Replace `<your_key_name>` with the name of your key.



For users who wish to automatically adjust their gas prices, you can add the following at the end of the command:

{% code overflow="wrap" %}
```javascript
--gas auto --gas-adjustment 2
```
{% endcode %}

This allows the system to determine the best gas price for your transaction and adjust it by a factor of 2.

#### **Notes**:

* Always ensure you're voting on the correct proposal number and double-check your choices before confirming.
* Make sure your CLI environment is set up correctly and that you have sufficient funds to cover any transaction fees.
