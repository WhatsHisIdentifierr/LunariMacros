# LNR_JIT / LNR_JIT_MAX

**Make it Fast**

Tells Lunari to go easier on a function so it runs faster. Use this for stuff that NEEDS speed.

## Aliases

- `LNR_JIT` - Lighter obfuscation
- `LNR_JIT_MAX` - Even lighter (fastest)

## Usage

```lua
function LNR_JIT(const function To_Optimize)
function LNR_JIT_MAX(const function To_Optimize)
```

## Purpose

If you have functions that need to run fast (like render loops or heavy math), this macro tells Lunari to use lighter obfuscation on them. The function still gets protected, just not as heavily.

## Correct Usage ✅

```lua
-- Basic - returns the fast function
local My_Function = LNR_JIT(function()
    -- Fast code here
end)


LNR_JIT(function()
    for I = 1, 1000 do
        -- We most of the time would want this to be fast since it runs multiple times per second, so we use LNR_JIT
    end
end)()

-- Pass as argument
Some_Function(LNR_JIT(function()
    return "optimized!"
end))


local Ultra_Fast = LNR_JIT_MAX(function(A, B) -- Heavy math calculations, so we use LNR_JIT_MAX (math would usually be more heavy but this is just an example)
    return A * B + A / B
end)

-- Rendering
local Render = LNR_JIT(function(Dt) -- Rendering can be pretty heavy most of the time, so we use LNR_JIT (rendering would usually be more heavy but this is just an example)
    for _, Entity in pairs(Entities) do
        Entity:Draw()
    end
end)
```

## Incorrect Usage ❌

```lua
-- ❌ It does NOT call the function for you!
LNR_JIT(function() 
    print("This won't print!")
end)

-- You HAVE to actually call it in your code:
-- ✅ Right way:
LNR_JIT(function() 
    print("This will print!")
end)()  -- See the () at the end?

-- ❌ It does NOT work with existing functions
local Existing_Func = function() end
local Optimized = LNR_JIT(Existing_Func)

-- ❌ Only ONE function at a time
local Bad = LNR_JIT(function() end, function() end)
```

## How it works

1. Lunari finds your `LNR_JIT`/`LNR_JIT_MAX` calls
2. Marks those functions to skip the heavy parts
3. They still get most of the basic protection, just not the most performance heavy parts of it
4. `LNR_JIT_MAX` skips even more for when you really need speed

## LNR_JIT vs LNR_JIT_MAX

**LNR_JIT** still keeps most protections but skips the really slow stuff:
- Variables get renamed
- Code gets minified
- Light VM wrapping
- Control flow obfuscation stays on
- Strings and numbers still get encrypted

**LNR_JIT_MAX** skips almost everything for speed:
- Variables get renamed
- Code gets minified
- That's pratically it - everything else is skipped

Basically: `LNR_JIT` = faster but still protected, `LNR_JIT_MAX` = as fast as possible

## When to use which

### LNR_JIT for:
- Render loops
- Physics calculations  
- Big data processing
- Heavy UI updates
- Anything running many times per second

### LNR_JIT_MAX for:
- Inner loops running millions of times
- Very math heavy algorithms
- Very heavy rendering functions that render multiple things per frame.

## Example: Game loop

```lua
local Update_Physics = LNR_JIT_MAX(function(Dt)
    for _, Body in ipairs(Bodies) do
        Body.X = Body.X + Body.VX * Dt
        Body.Y = Body.Y + Body.VY * Dt
        Body.VY = Body.VY + Gravity * Dt
    end
end)

local Render = LNR_JIT(function()
    for _, Sprite in ipairs(Sprites) do
        Sprite:Draw()
    end
end)

-- Main loop
while Running do
    local Dt = Get_Delta_Time()
    Update_Physics(Dt)
    Render()
end
```

## Tradeoff

Faster = less protected. Don't use these on:
- License checks
- Custom anti-tamper code
- Sensitive business logic
- Anything you really want secured

