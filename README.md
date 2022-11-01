# Gable Appchain

The Barnacle EVM-based Gable AppChain is a Substrate-based EVM compatible network based on [Parity's Frontier pallet](https://github.com/paritytech/frontier).

You can run any Solidity smart contract in Gable AppChain, and use any Ethereum development environments including Hardhat, Truffle, Remix, and many more.

## Running the Gable AppChain

Gable AppChain is a ready-to-use Appchain. To run the Appchain, you can firstly build it:

```
cargo build --release
```

Then run it:

```
./target/release/gable-barnacle --dev --enable-offchain-indexing true
```

Also, you can read these docs for more details:

+ about [`--dev`](https://docs.substrate.io/tutorials/get-started/build-local-blockchain/)
+ about [chain spec](https://docs.substrate.io/build/chain-spec/)

### Running Gable AppChain Testnet

If any one wishes to become a fullnode for Gable AppChain Testnet, you are invited to run with our genesis specification in ./resources/gable-testnet.json with the following command:

```
./target/release/gable-barnacle \
  --base-path ./data/node \
  --chain resources/gable-testnet.json \
  --port 30333 \
  --ws-port 9955 \
  --rpc-port 9953 \
  --validator \
  --rpc-methods Unsafe \
  --unsafe-ws-external \
  --unsafe-rpc-external \
  --rpc-cors all \
  --name your-node-name \
  --bootnodes /ip4/65.108.203.30/tcp/30333/p2p/12D3KooWGZuWhbKpueb1tt4Z8CGSQ7XcTajyUxzzKQiwNYpqzySk
```

### Running Gable AppChain Mainnet
The genesis specification for Gable AppChain Mainnet will be updated as soon as Mainnet launches.

## Connecting to the Gable AppChain Testnet
As Gable AppChain is an EVM-compatible platform, any EVM-compatible wallet such as Metamask can be used to interact with Gable with the followings:
* RPC: https://rpc1.gablechain.com/, https://rpc2.gablechain.com/
* ChainId: 1281
* Explorer: https://scan.gablechain.com/
* Faucet: https://faucet.gablechain.com/
* Simple Marketplace: https://marketplace.gablechain.com/

## How Gable AppChain Works

Gable AppChain is an EVM-compatible blockchain and doesn't have any custom Substrate pallets. The key to this template is in the `node/Cargo.toml`, where you have the `pallet-evm` and `pallet-ethereum` dependencies.

You can modify the snippet below within the `node/src/chain_spec.rs` file to add your pre-funded accounts.

```rust
// Pre-funded accounts
Some(
  vec![AccountId::from_str("f24FF3a9CF04c71Dbc94D0b566f7A27B94566cac").unwrap()],
)
```
Also, you can modify the sudo account as you need.

```rust
// Sudo account
AccountId::from_str("f24FF3a9CF04c71Dbc94D0b566f7A27B94566cac").unwrap(),
```

Note that there are two identical configurations in the file, but the difference is the running environment. Modify the configurations in `development_config()` if you run as development environment. Modify the configurations in `local_testnet_config()` if you run as local testnet environment.

Substrate will run an EVM smart contract platform, making it inherently interoperable with the Ethereum network. You can run any EVM-based smart contract within the EVM platform, like running it on an Ethereum Testnet or Mainnet.

The Octopus Network team provides you with the basic documentation for the [Barnacle EVM](https://docs.oct.network/guides/appchain-evm.html#evm-compatible-appchain). You can visit our [examples to learn more](docs/example/README.md#barnacle-hardhat-project-template).

## Parity Frontier [Releases](https://github.com/paritytech/frontier#releases)

### Primitives

Those are suitable to be included in a runtime. Primitives are structures shared
by higher-level code.

* `fp-consensus`: Consensus layer primitives.
  ![Crates.io](https://img.shields.io/crates/v/fp-consensus)
* `fp-evm`: EVM primitives. ![Crates.io](https://img.shields.io/crates/v/fp-evm)
* `fp-rpc`: RPC primitives. ![Crates.io](https://img.shields.io/crates/v/fp-rpc)
* `fp-storage`: Well-known storage information.
  ![Crates.io](https://img.shields.io/crates/v/fp-storage)

### Pallets

Those pallets serve as runtime components for projects using Frontier.

* `pallet-evm`: EVM execution handling.
  ![Crates.io](https://img.shields.io/crates/v/pallet-evm)
* `pallet-ethereum`: Ethereum block handling.
  ![Crates.io](https://img.shields.io/crates/v/pallet-ethereum)
* `pallet-dynamic-fee`: Extends the fee handling logic to be changed
  within the runtime.
  ![Crates.io](https://img.shields.io/crates/v/pallet-dynamic-fee)

### EVM Pallet precompiles

Those precompiles can be used together with `pallet-evm` for additional
functionalities of the EVM executor.

* `pallet-evm-precompile-simple`: Four basic precompiles in Ethereum EVMs.
  ![Crates.io](https://img.shields.io/crates/v/pallet-evm-precompile-simple)
* `pallet-evm-precompile-blake2`: BLAKE2 precompile.
  ![Crates.io](https://img.shields.io/crates/v/pallet-evm-precompile-blake2)
* `pallet-evm-precompile-bn128`: BN128 precompile.
  ![Crates.io](https://img.shields.io/crates/v/pallet-evm-precompile-bn128)
* `pallet-evm-precompile-ed25519`: ED25519 precompile.
  ![Crates.io](https://img.shields.io/crates/v/pallet-evm-precompile-ed25519)
* `pallet-evm-precompile-modexp`: MODEXP precompile.
  ![Crates.io](https://img.shields.io/crates/v/pallet-evm-precompile-modexp)
* `pallet-evm-precompile-sha3fips`: Standard SHA3 precompile.
  ![Crates.io](https://img.shields.io/crates/v/pallet-evm-precompile-sha3fips)
* `pallet-evm-precompile-dispatch`: Enable interoperability between EVM
  contracts and other Substrate runtime components.
  ![Crates.io](https://img.shields.io/crates/v/pallet-evm-precompile-dispatch)

### Client-side libraries

Those are libraries that you should use on the client-side to enable RPC, block hash
mapping, and other features.

* `fc-consensus`: Consensus block import.
  ![Crates.io](https://img.shields.io/crates/v/fc-consensus)
* `fc-db`: Frontier-specific database backend.
  ![Crates.io](https://img.shields.io/crates/v/fc-db)
* `fc-mapping-sync`: Block hash mapping syncing logic.
  ![Crates.io](https://img.shields.io/crates/v/fc-mapping-sync)
* `fc-rpc-core`: Core RPC logic.
  ![Crates.io](https://img.shields.io/crates/v/fc-rpc-core)
* `fc-rpc`: RPC implementation.
  ![Crates.io](https://img.shields.io/crates/v/fc-rpc)

## References

We forked this repository from [Barnable](https://github.com/octopus-network/barnacle), which originally forked from the
[Substrate Node Template](https://github.com/substrate-developer-hub/substrate-node-template). You
can find more information on features on this template there, and more detailed usage on the
[Substrate Developer Hub Tutorials](https://docs.substrate.io/tutorials/v3/) that use this heavily.
