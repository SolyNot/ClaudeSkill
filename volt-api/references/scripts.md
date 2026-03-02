# Scripts

Interact with running scripts, modules, and Lua code loading.

## Script Discovery

### `getscripts(): {LocalScript | Script | ModuleScript}`
All scripts currently in the game's instance tree.

### `getrunningscripts(): {LocalScript | Script}`
Scripts that are actively running (not just present in the tree).

### `getmodules(): {ModuleScript}`
All ModuleScript instances in the game.

### `getloadedmodules(): {ModuleScript}`
ModuleScripts that have been `require()`-d and are cached.

### `getcallingscript(): LocalScript | Script | nil`
Returns the script that called the current function. Useful in hooks.

### `getscriptfromthread(thread: thread): BaseScript?`
Returns the script associated with a given coroutine thread.

## Script Environments & Source

### `getsenv(script: BaseScript): table`
Returns the environment table (globals) of the given script. Access its internal variables.
```lua
local env = getsenv(workspace.SomeLocalScript)
print(env.someGlobal)
```

### `getscriptclosure(script: BaseScript): function`
Returns the main closure (function) of the script.

### `getscriptbytecode(script: BaseScript): string`
Returns the compiled bytecode of the script.

### `getscripthash(script: BaseScript): string`
Returns a hash of the script's bytecode. Useful for identifying script versions.

## Code Loading

### `loadstring(code: string, chunkname?: string): (function?, string?)`
Compile and load a Lua string as a function. Returns `(func, nil)` on success or `(nil, error)`. Works even when the game has disabled it.
```lua
local fn, err = loadstring("return 1 + 1")
if fn then print(fn()) end  -- 2
```
