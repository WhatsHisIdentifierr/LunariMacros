# LNR_JIT
function LNR_JIT(const function To_Optimize)

Description: Dial back the obfuscation for a specific function to squeeze out extra performance. Perfect for heavy-duty stuff like render loops or complex math where you need speed more than maximum protection. Just remember: less obfuscation means it's a bit easier to peek at.

Aliases: LNR_JIT_MAX (Stronger optimization, less obfuscation)

Correct Usage:

```lua
-- Optimize a specific function
local My_Func = LNR_JIT(function() 
    -- fast code here
end)

-- Optimize a loop by wrapping it
LNR_JIT(function()
    for I = 1, 1000 do 
        -- heavy logic
    end
end)()
```

Incorrect Usage:

```lua
local My_Func = LNR_JIT(Existing_Function_Variable) -- argument must be a function literal.
LNR_JIT(function() end, function() end) -- too many arguments passed.
LNR_JIT() -- not enough arguments passed.
```
