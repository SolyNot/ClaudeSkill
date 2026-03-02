# VoltSignal

Volt's own custom signal/event implementation. Used internally by Volt (e.g. `on_actor_state_created`, `LuaStateProxy.Event`, `DrawingImmediate.GetPaint`).

## Classes

### VoltSignal

#### `VoltSignal.new(): VoltSignal`
Create a new signal.
```lua
local signal = VoltSignal.new()
```

#### `VoltSignal:Connect(callback: function): VoltConnection`
Connect a handler. Fires every time the signal fires.
```lua
local conn = signal:Connect(function(a, b)
    print("fired:", a, b)
end)
```

#### `VoltSignal:Once(callback: function): VoltConnection`
Connect a handler that fires only once, then disconnects itself.

#### `VoltSignal:Wait(): (...any)`
Yields the current thread until the signal fires. Returns the fired arguments.
```lua
local a, b = signal:Wait()
```

#### `VoltSignal:Fire(...: any)`
Fire the signal, calling all connected handlers with the given arguments.
```lua
signal:Fire("hello", 42)
```

### VoltConnection

Returned by `:Connect()` and `:Once()`.

#### `VoltConnection:Disconnect()`
Disconnect this handler from the signal.
```lua
local conn = signal:Connect(myFunc)
-- Later:
conn:Disconnect()
```

## Example

```lua
local onDamage = VoltSignal.new()

onDamage:Connect(function(amount)
    print("Took", amount, "damage")
end)

onDamage:Fire(25)  -- prints: Took 25 damage
```
