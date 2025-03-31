Command for running the rollup (inside of `svm-rollup/crates/rollup`):

```bash
make run-mock
```

With changing the https config to:

```toml
[runner.http_config]
bind_port = 8999
```

Command for running the solana test validator:

```bash
solana-test-validator
```

Command for deploying core to nitrosvmlocalnet:

```bash
cargo run -- -k ~/.config/solana/id.json --url http://localhost:8999/rpc \
        core deploy --environment nitro-local \
        --environments-dir ../environments/ --chain nitrosvmlocalnet \
        --built-so-dir ../target/deploy/ --local-domain 13440
```

Command for deploying core to solanalocalnet:

```bash
cargo run -- -k ~/.config/solana/id.json --url http://localhost:8899 \
        core deploy --environment nitro-local \
        --environments-dir ../environments/ --chain solanalocalnet \
        --built-so-dir ../target/deploy/ --local-domain 13377
```

Command for deploying the warp route:

```bash
cargo run -- -k ~/.config/solana/id.json \
        warp-route deploy --environment nitro-local \
        --environments-dir ../environments/ \
        --built-so-dir ../target/deploy/ \
        --warp-route-name sol-nitrolocal-solanalocal \
        --token-config-file ../environments/nitro-local/warp-routes/sol-nitrolocal-solanalocal/token-config.json \
        --chain-config-file ../environments/nitro-local/chain-config.json \
        --ata-payer-funding-amount 10000000
```

Command for validator:

```bash
cargo run -p validator --release -- \
        --config-path ./config/nitro_localnet_config.json \
        --validator.key "0x9beda4987660d3c8d48d949ec33abc2bc00e158630c2fe87e7e172333132eb17" \
        --defaultSigner.key "0xb48bc90c3fb62d1e72ee5481ce5659e6c1261f7db8e4ba26c657dc8c9fe937e0" \
        --originChainName solanalocalnet \
        --checkpointSyncer.type localStorage \
        --checkpointSyncer.path "/tmp/hyperlane-validator-signatures-svm"
```

Command for relayer:

```bash
cargo run -p relayer --release -- \
        --config-path ./config/nitro_localnet_config.json \
        --relayChains nitrosvmlocalnet,solanalocalnet \
        --allowLocalCheckpointSyncers true \
        --defaultSigner.key "0xb48bc90c3fb62d1e72ee5481ce5659e6c1261f7db8e4ba26c657dc8c9fe937e0"
```

Command for ISM configuration:

```bash
cargo run -- -k ~/.config/solana/id.json --url http://localhost:8999/rpc \
        multisig-ism-message-id configure \
        --program-id 7hWAvb6Y8vMpniQpBWpx7jN5BSZXLU7DbqRHh2heCLZs \
        --chain-config-file ../environments/nitro-local/chain-config.json \
        --multisig-config-file ../environments/nitro-local/multisig-ism-message-id/nitrosvmlocalnet/hyperlane/multisig-config.json
```

Command for validator announce:

```bash
cargo run -- -k ~/.config/solana/id.json -u http://localhost:8899/ \
        validator-announce announce \
        --program-id EzXcRFiwtTKbN7kabQbz9UAAcm4GLWd8NdmyBeHZEAL8 \
        --validator 0x5C2B54188f7FEA7f3A3d452709c0b44e3ccd857F \
        --storage-location 'file:///tmp/hyperlane-validator-signatures-svm' \
        --signature 0x5e9a7ae15ac3657d8c9da45cf7b9690bf59d7454572428134a356a426653f95d28e558943cd04c13d79796c030e64d5a716f2ce388214a50c4ed012e5747c6fb1c
```

Command for token transfer:

```bash
cargo run -- -k ~/.config/solana/id.json -u http://localhost:8899 \
        token transfer-remote ~/.config/solana/id.json \
        100000 13440 2MCVmcuUcREwQKDS3HazuYctkkbZV3XRMspM5eLWRZUV \
        native --program-id 7fYBqSMrPi29LLjr98BhPTHwfqtKjYVk7h14C8enjB9m
```

Command for IGP configuration:

```bash
cargo run -- -k ~/.config/solana/id.json -u https://api.devnet.solana.com \
        igp configure \
        --program-id CpP9nXDsQsifneJgwZ3pX8iwFUFGk5Bu3Ph5gdyeN7zw \
        --gas-oracle-config-file ../environments/nitro-test/gas-oracle-configs.json \
        --chain-config-file ../environments/nitro-test/chain-config.json \
        --chain solanadevnet
```

Command for querying the Token collateral account of a warp route deployment:

```bash
cargo run -- -k ~/.config/solana/id.json -u https://api.devnet.solana.com \
        token query \
        --program-id FBxoyKyCe4rYkJQMVUFYqV1U7WdeC2WVV8m1RuDHZrrY native
```
