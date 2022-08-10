# Nestable Resources

|||
|-|-|
| **Name** | Nestable Resources |
| **Origin** | [Ville Sundell](https://github.com/villesundell) |
| **Example** | [TaoHe project](https://github.com/taoheorg/taohe) |
| **Depends on** | None |
| **Known to work on** | Move |

## Summary

**Nestable Resources** pattern provides a resource native approach to code reuse by building a nested structure of resources where each resource can be detached for use if the conditions are satisfied. For example, tokens can be placed into a time locked resource, which in turn can be placed into a resource which can be used only by a certain user, effectively creating a timelocked non-fungible token. For cleaner design and easier integration it is recommended that the nestable resources share a common interface for wrapping and unwrapping.

## Examples

```move
/// A nested resource (tao) for implementing a simple ownership model: owner can extract
/// the content.
module 0x1::Ownable {
    use Std::Signer;

    /// Simple ownership tao: the `owner` can extract `content`.
    struct Tao<Content> has key, store {
        owner: address,
        content: Content
    }

    /// Wrapping `content` into a tao the `owner` can only extract.
    public fun wrap<Content>(owner: address, content: Content): Tao<Content> {
        Tao<Content> { owner, content }
    }

    /// Immutable read-only reference to the owner address, and `content`.
    public fun read<Content>(tao: &Tao<Content>): (&address, &Content) {
        let Tao<Content> { owner, content } = tao;

        (owner, content)
    }

    /// If `account ` is the `owner`, extract `content`.
    public fun unwrap<Content>(account: &signer, tao: Tao<Content>): Content {
        let Tao<Content> { owner, content } = tao;

        assert!(owner == Signer::address_of(account), 123);

        content
    }
}
```

```move
/// A folder tao to store an arbitrary number of taos.
module 0x1::Folder {
    /// A simple tao struct containing a vector of resources.
    struct Tao<Content> has key, store {
        content: vector<Content>
    }

    /// Create a new tao, with the static set of resources inside it.
    public fun wrap<Content>(content: vector<Content>): Tao<Content> {
        Tao<Content> { content }
    }

    /// Immutable read-only reference to the vector containing resources.
    public fun read<Content>(tao: &Tao<Content>): &vector<Content> {
        let Tao<Content> { content } = tao;

        content
    }

    /// Destroy the tao, and return the static set of resources inside it.
    public fun unwrap<Content>(tao: Tao<Content>): vector<Content> {
        let Tao<Content> { content } = tao;

        content
    }
```

*A token can be placed inside `Ownable` and it can be placed inside `Folder`, or other way around, if so desired.*