# LNR_PNUM
number LNR_PNUM(const number To_Encrypt)

Description: Slaps an extra layer of complex, randomized math on top of your numbers. This makes it a nightmare for anyone trying to scan memory for specific values like health, damage, or currency.

Aliases: None

Correct Usage:

```lua
local My_Number = LNR_PNUM(123)
print(LNR_PNUM(456.78))
return LNR_PNUM(0)
```

Incorrect Usage:

```lua
local My_Number = LNR_PNUM(Variable) -- argument acts weird if it isn't a constant.
print(LNR_PNUM(1, 2)) -- too many arguments passed.
print(LNR_PNUM()) -- not enough arguments passed.
```
