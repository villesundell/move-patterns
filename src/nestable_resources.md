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

