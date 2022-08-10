# Multiple Configurations

|||
|-|-|
| **Name** | Multiple Configurations |
| **Origin** | [Ville Sundell](https://github.com/villesundell) |
| **Example** | [Diem Forum Post](https://web.archive.org/web/20211130211815/https://community.diem.com/t/multiple-configurations-approach-a-possible-design-pattern/3485) |
| **Depends on** | None |
| **Known to work on** | Move |

## Summary

In the **Multiple Configurations** approach singletons (especially for configuration data) are provided to the module as arguments instead of storing them to any specific location. 

By incorporating this design into your modules, you would automatically add a layer of configurability by giving users or admins (if any) a way to create configurations which others could use. This would be similar to Uniswap which lets anyone create markets others could participate in.

## Examples

Let's say you have an auction smart contract X and an admin has created a configuration to account A. Then B could issue a transaction script to bid on C's resource like this:

```move
X::place_bid(A, C, 1234);
```

By accepting parameters (such as C and the amount 1234), a transaction script could trivially hide the selection of the configuration. This depends, how flexible the final script implementation is in terms of arguments to `main()`, but the transaction script could look like this (quick mock-up):

```move
script {
    use 0xFF::X;

    const CONF: address = 0xCOFFEE;

    fun main(a: address, amount: XUS) {
        X::place_bid(CONF, a, amount);
    }
}
```
