# Capability

|||
|-|-|
| **Name** | Capability |
| **Origin** | [Libra Project](https://github.com/move-language/move/blob/5e034dde19a5320d7e2bdc9da25114e816b4454d/language/stdlib/modules/libra_coin.mvir#L8) / Unknown Author |
| **Example** | [Sui Move by Example](https://examples.sui.io/patterns/capability.html) / [Damir Shamanaev](https://github.com/damirka) |
| **Depends on** | None |
| **Known to work on** | Move |

## Summary

A **Capability** is a resource proving that the owner of the resource is permitted to execute a certain action. This is the oldest known Move design pattern dating back to the Libra project and its token smart contract, where capabilities were used to authorize minting of coins.

## Examples

```move
module examples::item {
    use sui::transfer;
    use sui::id::VersionedID;
    use sui::utf8::{Self, String};
    use sui::tx_context::{Self, TxContext};

    /// Type that marks Capability to create new `Item`s.
    struct AdminCap has key { id: VersionedID }

    /// Custom NFT-like type.
    struct Item has key, store { id: VersionedID, name: String }

    /// Module initializer is called once on module publish.
    /// Here we create only one instance of `AdminCap` and send it to the publisher.
    fun item(ctx: &mut TxContext) {
        transfer::transfer(AdminCap {
            id: tx_context::new_id(ctx)
        }, tx_context::sender(ctx))
    }

    /// The entry function can not be called if `AdminCap` is not passed as
    /// the first argument. Hence only owner of the `AdminCap` can perform
    /// this action.
    public entry fun create_and_send(
        _: &AdminCap, name: vector<u8>, to: address, ctx: &mut TxContext
    ) {
        transfer::transfer(Item {
            id: tx_context::new_id(ctx),
            name: utf8::string_unsafe(name)
        }, to)
    }
}
```

*Example for Sui Move is taken from the book [Sui Move by Example](https://examples.sui.io/patterns/capability.html) by [Damir Shamanaev](https://github.com/damirka).*