# LNR_CRASH

**Kill the VM**

Crashes Lunari's Lua VM.

## Aliases

Only name is: `LNR_CRASH`.

## Usage

```lua
void LNR_CRASH()
```

## Purpose

Lunari already has built in anti-tamper, but if you want to add your own custom checks, use this macro. It crashes the Lua VM when it is ran, the script crashes and cannot be recovered.

## Correct Usage ✅

```lua
-- In a return
return LNR_CRASH()

-- In a custom detection
if Is_Hooked(getfenv) then
    LNR_CRASH()
end

-- If a license check failed and it shouldn't
if not Validate_License(Key) then
    LNR_CRASH()
end
```

## Incorrect Usage

There isn't really any incorrect usage. If `LNR_CRASH()` is ran, the VM crashes, simple. Doesn't matter what else you pass.

```lua
-- All of these crash the VM
LNR_CRASH()
LNR_CRASH(1, 2, 3)
LNR_CRASH("whatever")
```

## How it works

When you obfuscate, `LNR_CRASH()` gets replaced with one of several crash methods:
- Stack overflow from infinite recursion
- Memory bomb
- Metatable loops

Which one you get is random each build.

## When to use it

- Caught hook functions
- License validation failed
- Integrity checks failed
- Found debuggers or analysis tools
- Kill switch when someone's tampering


## Keep in mind

1. **No recovery** - Once it runs, the VM WILL crash, you cannot recover it
2. **Different each build** - Every obfuscation uses different crash code

## Don't crash your real users

Always use conditions so you only crash when something's actually wrong:

```lua
-- Good - only crashes on tampering
if Tampered_Detected then
    LNR_CRASH()
end

-- Bad - crashes everyone
LNR_CRASH()
```


