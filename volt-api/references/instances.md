# Instances

Interact with Roblox instances in privileged ways.

## Reference Management

### `cloneref(instance: Instance): Instance`
Creates a new independent reference to the same instance. Useful for bypassing cache-based identity checks.

### `compareinstances(a: Instance, b: Instance): boolean`
Returns `true` if both references point to the same underlying instance, even if they are different refs.

## Interaction Events

### `fireclickdetector(clickDetector: ClickDetector, distance?: number)`
Fires a ClickDetector as if the local player clicked it.
```lua
fireclickdetector(workspace.Door.ClickDetector)
```

### `fireproximityprompt(prompt: ProximityPrompt)`
Triggers a ProximityPrompt without the player being nearby.

### `firetouchinterest(part: BasePart, toucher: BasePart, toggle: 0|1)`
Simulates a touch event. `toggle = 1` = touch started, `0` = touch ended.
```lua
firetouchinterest(workspace.Trigger, game.Players.LocalPlayer.Character.HumanoidRootPart, 1)
```

## Instance Discovery

### `getinstances(): {Instance}` — All instances in the game (including nil-parented).
### `getnilinstances(): {Instance}` — Instances parented to `nil` (hidden/unparented).
### `getinstancecache(): {Instance}` — All instances currently in the reference cache.

## UI & Callbacks

### `gethui(): Instance`
Returns Volt's hidden UI container (a ScreenGui not visible to game scripts). Add your UI here to avoid detection.
```lua
local gui = Instance.new("ScreenGui")
gui.Parent = gethui()
```

### `getcallbackvalue(obj: Instance, property: string): function?`
Returns the current callback function assigned to a callback property (e.g. `BindableFunction.OnInvoke`).

## Rendering

### `getrendersteppedlist(): {[string]: function}`
Returns all functions registered with `RunService:BindToRenderStepped`.
