# Reflection

Access hidden properties, thread identity, and property scriptability.

## Hidden Properties

### `gethiddenproperty(instance: Instance, property: string): (any, boolean)`
Returns `(value, isHidden)`. Reads properties not normally accessible via Luau.
```lua
local val, hidden = gethiddenproperty(workspace.Part, "SomeHiddenProp")
```

### `gethiddenproperties(instance: Instance): {[string]: any}`
Returns a table of all hidden properties and their values for the instance.

### `sethiddenproperty(instance: Instance, property: string, value: any)`
Write a hidden property value.

### `getproperties(instance: Instance): {[string]: any}`
Returns all properties (normal + hidden) and their current values.

### `isscriptable(instance: Instance, property: string): boolean`
True if the property is currently scriptable (accessible from Lua).

### `setscriptable(instance: Instance, property: string, scriptable: boolean): boolean`
Toggle scriptability of a property. Returns previous state.
```lua
-- Make a normally inaccessible property readable
local old = setscriptable(workspace.Part, "HiddenProp", true)
print(workspace.Part.HiddenProp)
setscriptable(workspace.Part, "HiddenProp", old)
```

## Thread Identity

Thread identity controls what privileged operations are allowed. Volt runs at identity 8 (max).

| Level | Name | Capabilities |
|---|---|---|
| 0 | None | Sandboxed |
| 2 | Plugin | Basic game access |
| 3 | RobloxPlugin | Extended plugin |
| 5 | CoreScript | Core access |
| 6 | RobloxScript | Roblox internal |
| 7 | RobloxGameScript | Game services |
| 8 | RobloxScript | Maximum (executor level) |

### `getthreadidentity(): number` — Get current identity level.
### `setthreadidentity(level: number)` — Set identity level.

```lua
print(getthreadidentity())  -- 8
setthreadidentity(3)  -- drop to plugin level
```

## Network & Simulation

### `isnetworkowner(part: BasePart): boolean`
Returns true if the local player is the network owner of the part.

### `setsimulationradius(radius: number)`
Override the local simulation radius (controls physics simulation range).
