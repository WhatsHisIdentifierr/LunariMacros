# LNR_PSTR
string LNR_PSTR(const string To_Encrypt)

Description: Wraps your string in an extra layer of heavy, multi-stage encryption. It's basically a must-have for hiding API keys, webhooks, or any secrets you'd rather not have leaked.

Aliases: None

Correct Usage:

```lua
local My_String = LNR_PSTR("Important String")
print(LNR_PSTR("Hello, World!"))
return LNR_PSTR("Goodbye!")
```

Incorrect Usage:

```lua
local My_String = LNR_PSTR(Variable) -- argument acts weird if it isn't a constant.
print(LNR_PSTR("A", "B")) -- too many arguments passed.
print(LNR_PSTR()) -- not enough arguments passed.
```
