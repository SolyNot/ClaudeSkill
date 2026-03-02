# oth (On-Thread Hooking)

Thread-safe alternative to `hookfunction` for hooking **C functions**. Hooks execute on separate threads for better isolation.

## Why oth?

- `hookfunction` cannot safely hook C closures — use `oth.hook` instead.
- Hooks run on isolated threads, preventing crashes from hook conflicts.
- You can detect whether code is currently inside a hook context.

## Functions

### `oth.hook(target: function, hook: function): originalFunction`
Hook `target` with `hook`. The hook runs on a separate thread. Returns the original function.

```lua
local originalWarn = oth.hook(warn, function(...)
    print("[intercepted warn]", ...)
    -- call original via oth.get_root_callback or the returned ref
    originalWarn(...)
end)
```

### `oth.unhook(target: function)`
Remove the hook from `target`, restoring the original behavior.

### `oth.get_root_callback(target: function): function`
Returns the deepest/original function before any hooks were applied. Useful when multiple hooks are stacked.

### `oth.is_hook_thread(): boolean`
Returns `true` if the current thread is an oth hook thread (i.e., you're inside a hook callback).

### `oth.get_original_thread(): thread`
Returns the original thread that triggered the hook. Allows accessing the calling context.

## Example: Hook a C function safely

```lua
local orig = oth.hook(game.GetService, function(self, serviceName)
    print("GetService called for:", serviceName)
    return orig(self, serviceName)
end)
```

## Related
- `closures/hookfunction` — for Luau closure hooking (inline, same thread)
- `closures/hookmetamethod` — for metamethod hooking
