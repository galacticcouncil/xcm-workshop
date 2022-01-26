
# XCM Introduction

> XCM - cross chain message
> XCMP - cross chain message protocol

XCM setup:

- xcm-executor
- XcmConfig
- queues 
    - ump
    - dmp
    - hrmp


## XCM versions
Current XCM version is V2.

Compatibility.

## Sovereign parachain accounts

It is an account controllable by sender or receiver chain on given chain.

- Basilisk: 5Ec4AhNugFBakYoh6kD3mgCkUDhy4vVm5o78KDtG42yrXKwS

- Karura: 5Ec4AhPUwPeyTFyuhGuBbD224mY85LKLMSqSSo33JYWCazU4

- Statemint: 5Ec4AhPZk8STuex8Wsi9TwDtJQxKqzPJRCH7348Xtcs9vZLJ

Accounts on statemint are derived from parachain id:
- Basilisk: 5Eg2fnsikyNUt9XqekA8tKYZihPGnLYs9SkZaBQkvm1RNvdh
 
- Karura: 5Eg2fntJ27qsari4FGrGhrMqKFDRnkNSR6UshkZYBGXmSuC8

## MultiLocation

Multilocation type identifies any single location that can exist.

It can represent many things( parachain, account, asset etc ). Let's focus on asset location for now.

>  MultiLocation always represents location relative to the current location.

Eg. 
../Parachain(2000) - if evaluates on parachains, it identifies sibling parachain with ID 2000.
Parachain(2000)/AccountId32(0x1234..) - if evaluated on relay chains, it identifies account id on parachain 2000.

## MultiAsset

Assets in XCM are represented by MultiAsset datatype:

```rust
struct MultiAsset {
   id: AssetId,
   fun: Fungibility,
}
```

```rust
enum AssetId {
   Concrete(MultiLocation),
   Abstract(BinaryBlob),
}
```

```rust
enum Fungibility {
   Fungible(NonZeroAmount),
   NonFungible(AssetInstance),
}
```

## Assets and locations
Each chain can represent its assets differently. 

For example, on Basilisk our asset type is u32. Karura has currency type defined as an enum.

Therefore, to be able to send assets between chains, some mapping have to be implemented. Each asset's location uniquely identified in the polkadot ecosystem.

Examples: 
Karura's KUSD location
```
MultiLocation((1, X2(Parachain(2000), GeneralKey(0x0081))))
```

Basilisk BSX location
```
MultiLocation((1, X1(Parachain(2090))))
```

Why in case of Basilisk's BSX location, there is no need for GeneralKey ?

Basilisk currently has only one token which it can transfer to other chain, there is no need to specify anything else besides the parachain location. 

In case of Karura - it is possible to send KAR,KUSD, ??? - therefore it must be more specific which assets is being transferred.


## asset <-> location conversions
If a chain wants to accept another chain's asset, it needs to configure the xcm system to accept the asset and define the conversion to internal asset representation.

Let's say Basilisk wants to accept KUSD from Karura. 

It needs to register the asset in Basilisk's asset registry and define its location. Basilisk implements dynamic asset registry, so it is possible add ( or remove) accepted assets without needing of any code changes and upgrades. 

Not all chains implements this - in such case, upgrade would likely be necessary. 

Basilisk registers KUSD in its asset registry - and internal asset id is assigned to the newly registered token. Asset Location is set and from that moment, any transfer from Karura with that location would be accepted and transfer executed.

### What happens if location is not set ?
