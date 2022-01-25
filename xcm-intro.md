
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
Currently the latest version is V2.

Compatilibty.

## MultiLocation
Each chain can represent its assets differently. 

For example, on Basilisk our asset type is u32. Karura has currency type defined as an enum.

Therefore, to be able to send asssets between chains, some mapping have to be implemented. Each asset's uniquely identified in the polkadot ecosystem.

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

In case of Karura - it is possiuble to send KAR,KUSD, ??? - therefore it must be more specific which asssets is being transferred.


## asset <-> location conversions
If a chain wants to accept another chain's asset, it needs to configure the xcm system to accept the asset and define the conversion to internal asset representation.

Let's say Basilisk wants to accept KUSD from Karura. 

It needs to register the asset in Basilisk's asset registry and define its location. Baislisk implments dynamic asset registry, so it is possible add ( or remove) accepted assets without needing of any code changes and upgrades. 

Not all chains implements this - in such case, upgrade would likely be necessary. 

Basislisk registers KUSD in its asset registry - and internal asset id is assigned to the newly registred token. Asset Location is set and from that moment, any transfer from Karura with that location would be accepted and transfer executed.

## what happens if location is not set ?
