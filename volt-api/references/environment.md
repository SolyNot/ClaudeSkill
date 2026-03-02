# Environment

Access and manipulate Lua environments and the garbage collector.

## Global Environments

### `getgenv(): table`
Returns Volt's global environment — shared across all your script executions. Use to persist variables or inject globals.
```lua
getgenv().MyLib = { version = "1.0" }
-- Now accessible in any other Volt script:
-- print(MyLib.version)
```

### `getrenv(): table`
Returns the game's Lua environment (contains `game`, `workspace`, `script`, etc.).

### `gettenv(thread: thread): table`
Returns the environment table of the given coroutine thread.

### `getreg(): table`
Returns the Lua registry — a special internal table used by the Lua VM. Contains all loaded modules, threads, etc.

## Garbage Collector

### `getgc(include_tables?: boolean): {any}`
Returns all Lua objects currently tracked by the garbage collector. If `include_tables = true`, tables are included (can be very large).

### `filtergc(type: string, options?: table): {any}`
Filters GC objects by type and optional criteria. More efficient than iterating `getgc()` manually.

```lua
-- Find all functions with a specific upvalue name
local results = filtergc("function", {
    upvaluename = "mySecret"
})
```

Options table fields:
- `upvaluename: string` — filter closures by upvalue name
- `name: string` — filter by function name
- `namespace: string` — filter by namespace

## Environment Types Summary

| Function | Returns |
|---|---|
| `getgenv()` | Volt executor global env |
| `getrenv()` | Roblox game global env |
| `gettenv(thread)` | Specific thread's env |
| `getreg()` | Lua registry table |
