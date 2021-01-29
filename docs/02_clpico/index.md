---
content_title: Clpico
---

## Introduction

`clpico` is a command line tool that interfaces with the REST API exposed by `nodpico`. Developers can also use `clpico` to deploy and test PICOIO smart contracts.

## Installation

`clpico` is distributed as part of the [PICOIO software suite](https://github.com/PICOIO/pico/blob/master/README.md). To install `clpico` just visit the [PICOIO Software Installation](../00_install/index.md) section.

## Using Clpico

To use `clpico`, you need the end point (IP address and port number) of a running `nodpico` instance. Also, the `nodpico` instance must be configured to load the `picoio::chain_api_plugin` when launched. This allows `nodpico` to respond to the RPC requests coming from `clpico`.

### Clpico Commands

For a list of all `clpico` commands, run:

```sh
clpico --help
```

```console
Command Line Interface to PICOIO Client
Usage: clpico [OPTIONS] SUBCOMMAND

Options:
  -h,--help                   Print this help message and exit
  -u,--url TEXT=http://127.0.0.1:8888/
                              the http/https URL where nodpico is running
  --wallet-url TEXT=unix:///Users/username/picoio-wallet/kpicod.sock
                              the http/https URL where kpicod is running
  -r,--header                 pass specific HTTP header; repeat this option to pass multiple headers
  -n,--no-verify              don't verify peer certificate when using HTTPS
  --no-auto-kpicod             don't automatically launch a kpicod if one is not currently running
  -v,--verbose                output verbose errors and action console output
  --print-request             print HTTP request to STDERR
  --print-response            print HTTP response to STDERR

Subcommands:
  version                     Retrieve version information
  create                      Create various items, on and off the blockchain
  convert                     Pack and unpack transactions
  get                         Retrieve various items and information from the blockchain
  set                         Set or update blockchain state
  transfer                    Transfer tokens from account to account
  net                         Interact with local p2p network connections
  wallet                      Interact with local wallet
  sign                        Sign a transaction
  push                        Push arbitrary transactions to the blockchain
  multisig                    Multisig contract commands
  wrap                        Wrap contract commands
  system                      Send picoio.system contract action to the blockchain.
```

### Clpico Subcommands

To get help with any particular subcommand, run `clpico SUBCOMMAND --help`. For instance:

```sh
clpico create --help
```

```console
Create various items, on and off the blockchain
Usage: clpico create SUBCOMMAND

Subcommands:
  key                         Create a new keypair and print the public and private keys
  account                     Create a new account on the blockchain
                              (assumes system contract does not restrict RAM usage)
```

`clpico` can also provide usage help for subcommands within subcommands. For instance:

```sh
clpico create account --help
```

```console
Create a new account on the blockchain (assumes system contract does not restrict RAM usage)
Usage: clpico create account [OPTIONS] creator name OwnerKey [ActiveKey]

Positionals:
  creator TEXT                The name of the account creating the new account (required)
  name TEXT                   The name of the new account (required)
  OwnerKey TEXT               The owner public key or permission level for the new account (required)
  ActiveKey TEXT              The active public key or permission level for the new account

Options:
  -h,--help                   Print this help message and exit
  -x,--expiration             set the time in seconds before a transaction expires, defaults to 30s
  -f,--force-unique           force the transaction to be unique. this will consume extra bandwidth and remove any protections against accidently issuing the same transaction multiple times
  -s,--skip-sign              Specify if unlocked wallet keys should be used to sign transaction
  -j,--json                   print result as json
  --json-file TEXT            save result in json format into a file
  -d,--dont-broadcast         don't broadcast transaction to the network (just print to stdout)
  --return-packed             used in conjunction with --dont-broadcast to get the packed transaction
  -r,--ref-block TEXT         set the reference block num or block id used for TAPOS (Transaction as Proof-of-Stake)
  --use-old-rpc               use old RPC push_transaction, rather than new RPC send_transaction
  -p,--permission TEXT ...    An account and permission level to authorize, as in 'account@permission' (defaults to 'creator@active')
  --max-cpu-usage-ms UINT     set an upper limit on the milliseconds of cpu usage budget, for the execution of the transaction (defaults to 0 which means no limit)
  --max-net-usage UINT        set an upper limit on the net usage budget, in bytes, for the transaction (defaults to 0 which means no limit)
  --delay-sec UINT            set the delay_sec seconds, defaults to 0s
```

## Clpico Example

The following `clpico` command creates a local wallet named `mywallet` and displays the password to the screen:

```sh
clpico wallet create -n mywallet --to-console
```

```console
Creating wallet: mywallet
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5JbF34UdA193Eps1bjrWVJRaNMt1VKddLn4Dx6SPVTfMDRnMBWN"
```
