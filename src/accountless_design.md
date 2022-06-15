# Accountless Design

|||
|-|-|
| **Name** | Accountless Design |
| **Origin** | [Ville Sundell](https://github.com/villesundell) |
| **Example** | [Diem Forum Post](https://web.archive.org/web/20220202065315/https://community.diem.com/t/outbox-an-alternative-way-to-store-resources/3737) |
| **Depends on** | None |
| **Known to work on** | Move |

## Summary

Move module following the **Accountless Design** pattern doesn't handle storage (`move_to()` / `move_from()`) directly, instead the storage must be handled outside the module in transaction scripts. This makes the module code footprint smaller, design simpler, implementation more portable and provides a way to implement storage agnostic smart contract design on Move powered platforms.

## Examples