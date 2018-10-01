# p2p broadcast app with libp2p

This program demonstrates a simple p2p broadcast application. It can work between several peers if
1. Both have private IP address (same network).
2. At least one of them has a public IP address.

Assume if 'A' and 'B' are on different networks host 'A' may or may not have a public IP address but host 'B' has one.

Usage: Run `./broadcast -sp <SOURCE_PORT>` on host 'B' where <SOURCE_PORT> can be any port number. Now run `./broadcast -d <MULTIADDR_B>` on node 'A' [`<MULTIADDR_B>` is multiaddress of host 'B' which can be obtained from host 'B' console].

## Build

To build the example, first run `make deps` in the root directory.

```
> make deps
> go build broadcast.go
```

## Usage

On node 'B'

```
$ go run broadcast.go -sp 3000
Run './broadcast -d /ip4/127.0.0.1/tcp/3000/ipfs/QmVSKT7PVGjpXKodMmbdyxit2Bv2RneH8EA5M4zJCftHyx' on another console.
 You can replace 127.0.0.1 with public IP as well.

Waiting for incoming connection

> 2018/09/30 20:55:30 Got a new stream!
> test test (received messages in dark green color)
> hi hi hi (sending messages in light green color)
```

On node 'A'. Replace 127.0.0.1 with <PUBLIC_IP> if node 'B' has one.

```
$ go run broadcast.go -d /ip4/127.0.0.1/tcp/3000/ipfs/QmVSKT7PVGjpXKodMmbdyxit2Bv2RneH8EA5M4zJCftHyx
Run './broadcast -d /ip4/127.0.0.1/tcp/0/ipfs/QmSmiLDiPpVVaduZiWnADC6LBSEEgG2RR5ZjnLCCKoDARa' on another console.
 You can replace 127.0.0.1 with public IP as well.

> test test
> hi hi hi
```

**NOTE: debug mode is enabled by default, debug mode will always generate same node id (on each node) on every execution. Disable debug using `--debug false` flag while running your executable.**

## Authors

Wei Chen

## Reference

https://github.com/libp2p/go-libp2p-examples/tree/master/chat
