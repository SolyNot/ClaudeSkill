# Signals

Fire and manage Roblox RBXScriptSignal events (RemoteEvents, BindableEvents, built-in signals).

## Functions

### `firesignal(signal: RBXScriptSignal, ...: any)`
Fire any RBXScriptSignal programmatically, calling all connected handlers with the given arguments.
```lua
-- Fire a signal as if the event occurred
firesignal(game.Players.LocalPlayer.CharacterAdded, game.Players.LocalPlayer.Character)
```

### `getconnections(signal: RBXScriptSignal): {Connection}`
Returns all active connections on a signal. Each connection object has:
- `.Function` — the connected callback
- `.State` — connection state
- `:Fire(...)` — fire just this connection
- `:Disconnect()` — disconnect it
- `:Enable()` / `:Disable()` — toggle without removing

```lua
local conns = getconnections(workspace.ChildAdded)
for _, c in ipairs(conns) do
    print(c.Function)
end
```

### `replicatesignal(signal: RBXScriptSignal, ...: any)`
Fire a signal for replication to the server. Used for events that have server-side listeners.

### `cansignalreplicate(signal: RBXScriptSignal): boolean`
Returns `true` if the signal supports server replication.

### `getsignalarguments(signal: RBXScriptSignal): {string}`
Returns the argument type names the signal passes to connected handlers.

### `getsignalargumentsinfo(signal: RBXScriptSignal): {table}`
Returns detailed type info for each signal argument.

### `getsignalwhitelist(signal: RBXScriptSignal): {string}?`
Returns the whitelist of allowed sources for this signal, if any.

## Example: Disable all game connections on a signal

```lua
local conns = getconnections(workspace.Part.Touched)
for _, c in ipairs(conns) do
    c:Disable()  -- temporarily mute without disconnecting
end
```
