# XCM Message

Xcm Message is just ordered-set of instructions.

```rust
pub struct Xcm<Call>(pub Vec<Instruction<Call>>);
```

[List of instructions](xcm-instructions.md)


Example:

```
WithdrawAsset((Parent, 10_000_000_000).into()),
InitiateReserveWithdraw {
    assets: All.into(),
    dest: ParentThen(Parachain(1000)).into(),
    xcm: Xcm(vec![
        BuyExecution {
            fees: (Parent, 10_000_000_000).into(),
            weight: 3_000_000,
        },
        DepositReserveAsset {
            assets: All.into(),
            max_assets: 1,
            dest: ParentThen(Parachain(2001)).into(),
            xcm: Xcm(vec![
                BuyExecution {
                    fees: (Parent, 10_000_000_000).into(),
                    weight: 3_000_000,
                },
                DepositAsset {
                    assets: All.into(),
                    max_assets: 1,
                    beneficiary: ParentThen(Parachain(2000)).into(),
                },
            ]),
        },
    ]),
},

```