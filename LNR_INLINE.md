# LNR_INLINE

**Inline Functions**

Instead of calling your function, Lunari pastes the function's code directly where you use it.

## Usage

```lua
function LNR_INLINE(const function To_Inline)
```

## What it does

This macro puts your function's code directly where it was called, instead of making a function call. This removes the function call overhead but makes your output bigger since the code is being duplicated.

## Correct Usage ✅

```lua
-- Has to be assigned to a local
local Test_Func = LNR_INLINE(function(Start, End_N)
    local Total = 0
    for I = Start, End_N do
        Total = Total + I
    end
    return Total
end)

-- Using it
print(Test_Func(1, 100))

-- Simple getter func
local Get_Player_Health = LNR_INLINE(function()
    return Player.Health
end)

-- Math helper
local Clamp = LNR_INLINE(function(Value, Min, Max)
    if Value < Min then return Min end
    if Value > Max then return Max end
    return Value
end)

local Result = Clamp(X, 0, 100)
```

## Incorrect Usage ❌

```lua
-- ❌ Has to be assigned to something
LNR_INLINE(function() end)

-- ❌ No ... allowed
local Bad = LNR_INLINE(function(...)
    return ...
end)

-- ❌ Cant call itself
local Bad = LNR_INLINE(function()
    return Bad()
end)
```

## Limitations

1. **No `...`** - Variadic functions will NOT work
2. **No recursion** - The function can NOT call itself
3. **Specific format** - You HAVE to use `local Something = LNR_INLINE(function() ... end)`



## How it works

1. Lunari finds your `LNR_INLINE` declarations
2. Notes which variable holds it
3. Finds everywhere you call that variable
4. Replaces each call with the actual function code


## Example: Inlined math helpers

```lua
local Lerp = LNR_INLINE(function(A, B, T)
    return A + (B - A) * T
end)

local Clamp = LNR_INLINE(function(V, Lo, Hi)
    if V < Lo then return Lo end
    if V > Hi then return Hi end
    return V
end)

-- These become direct inline code
local Value = Clamp(Lerp(Start_Pos, End_Pos, 0.5), 0, 100)
```

## Tradeoff

Inlining trades **bigger code** for **faster execution**. Use it on small functions you call a lot.
