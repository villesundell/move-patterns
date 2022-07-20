# Witness

|||
|-|-|
| **Name** | Witness |
| **Origin** | [FastX](https://github.com/MystenLabs/sui/blob/c1ed7cc451119432d32d8eacf471f314e0ce5275/fastx_programmability/sources/Coin.move#L85) / [Sam Blackshear](https://github.com/sblackshear) |
| **Example** | [Sui Move by Example](https://examples.sui.io/patterns/witness.html) / [Damir Shamanaev](https://github.com/damirka) |
| **Depends on** | None |
| **Known to work on** | Move |

## Summary

A **Witness** is an ephemeral resource designed to prove only once that the a resource in question can be initiated only once after the witness has been created. The resource is dropped after use, ensuring that the same resource cannot be reused to initialize any other struct.

## Examples

```move
/// Module that defines a generic type `Guardian<T>` which can only be
/// instantiated with a witness.
module examples::guardian {
    use sui::id::VersionedID;
    use sui::tx_context::{Self, TxContext};

    /// Phantom parameter T can only be initialized in the `create_guardian`
    /// function. But the types passed here must have `drop`.
    struct Guardian<phantom T: drop> has key, store {
        id: VersionedID
    }

    /// The first argument of this function is an actual instance of the
    /// type T with `drop` ability. It is dropped as soon as received.
    public fun create_guardian<T: drop>(
        _witness: T, ctx: &mut TxContext
    ): Guardian<T> {
        Guardian { id: tx_context::new_id(ctx) }
    }
}

/// Custom module that makes use of the `guardian`.
module examples::peace {
    use sui::transfer;
    use sui::tx_context::{Self, TxContext};

    // Use the `guardian` as a dependency.
    use 0x0::guardian;

    /// This type is intended to be used only once.
    struct PEACE has drop {}

    /// Module initializer is the best way to ensure that the
    /// code is called only once. With `Witness` pattern it is
    /// often the best practice.
    fun init(ctx: &mut TxContext) {
        transfer::transfer(
            guardian::create_guardian(PEACE {}, ctx),
            tx_context::sender(ctx)
        )
    }
}
```

*Example for Sui Move is taken from the book [Sui Move by Example](https://examples.sui.io/patterns/witness.html) by [Damir Shamanaev](https://github.com/damirka).*
