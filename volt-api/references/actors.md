# Actors

Parallel Luau execution and Lua state management.

## Functions

### `getactors(): {Actor}`
Alias: `get_actors`. Returns all Actor instances in the game.
```lua
local actors = getactors()
for i, actor in ipairs(actors) do print(i, actor:GetFullName()) end
```

### `run_on_actor(actor: Actor, source: string, ...: any)`
Execute a script string on the actor's Lua state. Varargs are passed as `...` inside the script.
```lua
local actor = Instance.new("Actor")
actor.Parent = workspace
run_on_actor(actor, [[
    print("args:", ...)
]], "hello", 42)
```

### `isparallel(): boolean`
Alias: `is_parallel`. Returns `true` when called inside an actor (parallel context).

### `getluastate(actor_or_script?: Actor | BaseScript): LuaStateProxy`
Returns the LuaStateProxy for the given actor/script, or the current state if no arg given.

### `getgamestate(): LuaStateProxy`
Returns the LuaStateProxy for the default game Lua state (`IsActorState = false`).

### `getactorstates(): {LuaStateProxy}`
Returns all active LuaStateProxy objects (actor states + game state).

### `create_comm_channel(): (number, BindableEvent)`
Creates a communication channel. Returns `(id, bindableEvent)`. The BindableEvent exposes `.Event` and `:Fire(...)`.
```lua
local id, channel = create_comm_channel()
channel.Event:Connect(function(msg) print("Got:", msg) end)
run_on_actor(actor, [[
    local ch = get_comm_channel(...)
    ch:Fire("hello from actor")
]], id)
```

### `get_comm_channel(id: number): BindableEvent`
Retrieves a channel created with `create_comm_channel` by ID. Used inside actors to talk back to main thread.

### `on_actor_state_created: VoltSignal<Actor>`
VoltSignal that fires **before** any scripts run on a new actor state. Useful for early injection.
```lua
on_actor_state_created:Connect(function(actor)
    local state = getluastate(actor)
    state:Execute([[ print("injected early!") ]])
end)
```

## LuaStateProxy

Object representing a Lua execution environment.

| Member | Type | Description |
|---|---|---|
| `Id` | `number` | Unique state identifier |
| `IsActorState` | `boolean` | True if this is an actor state |
| `Event` | `VoltSignal` | Fires when the state receives a message |
| `:GetActors()` | `{Actor}` | All actors associated with this state |
| `:Execute(source: string, ...: any)` | — | Run code on this state with optional varargs |
