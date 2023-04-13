# file_actor_example

An actor example for creating and deploying on filecoin Network.

Step by steps to run the node and deploy the actor and onvoking. In this node running inside the docker container.

## Steps

Run The Node

    `docker run -p 1234:1234 -i -t --rm --name lotus-fvm-localnet ghcr.io/jimpick/lotus-fvm-localnet-lite:latest lotus daemon --lotus-make-genesis=devgen.car --genesis-template=localnet.json --bootstrap=false`


Run the Minor 
```docker exec -i -t lotus-fvm-localnet lotus-miner run --nosync```

build The Wasm

1. Clone this Repository
2. Build the it
    
    `Cargo build --release`
    
3. The wasm will be in 

    `./target/release/wbuild/filecoin_hello_world_actor/smart_contract.compact.wasm`
    
    
 ## Deploy to the Filecoin
1. Connect to the local net
    - Before that you need to expose the ip in docker container
        - Open the config.toml file present inside the ./lotus folder in container
        - Uncomment the ListenAddress to 0.0.0.0 eg: ListenAddress = "/ip4/0.0.0.0/tcp/1234/http"
        - Restart the Node
2. Install the Actor code
    
    `lotus chain install-actor <wasm-file>`
    
    You will get a code-CID, Note this code-cid
    
3. Create Actor Instance
    
    `lotus chain create-actor <code-cid>`
    
    In this you will get ID Address, note this actor address id for invoking.
    
4. Invoke the Actor
    
    `lotus chain invoke <actor-id-address> <method-number>`
    
    Eg : lotus chain invoke t1001 2
