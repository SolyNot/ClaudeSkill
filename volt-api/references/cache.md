# Cache

Manipulate the Roblox instance reference cache.

## Functions

### `cache.replace(old: Instance, new: Instance)`
All existing references to `old` now resolve to `new`. The original instance still exists internally.
```lua
local fake = Instance.new("Part")
fake.Name = "Disguised"
cache.replace(workspace.RealPart, fake)
print(workspace.RealPart.Name) -- "Disguised"
```

### `cache.invalidate(instance: Instance)`
Removes `instance` from the cache. The next access creates a fresh reference.
```lua
cache.invalidate(workspace.Part)
```

### `cache.iscached(instance: Instance): boolean`
Returns `true` if the instance is currently in the reference cache.
```lua
print(cache.iscached(workspace.Part)) -- true
cache.invalidate(workspace.Part)
print(cache.iscached(workspace.Part)) -- false
```

## Related
- `cloneref(instance)` — in Instances library, creates an independent reference copy.
- `compareinstances(a, b)` — checks if two refs point to same underlying instance.
