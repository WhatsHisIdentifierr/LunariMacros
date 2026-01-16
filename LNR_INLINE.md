# LNR_INLINE
function LNR_INLINE(const function To_Inline)

Description: Tells the obfuscator to copy the function body directly into every place you call it. It basically deletes the manual function call to boost speed, but watch out for file size if you inline huge functions. It's essentially source-level inlining.

Aliases: None

Correct Usage:

```lua
-- Define inline function
local Add_Numbers = LNR_INLINE(function(A, B)
    return A + B
end)

-- Call it (code is pasted here)
print(Add_Numbers(1, 2))
```

Incorrect Usage:

```lua
LNR_INLINE(function() end) -- must be assigned to a variable.
local Fn = LNR_INLINE(Existing_Func) -- argument must be a function literal.
local Fn = LNR_INLINE(function(...) end) -- varargs (...) are not supported in inlined functions.
local Recursive = LNR_INLINE(function() Recursive() end) -- recursion is not supported.
```
