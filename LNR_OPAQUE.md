# LNR_OPAQUE
boolean LNR_OPAQUE(const boolean Value)

Description: Swaps out a simple `true` or `false` with a nasty, complex math equation that analysts can't easily predict. It makes your logic flow much harder to map out because there's no clear "true" or "false" in the source! It adds a critical layer to your conditional checks.

Aliases: None

Correct Usage:

```lua
-- Obfuscate true/false logic
if Is_Admin == LNR_OPAQUE(true) then
    print("Welcome Admin")
end

-- Use in logic
local Can_Run = LNR_OPAQUE(true)
while Can_Run do
    -- logic
end
```

Incorrect Usage:

```lua
local Val = LNR_OPAQUE(Variable) -- argument must be a constant boolean.
local Val = LNR_OPAQUE(123) -- argument must be boolean (not number).
LNR_OPAQUE(true) -- Result must be used/assigned.
```


