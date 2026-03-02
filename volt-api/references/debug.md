# Debug

Extended `debug` library for inspecting and modifying Luau function internals.

## Terminology

- **Constants**: Literal values embedded in bytecode (strings, numbers, booleans).
- **Upvalues**: Variables captured from outer scope by a closure.
- **Protos**: Sub-functions (inner functions) defined inside a function.
- **Stack**: The call stack / local variable slots at a given call level.

## Functions

### `debug.getconstants(func): {any}` — All constants of `func`.
### `debug.getconstant(func, index: number): any` — Constant at `index`.
### `debug.setconstant(func, index: number, value: any)` — Replace a constant.

### `debug.getupvalues(func): {any}` — All upvalues.
### `debug.getupvalue(func, index: number): any` — Upvalue at `index`.
### `debug.setupvalue(func, index: number, value: any)` — Replace an upvalue.

### `debug.getprotos(func): {ProtoProxy}` — All inner functions as ProtoProxy objects.
### `debug.getproto(func, index: number, activated?: boolean): ProtoProxy | {function}` 
Returns the proto at `index`. If `activated = true`, returns active closures of that proto.

### `debug.getstack(level: number, index?: number): any | {any}`
Get local variable(s) at call stack `level`. `level = 1` is the current function.

### `debug.setstack(level: number, index: number, value: any)` — Set a stack local.

### `debug.getinfo(func_or_level): table`
Returns info table with fields like `source`, `currentline`, `nups`, `numparams`, `is_vararg`, `what`.

### `debug.getcallstack(level?: number): {table}` — Full call stack info.

### `debug.validlevel(level: number): boolean` — True if a stack level is valid.

## ProtoProxy

Returned by `debug.getproto`. Represents a sub-function definition. Use `activated = true` on `getproto` to get real callable closures.

## Example

```lua
-- Patch a constant in a game module
local mod = require(game.ReplicatedStorage.SomeModule)
local consts = debug.getconstants(mod.someFunction)
for i, v in ipairs(consts) do
    if v == "oldValue" then
        debug.setconstant(mod.someFunction, i, "newValue")
    end
end
```
