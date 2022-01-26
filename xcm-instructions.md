# List of instructions

```rust
pub enum Instruction<Call> {
    WithdrawAsset(MultiAssets),
    ReserveAssetDeposited(MultiAssets),
    ReceiveTeleportedAsset(MultiAssets),
    QueryResponse { query_id: QueryId, response: Response, max_weight: u64 },
    TransferAsset { assets: MultiAssets, beneficiary: MultiLocation },
    TransferReserveAsset { assets: MultiAssets, dest: MultiLocation, xcm: Xcm<()> },
    Transact { origin_type: OriginKind, require_weight_at_most: u64, call: DoubleEncoded<Call> },
    HrmpNewChannelOpenRequest { sender: u32, max_message_size: u32, max_capacity: u32 },
    HrmpChannelAccepted { recipient: u32 },
    HrmpChannelClosing { initiator: u32, sender: u32, recipient: u32 },
    ClearOrigin,
    DescendOrigin(InteriorMultiLocation),
    ReportError { query_id: QueryId, dest: MultiLocation, max_response_weight: u64 },
    DepositAsset { assets: MultiAssetFilter, max_assets: u32, beneficiary: MultiLocation },
    DepositReserveAsset { assets: MultiAssetFilter, max_assets: u32, dest: MultiLocation, xcm: Xcm<()> },
    ExchangeAsset { give: MultiAssetFilter, receive: MultiAssets },
    InitiateReserveWithdraw { assets: MultiAssetFilter, reserve: MultiLocation, xcm: Xcm<()> },
    InitiateTeleport { assets: MultiAssetFilter, dest: MultiLocation, xcm: Xcm<()> },
    QueryHolding { query_id: QueryId, dest: MultiLocation, assets: MultiAssetFilter, max_response_weight: u64 },
    BuyExecution { fees: MultiAsset, weight_limit: WeightLimit },
    RefundSurplus,
    SetErrorHandler(Xcm<Call>),
    SetAppendix(Xcm<Call>),
    ClearError,
    ClaimAsset { assets: MultiAssets, ticket: MultiLocation },
    Trap(u64),
    SubscribeVersion { query_id: QueryId, max_response_weight: u64 },
    UnsubscribeVersion,
}
```