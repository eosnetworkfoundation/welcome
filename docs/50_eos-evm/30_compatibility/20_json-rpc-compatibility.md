---
title: JSON RPC Compatibility
---

All the JSON-RPC calls are inherently supported thanks to the full functioning EOS EVM node which is built based on Silkworm node. However, some methods are blocked in the current phase for the following reasons:

* Some methods are deprecated or discontinued.
* Some methods are designed for the local node scenario. They are not exposed to the public API, however you can access them when you deploy your own EOS EVM node.
* Some methods involve complex logic, therefore more tests need to be performed before they will be exposed.

## RPC List

| RPC Method                               | Destination  |
| ---------------------------------------- | ------------ |
| web3\_clientVersion                      | EOS EVM node |
| web3\_sha3                               | Block        |
| net\_version                             | EOS EVM node |
| net\_peerCount                           | Block        |
| net\_listening                           | Block        |
| eth\_protocolVersion                     | Block        |
| eth\_syncing                             | Block        |
| eth\_coinbase                            | Block        |
| eth\_mining                              | Block        |
| eth\_hashrate                            | Block        |
| eth\_gasPrice                            | Wrapper      |
| eth\_accounts                            | Block        |
| eth\_blockNumber                         | EOS EVM node |
| eth\_getBalance                          | EOS EVM node |
| eth\_getStorageAt                        | EOS EVM node |
| eth\_getTransactionCount                 | EOS EVM node |
| eth\_getBlockTransactionCountByHash      | EOS EVM node |
| eth\_getBlockTransactionCountByNumber    | EOS EVM node |
| eth\_getUncleCountByBlockHash            | Block        |
| eth\_getUncleCountByBlockNumber          | Block        |
| eth\_getCode                             | EOS EVM node |
| eth\_sign                                | Block        |
| eth\_signTransaction                     | Block        |
| eth\_sendTransaction                     | Block        |
| eth\_sendRawTransaction                  | Wrapper      |
| eth\_call                                | EOS EVM node |
| eth\_estimateGas                         | Wrapper      |
| eth\_getBlockByHash                      | EOS EVM node |
| eth\_getBlockByNumber                    | EOS EVM node |
| eth\_getTransactionByHash                | EOS EVM node |
| eth\_getTransactionByBlockHashAndIndex   | EOS EVM node |
| eth\_getTransactionByBlockNumberAndIndex | EOS EVM node |
| eth\_getTransactionReceipt               | EOS EVM node |
| eth\_getUncleByBlockHashAndIndex         | Block        |
| eth\_getUncleByBlockNumberAndIndex       | Block        |
| eth\_getCompilers                        | Block        |
| eth\_compileLLL                          | Block        |
| eth\_compileSolidity                     | Block        |
| eth\_compileSerpent                      | Block        |
| eth\_newFilter                           | Block        |
| eth\_newBlockFilter                      | Block        |
| eth\_newPendingTransactionFilter         | Block        |
| eth\_uninstallFilter                     | Block        |
| eth\_getFilterChanges                    | Block        |
| eth\_getFilterLogs                       | Block        |
| eth\_getLogs                             | Block        |
| eth\_getWork                             | Block        |
| eth\_submitWork                          | Block        |
| eth\_submitHashrate                      | Block        |
| db\_putString                            | Block        |
| db\_getString                            | Block        |
| db\_putHex                               | Block        |
| db\_getHex                               | Block        |
| shh\_post                                | Block        |
| shh\_version                             | Block        |
| shh\_newIdentity                         | Block        |
| shh\_hasIdentity                         | Block        |
| shh\_newGroup                            | Block        |
| shh\_addToGroup                          | Block        |
| shh\_newFilter                           | Block        |
| shh\_uninstallFilter                     | Block        |
| shh\_getFilterChanges                    | Block        |
| shh\_getMessages                         | Block        |