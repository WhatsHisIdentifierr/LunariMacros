# Lunari Macro FAQ

## What are Macros?
Lunari macros allow you to control the obfuscation process for specific parts of your code. By using these special function calls, you can instruct Lunari to apply stronger encryption to sensitive strings, optimize, or make custom anti-tamper.

## How do I test my script without obfuscating?
Since macros like `LNR_PSTR` are only used by the obfuscator, running your raw script will cause nil value errors. To work around this and test your script, you should define "passthrough" globals at the top of your script that only run when the script is *not* obfuscated.

```lua
if not LNR_OBFUSCATED then
    getgenv().LNR_PSTR = function(x) return x end
    getgenv().LNR_PNUM = function(x) return x end
    getgenv().LNR_JIT = function(f) return f end
    getgenv().LNR_INLINE = function(f) return f end
    getgenv().LNR_OPAQUE = function(x) return x end
    getgenv().LNR_CRASH = function() end
end
```

Lunari automatically removes these during the obfuscation process.

## Reserved Identifiers
The `LNR_` prefix is strictly reserved for Lunari's internal use.
*   **Do not** name your own variables starting with `LNR_` (e.g., `local LNR_MyVar = 1` will cause an error).
*   **Do not** attempt to call non-existent macros (e.g., `LNR_FAKE_MACRO()`).

## Available Macros
*   [LNR_PSTR](LNR_PSTR.md) - String Encryption
*   [LNR_PNUM](LNR_PNUM.md) - Number Encryption
*   [LNR_JIT](LNR_JIT.md) - Performance Optimization
*   [LNR_CRASH](LNR_CRASH.md) - VM Crash
*   [LNR_INLINE](LNR_INLINE.md) - Function Inlining
*   [LNR_OPAQUE](LNR_OPAQUE.md) - Replaces static booleans with runtime-calculated opaque predicates.
*   [LNR_VIT_OFF](LNR_VIT_OFF.md) - Disables virtualization for a specific function (Performance).