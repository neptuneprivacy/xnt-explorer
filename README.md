# xnt-explorer

A web-based block explorer for the Neptune Privacy blockchain.  xnt-explorer provides a basic HTML view and a REST RPC API.

Some [design notes](./doc/design_notes.md) are available.

## Installing

### Compile from Source -- Linux Debian/Ubuntu

You may need to:

```
sudo apt install pkg-config libssl-dev
```

Then

```
git clone https://github.com/xnt-privacy/xnt-explorer.git
cd xnt-explorer
cargo install --locked --path .
```

### Windows, Mac

not tested or supported.   Please let us know if you get it work.  patches accepted.

## Running

1. install [xnt-core](https://github.com/xnt-privacy/xnt-core) and start it, or otherwise find a running xnt-core instance.
2. start xnt-explorer

```
nohup xnt-explorer --site-domain testdomain 2>&1 > /path/to/logs/xnt-explorer.log &
```

Notes:
* The block-explorer automatically uses the same network (mainnet, testnet, etc) as the xnt-core instance it is connected to, and the network is displayed in the web interface.
* If xnt-core RPC server is running on a non-standard port, you can provide it with the `--xnt-rpc-port` flag.
* xnt-explorer listens for http requests on port 3000 by default.  This can be changed with the `--listen-port` flag.
* Site name can be specified with the --site-name flag.
* Site domain *must* be specified with the `--site-domain` flag.


## Connecting via Browser

Just navigate to http://localhost:3000/

## Mocking

When connected to an out-of-date or unsynced xnt-core node, it might be a good idea to turn on mocking so that whenever a resource is unavailable, a random one is generated and returned. To do this, compile with the feature flag "mock" and make sure that the "MOCK" environment variable is set.

In one command: `MOCK=1 cargo run --features "mock" -- --site-domain testdomain`

## SSL/TLS, Nginx, etc.

If hosting for public use, it is suggested to use nginx or similar in reverse-proxy mode to connect to `http://localhost:3000`.  Nginx can then handle SSL/TLS certs and connections, as xnt-explorer has no built-in support for that.


## Logging

All logging is output to standard out.

The log level can be set through the environment variable `RUST_LOG`. Valid values are: `trace`, `debug`, `info`, `warn`, and `error`. The default value is `info`. E.g.: `RUST_LOG=trace cargo run`.
