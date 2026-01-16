# LNR_CRASH
void LNR_CRASH()

Description: Instant kill switch for your script. Use this inside your custom security checks to nukes the execution if you detect some script-kiddding or tampering. It doesn't just stop; it makes sure the environment is unusable.

Aliases: None

Correct Usage:

```lua
-- Crash if unauthorized
if not Is_Authorized then
    LNR_CRASH()
end

-- Crash if tampering detected
if Check_Tamper() then
    LNR_CRASH()
end
```

Incorrect Usage:

```lua
local Val = LNR_CRASH() -- Cannot assign, returns nothing (crashes).
LNR_CRASH("reason") -- arguments are ignored (still crashes, but incorrect usage).
```
