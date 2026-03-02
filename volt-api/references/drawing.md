# Drawing

Persistent screen-overlay drawing objects (retained-mode).

## Creating Objects

```lua
local obj = Drawing.new(type)
```

Types: `"Line"`, `"Circle"`, `"Square"`, `"Triangle"`, `"Text"`, `"Image"`, `"Quad"`

Objects persist across frames until explicitly removed. Always call `:Remove()` when done.

## Common Properties (all types)

| Property | Type | Description |
|---|---|---|
| `Visible` | `boolean` | Show/hide |
| `ZIndex` | `number` | Render order (higher = on top) |
| `Transparency` | `number` | 0 = opaque, 1 = invisible |
| `Color` | `Color3` | Draw color |

## Type-Specific Properties

**Line**: `From: Vector2`, `To: Vector2`, `Thickness: number`

**Circle**: `Position: Vector2`, `Radius: number`, `Thickness: number`, `Filled: boolean`

**Square**: `Position: Vector2`, `Size: Vector2`, `Thickness: number`, `Filled: boolean`

**Triangle**: `PointA/B/C: Vector2`, `Thickness: number`, `Filled: boolean`

**Text**: `Position: Vector2`, `Text: string`, `Size: number`, `Font: Drawing.Fonts.*`, `Center: boolean`, `Outline: boolean`, `OutlineColor: Color3`

**Image**: `Position: Vector2`, `Size: Vector2`, `Data: string` (raw image bytes or rbxasset uri)

**Quad**: `PointA/B/C/D: Vector2`, `Thickness: number`, `Filled: boolean`

## Utility Functions

### `cleardrawcache()` — Remove all drawing objects at once.
### `isrenderobj(obj): boolean` — Check if a value is a drawing object.
### `getrenderproperty(obj, prop: string): any` — Get a property by name string.
### `setrenderproperty(obj, prop: string, value: any)` — Set a property by name string.

## Example

```lua
local box = Drawing.new("Square")
box.Position = Vector2.new(100, 100)
box.Size = Vector2.new(200, 50)
box.Color = Color3.fromRGB(255, 0, 0)
box.Thickness = 2
box.Filled = false
box.Visible = true

local label = Drawing.new("Text")
label.Text = "Hello"
label.Position = Vector2.new(100, 80)
label.Size = 18
label.Color = Color3.new(1,1,1)
label.Visible = true

-- Cleanup
task.delay(5, function()
    box:Remove()
    label:Remove()
end)
```
