# tendermint-kvstore-external
An example of creating an externally connected Tendermint Core application acting as a distributed key-value store.

### Version
- [Go](https://golang.org/): 1.17
- [Tendermint](https://tendermint.com/): 0.34.13
- [Badger](https://dgraph.io/badger): 1.6.2

### Installation
Install Go.
```
brew install golang
```

Install Tendermint.
```
brew install tendermint
```

### Build
```
go build
```

### Configuration
Clean the generated files (optional).
```
rm -rf ./tmp/kvstore
```

Create a default configuration, nodeKey and private validator files.
```
TMHOME="./tmp/kvstore" tendermint init
```

### Get Started
Clean the generated socket file (optional).
```
rm kvstore.sock
```

Start the application.
```
./kvstore
```

Start Tendermint Core and point it to the application.
```
TMHOME="./tmp/kvstore" tendermint node --proxy_app=unix://kvstore.sock
```

### Testing
Send a transaction to insert a key-value pair.
```
curl -s 'localhost:26657/broadcast_tx_commit?tx="tendermint=rocks"'
```

Query the value with the key. The `key` and `value` in the response are base64-encoded.
```
curl -s 'localhost:26657/abci_query?data="tendermint"'
```

### Reference
https://docs.tendermint.com/v0.34/tutorials/go.html