# LNR_OPAQUE

**Opaque Predicates**

Replaces a boolean with a complex math expression that evaluates to the same value.

## Usage

```lua
boolean LNR_OPAQUE(const boolean Value)
```

## What it does

If you have important security checks like `if Is_Admin == true`, bums who want to crack it can easily find and flip that boolean. This macro replaces `true` or `false` with a complex algebraic expression that evaluates to the same value at runtime.

For example, `LNR_OPAQUE(true)` might become something like `((47 * 47) >= 0)` which is always true, but WAY harder to reverse.

## Correct Usage ✅

```lua
-- Basic usage in conditionals
if Is_Whitelisted == LNR_OPAQUE(true) then
    -- Protected code here
end

-- Checking for false
if Is_Banned == LNR_OPAQUE(false) then
    -- User is not banned
end

-- In variable assignments
local Should_Run = LNR_OPAQUE(true)
if Should_Run then
    Run_Protected_Code()
end

-- Multiple checks
if Has_License == LNR_OPAQUE(true) and Is_Valid == LNR_OPAQUE(true) then
    -- Both conditions use opaque predicates
end
```

## Incorrect Usage ❌

```lua
-- ❌ You HAVE to pass a constant (true or false), NOT a variable
local Is_Whitelisted = true
if User == LNR_OPAQUE(Is_Whitelisted) then end

-- ❌ Booleans ONLY, not numbers or strings
local Val = LNR_OPAQUE(100)
local Str = LNR_OPAQUE("true")

-- ❌ You HAVE to use the return value, it's not a standalone call
LNR_OPAQUE(true)
```

## How it works

1. Lunari finds all your `LNR_OPAQUE` calls
2. Picks a random algebraic pattern that always evaluates to the boolean you passed
3. Replaces the macro with that complex expression
4. At runtime, the math runs andgives you the correct boolean 

## Why this prevents logic flipping

**Without LNR_OPAQUE:**
```lua
if admin == true then  -- Bum finds this and flips it to false 😡
```

**With LNR_OPAQUE (before other obfuscation):**
```lua
if admin == (((47 + 23) - 23) == 47) then
```

**After full Lunari obfuscation:**
```lua
H:oP8eH5(u[47832], u[92847]) -- Bum has no idea what this is doing 😈
```

The opaque predicate is just the first layer. Then the other obfuscation steps:
- Encrypt all the numbers (47, 23, etc. become unreadable)
- Virtualize the operations (math becomes VM bytecode)
- Mangle all the variable names

So even if someone knows the pattern of it, they can't find or change the numbers because they're encrypted and hidden inside the VM.

## When to use it

- License/whitelist checks
- Admin permission checks
- Critical security conditionals
- Any boolean check you don't want flipped

## Performance

Very minimal depending on how much it's used, if it's used a lot you may notice a moderate decrease in performance, if you only use it 2-3 times you shouldn't worry..

## Common Missunderstandings

**"Doesn't it just evaluate to true anyway?"**
Yes, of course it does, your code needs it to be true to work. The point isnt just to hide the *result*, but to hide the *location*. There is no simple `true` boolean in the file for someone reversing to find and flip. They have to devirtualize the whole script to even find where the check happens.

**"Can't I just hook the equality check?"**
No. Logic operators like `==` on booleans cannot be hooked in Lua/Luau because they don't use metamethods. The check happens inside the VM and it's internal instruction loop, so standard hooking methods wont work 💔.



