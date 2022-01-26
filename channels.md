# HRMP channels

> Horizontal Relay-routed Message Passing

Channels are needed for parachains to communicate between each other. 

For example if Basilisk wants to send a message to Karura, a channel between them has to be opened. 

Hrmp channel is uni-directional, that means if Karura wanted to send a message back to Basilisk, another channel would have to be created for this purpose.

In this section, we demonstrate how to manually open channels between Karura and Basilisk.

## HRMP Config

To check HRMP configuration -> Relay -> Chain state -> configuration -> activeConfig.

There are few parameters releated to hrmp which you need to know when opnmeing a channel = max capacity, max size and deposit.

Deposit is needed for opening a channel as well as accepting an open channel request.

Basilisk Testnet:

```rust
  hrmpMaxParachainOutboundChannels: 10
  hrmpMaxParathreadOutboundChannels: 0
  hrmpSenderDeposit: 67,274,662,584,000
  hrmpRecipientDeposit: 67,274,662,584,000
  hrmpChannelMaxCapacity: 1,000
  hrmpChannelMaxTotalSize: 102,400
  hrmpMaxParachainInboundChannels: 10
  hrmpMaxParathreadInboundChannels: 0
  hrmpChannelMaxMessageSize: 102,400

```

## Opening a channel

Xcm Transact message to Relay chain.

0x1000010100020c000400000000070010a5d4e81300000000070010a5d4e800060002286bee381700d007000008000000401f0000

To check if request has been accepted succesfully. 

Relay -> Chain State -> hrmp -> hrmpOpenChannelRequests

```rust
hrmp.hrmpOpenChannelRequests: Option<PolkadotRuntimeParachainsHrmpHrmpOpenChannelRequest>

[
  [
    [
      {
        sender: 2,090
        recipient: 2,000
      }
    ]
    {
      confirmed: false
      age: 0
      senderDeposit: 0
      maxMessageSize: 8,000
      maxCapacity: 8
      maxTotalSize: 8,192
    }
  ]
]
```

## Accepting a request