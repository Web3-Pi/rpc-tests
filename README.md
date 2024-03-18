# The fork of rpc-test

This is the fork of erigon's rpc-tests repo. 
The original README is below.
For now, only `integration` tests are in use, and only `mainnet`.
The suits `eth_call`, `eth_getBalance` and `eth_getCode` were using requests to an archive node -
they were copied to `arch_etharch_call`, `arch_etharch_getBalance` and `arch_etharch_getCode`
and original tests were adjusted to use recent blocks.
The suit `eth_callMany` seems to be ergon specific and was moved to `arch_etherigon_callMany`.
To install follow the original instructions.
To run execute

```shell
cd integration
python3 run_tests.py -b mainnet -a eth_call -r -c -H 93.174.26.241 -p 8545 -T http -v 1
```

Current status:
1. eth_getTransactionByHash - failed, returns 'null', even for recent blocks
2. eth_getTransactionReceipt - failed, returns 'null', even for recent blocks
3. eth_getBlockByNumber - OK, but adds 'yParity' which has the same value as 'v' for tx with 'accessList', updated in tests
4. eth_getBlockByHash - Ok, but the same as eth_getBlockByNumber
5. eth_createAccessList - failed, what is that?
6. eth_call - OK, but the message in the test 2 may be changed 
7. eth_protocolVersion - failed, geth does not support it yet, but should
8. eth_getProof - OK, but the response for the test 1 may be changed
9. arch_etharch_getProof - failed, for the current block: 'header not found'

# rpc-tests
Collection of JSON RPC black-box testing tools

## Table of Contents
1. ### [Installation](#installation)
    1. [Prerequisites](#prerequisites)
    2. [Obtaining rpc-tests](#obtaining-rpc-tests)
2. ### [Integration Testing](#integration-testing)
3. ### [Performance Testing](#performance-testing)
4. ### [Contributing](#contributing)

## Installation

#### Prerequisites

Using `rpc-tests` requires installing:
* [`Vegeta`](https://github.com/tsenart/vegeta) >= 12.8.4
* [`Python`](https://python.org/) >= 3.10
* [`python3-jsonpatch`] >= 1.32 (see README on integration subfolder)
* [`json-diff`] using npm (see README on integration subfolder)

After installation, make sure `vegeta`, `json-diff` and `json-patch-jsondiff ` commands are available at your shell prompt.

After installation, make sure `python3` and `pip3` commands are available at your shell prompt by running `python3 -h` and `pip3 -h`.

#### Obtaining `rpc-tests`

To obtain `rpc-tests` source code for the first time:
```
git clone https://github.com/erigontech/rpc-tests.git
```

`rpc-tests` uses a few Python third-party libraries, so after you've updated to the latest code with
```
git pull
```
update the dependencies as well by running
```
pip3 install -r requirements.txt
```

## Integration Testing

Check out the dedicated guide in [Integration Tests](./integration/README.md).

## Performance Testing

Check out the dedicated guide in [Performance Tests](./perf/README.md).
