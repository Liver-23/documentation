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

# Consensus

Consensus on Cascadia is determined by CometBFT, a successor to Tendermint Core, which aims to improve the state machine replication process.



**Steps to follow**

* Replace `github.com/tendermint/tendermint` with `github.com/cometbft/cometbft`.
* Switch `github.com/tendermint/tm-db` to `github.com/cometbft/cometbft-db`.
* Ensure `github.com/tendermint/tendermint` isn't a dependency in the `go.mod`.
* Run `make proto-gen`.



**Features**

The params module operates in maintenance mode. Rather than a singular module for parameters, individual modules now manage their parameters, enhancing flexibility.

ABCI 1.0 brings methods like “prepareProposal” and “processProposal” for streamlined communication between the application and the consensus engine. An App-side mempool addition enables custom block creation.

To buffer the protocol you need to migrate from `gogo/proto` to `cosmos/gogoproto`
