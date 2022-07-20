# Hot Potato

|||
|-|-|
| **Name** | Hot Potato |
| **Origin** | [Sui Project](https://github.com/MystenLabs/sui/blob/20e68787b3ace2b408ba0c1d8d9117fc5206cb05/sui_programmability/examples/defi/sources/FlashLender.move#L19) / [Todd Nowacki](https://github.com/tnowacki) |
| **Example** | [FlashLender.move](https://github.com/MystenLabs/sui/blob/a6156aeaf332b9f257cf04063a9a751a7a431360/sui_programmability/examples/defi/sources/flash_lender.move) |
| **Depends on** | None |
| **Known to work on** | Move |

## Summary

A **Hot Potato** is a struct without `key`, `store` and `drop` [abilities](https://move-language.github.io/move/abilities.html) forcing the struct to be used within the transaction it was created in. This is desired in applications like [flash loans](https://github.com/MystenLabs/sui/blob/a6156aeaf332b9f257cf04063a9a751a7a431360/sui_programmability/examples/defi/sources/flash_lender.move) where the loans must be initiated and repaid during the same transaction.

## Examples

