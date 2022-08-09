# Accountless Design

|||
|-|-|
| **Name** | Accountless Design |
| **Origin** | [Ville Sundell](https://github.com/villesundell) |
| **Example** | [Diem Forum Post](https://web.archive.org/web/20220202065315/https://community.diem.com/t/outbox-an-alternative-way-to-store-resources/3737) |
| **Depends on** | None |
| **Known to work on** | Move |

## Summary

Move module following the **Accountless Design** pattern doesn't handle storage (`move_to()` / `move_from()`) directly, instead the storage must be handled outside the module in transaction scripts. This makes the module code footprint smaller, design simpler, implementation more portable and provides a way to implement storage agnostic smart contract design on some Move powered platforms.

## Examples

```move
module 0x1::Outbox {
    use Std::Event;
    use Std::Signer;
    use Std::Vector;

    struct Item<Content: key + store> has key, store {
        from: address,
        to: address,
        content: Content
    }

    struct Outbox<Content: key + store> has key, store {
        content: vector<Item<Content>>
    }

    struct Put<phantom Content> has key, drop, store {
    }

    struct EventHandle<phantom Content: drop + store> has key, store {
        event_handle: Event::EventHandle<Content>
    }

    public fun create<Content: key + store>(account: &signer) {
        move_to<Outbox<Content>>(account, Outbox<Content> { content: Vector::empty<Item<Content>>() });
        move_to<EventHandle<Put<Content>>>(account, EventHandle<Put<Content>> { event_handle: Event::new_event_handle<Put<Content>>(account) } );
    }

    public fun put<Content: key + store>(account: &signer, from: address, to: address, content: Content) acquires EventHandle, Outbox {
        let outbox_owner = Signer::address_of(account);
        let event_handle = borrow_global_mut<EventHandle<Put<Content>>>(outbox_owner);
        let outbox = borrow_global_mut<Outbox<Content>>(outbox_owner);

        assert!(to != @0x0, 123);

        Vector::push_back<Item<Content>>(&mut outbox.content, Item<Content>{ from, to, content });
        Event::emit_event<Put<Content>>(&mut event_handle.event_handle, Put<Content> {});
    }

    public fun get<Content: key + store>(account: &signer, outbox_owner: address, index: u64): Content acquires Outbox {
        let account_addr = Signer::address_of(account);
        let outbox = borrow_global_mut<Outbox<Content>>(outbox_owner);

        let Item<Content>{from, to, content} = Vector::swap_remove<Item<Content>>(&mut outbox.content, index);

        assert!(from == account_addr || to == account_addr, 123);

        content
    }
}
```

*Now `Outbox` can be used to retrieve and store resources in transaction scripts, and pass those to modules following the [Script Based Design](./script_based_design.md) pattern.*