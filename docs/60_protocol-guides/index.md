---
content_title: Protocol Guides
link_text: Protocol Guides
---

The Antelope Protocol section describes how the `Antelope framework` actually works and can be split into two layers. The core which is open source and implemented in `C++` and system which is implemented in smart contracts running on the core.  

## Core

The `Antelope Core` provides the basic building blocks for the `system` layer and are not implemented as smart contracts. The `core` implementation is open source and the source code can be customised to suit specific business requirements.

The core protocols are:

1. [Consensus Protocol](10_consensus_protocol.md)
2. [Transactions Protocol](20_transactions_protocol.md)
3. [Network or Peer to Peer Protocol](30_network_peer_protocol.md)
4. [Accounts and Permissions](40_accounts_and_permissions.md)

## System

The Antelope blockchain framework is unique in that the features and characteristics of the blockchain built on it are flexible, that is, they can be changed, or be modified completely to suit each business case requirement. Core blockchain features such as consensus, fee schedules, account creation and modification, token economics, block producer registration, voting, multi-sig, etc., are implemented inside smart contracts which are deployed on the blockchain built on the Antelope framework. These smart contracts are referred to as `system contracts` and the layer as the `Antelope system` layer, or simply `system` layer.

EOS Network Foundationimplements and maintains these `system contracts`, as samples only, encapsulating the base functionality for an Antelope based blockchain and they are listed below:

1. [eosio.bios](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/action-reference/eosio.bios)
2. [eosio.system](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/action-reference/eosio.system)
3. [eosio.msig](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/action-reference/eosio.msig)
4. [eosio.token](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/action-reference/eosio.token)
5. [eosio.wrap](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/action-reference/eosio.wrap)

Also part of the `system` layer are the following concepts:

1. [System accounts](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/index/#system-contracts-system-accounts-priviledged-accounts)
2. [RAM](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/index/#ram)
3. [CPU](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/index/#cpu)
4. [NET](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/index/#net)
5. [Stake](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/index/#stake)
6. [Vote](https://docs.eosnetwork.com/manuals/eos-system-contracts/latest/index/#vote)