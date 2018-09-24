## Install

```
git clone https://github.com/vy-nguyen/bcpoc.git
```

Delete git setup

```
cd bcpoc
rm -rf .git
```

Edit config file

```
nano config/node-0.toml

Change HTTP port if needed, the default port is 8000
HTTPPort = 8000

Change bootstrap node to have correct IP, port
enode://dc9a088eaaf21d53c4...8e99175371b4b01@127.0.0.1:30000"
                                             ^^^^^^^ ip, port
                                             
Change port binding for the bootstrap node
ListenAddr = "localhost:30000"
                        ^^^ must match with the port above.
```
Save and exit.
Change config file for other nodes.  Other node configs can run in the same node with different port or different node at the same port.  If running in the same node, must change HTTPort binding to avoid conflict.
```
nano config/node-1.toml
```

## Running
```
In bcpoc directory
./bc --config config/node-0.toml
./bc --config config/node-1.toml
...
```

## Curl
Put key="key-xyz", value="value-abc" to the database for branch name "XYZ" from <node-0-ip>, http port 8000.
  
```
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method": "kv_putKey", "params": [ "XYZ", "key-xyz", "value-abc" ], "id": "foo" }' <node-0-ip>:8000
```

Get key="key-xyz" from the other node.
```
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method": "kv_getKey", "params": [ "XYZ", "key-xyz" ], "id": "foo" }' <node-1-ip>:8000
```
