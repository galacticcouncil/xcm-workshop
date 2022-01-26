# Holding register
It is a temporary position which cannot persist, and it is place where withdrawn and unspent are held during xcm execution.

For example, WithdrawAsset instruction has only information which asset to withdraw, but it does not know yet what to do with that.

```rust
    WithdrawAsset(MultiAssets),
```

For that, you need corresponding deposit instruction, but again it does not know where to take it from, so it takes is fromthe holding register.

```rust
   DepositAsset {
    assets: MultiAssetFilter,
    max_assets: u32,
    beneficiary: MultiLocation,
  }
```

If there is anything left in the register after xcm execution, it is trapped