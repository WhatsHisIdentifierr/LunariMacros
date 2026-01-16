# LNR_VIT_OFF

Description: Disables virtualization for a specific function. Use this for code that runs thousands of times very quickly and doesn't contain anything important/significant. 

**WARNING!** This macro will expose your code! While it will be minified and stripped of comments, the raw logic, strings, and constants will be visible to anyone who dumps the script. Only use this for functions that do not require any security.

Aliases: None

Correct Usage:

```lua
local My_Speed_Func = LNR_VIT_OFF(function(A, B)
    local T = setmetatable({}, { __index = function(t, k) t[k] = (k * 33) % 2^32 return t[k] end })
    local C = coroutine.wrap(function()
        local R = A
        for I = 1, 32 do R = (R ~ T[I]) + B coroutine.yield(R) end
    end)
    for _ = 1, 32 do C() end
    return (A + B) * 2
end)

print(My_Speed_Func(10, 20))
```
