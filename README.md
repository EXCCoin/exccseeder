# exccseeder

[![Build Status](https://github.com/EXCCoin/exccseeder/workflows/Build%20and%20Test/badge.svg)](https://github.com/EXCCoin/exccseeder/actions)
[![ISC License](https://img.shields.io/badge/license-ISC-blue.svg)](http://copyfree.org)

## Overview

exccseeder is a crawler for the ExchangeCoin network, which exposes a list of reliable
nodes via a built-in HTTP server.

When exccseeder is started for the first time, it will connect to the dcrd node
specified with the `-s` flag, send a `getaddrs` request, expecting an  `addr`
message response. This message contains hostnames and IPs of peers known by the
node. exccseeder will then connect to each of these peers, send a `getaddrs`
request, and will continue traversing the network in this fashion. exccseeder
maintains a list of all known peers and periodically checks that they are
online and available. The list is stored on disk in a json file, so on
subsequent start ups the dcrd node specified with `-s` does not need to be
online.

When exccseeder is queried for node information, it responds with details of a
random selection of the reliable nodes it knows about.

## Requirements

[Go](https://golang.org) 1.19 or newer.

### Getting Started

To build and install from a checked-out repo, run `go install` in the repo's
root directory.

To start exccseeder listening on localhost:8000 with an initial connection to working testnet node 192.168.0.1:

```no-highlight
$ ./exccseeder -s 192.168.0.1 --testnet --httplisten=localhost:8000
```

You will then need to redirect HTTPS traffic on your public IP to localhost:8000

## Issue Tracker

The [integrated github issue tracker](https://github.com/decred/exccseeder/issues)
is used for this project.

## License

exccseeder is licensed under the [copyfree](http://copyfree.org) ISC License.
