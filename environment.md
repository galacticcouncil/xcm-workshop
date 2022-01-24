# Local Environment


Local environment includes:
- Relay chain ( rococo )
- Parachains
    - Basilisk (ID: 2090)
    - Karura (ID: 2000)
    - Westmint (ID: 1000)


## Basilisk and Karura

Let's setup these 2 chains using polkadot-launch tool. 

The config can be found [here]() TODO ( add link)

Polkadot-launch is [here]()

```bash
polkadot-launch basilisk-karura.json
```

Details:

Basilisk's port: 9988

Karura's port: 9999


## Westmint

Clone cumulus [repository]()

Build

Start collator:
```bash
./target/release/polkadot-collator
```

### Registering as parachain

