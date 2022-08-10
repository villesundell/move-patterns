# Script Based Design

|||
|-|-|
| **Name** | Script Based Design |
| **Origin** | [Ville Sundell](https://github.com/villesundell) |
| **Example** | Diem Forum post lost, April 18 2022 |
| **Depends on** | [Accountless Design](./accountless_design.md) |
| **Known to work on** | Move |

## Summary

**Script Based Design** combines [Accountless Design](./accountless_design.md) with *Move Transaction Scripts* enabling a design where most of the business logic resides in transaction scripts, while keeping the most critical parts in modules. This way the transaction scripts can be developed and improved faster than a regular module would, while providing the same kind of guarantees as regular modules by keeping the most critical part (state transitions) in modules.

## Examples
