# DrawingImmediate

Immediate-mode (per-frame, stateless) screen drawing. No persistent objects — must redraw every frame inside a `GetPaint` event.

## Setup

```lua
local paint = DrawingImmediate.GetPaint(z_index)  -- returns VoltSignal
paint:Connect(function()
    -- All draw calls go here — fires every frame
    DrawingImmediate.FilledRectangle(
        Vector2.new(10, 10),
        Vector2.new(200, 50),
        Color3.new(1, 0, 0),
        1.0
    )
end)
```

- `z_index` controls render order. Lower = drawn earlier (behind), higher = in front.
- **All** `DrawingImmediate.*` calls **must** happen inside a `GetPaint` callback.

## Available Draw Functions

### Lines & Shapes

| Function | Signature |
|---|---|
| `Line` | `(from: Vector2, to: Vector2, color: Color3, thickness: number, transparency: number)` |
| `Circle` | `(center: Vector2, radius: number, color: Color3, thickness: number, transparency: number)` |
| `FilledCircle` | `(center: Vector2, radius: number, color: Color3, transparency: number)` |
| `Triangle` | `(a: Vector2, b: Vector2, c: Vector2, color: Color3, thickness: number, transparency: number)` |
| `FilledTriangle` | `(a: Vector2, b: Vector2, c: Vector2, color: Color3, transparency: number)` |
| `Rectangle` | `(pos: Vector2, size: Vector2, color: Color3, thickness: number, transparency: number)` |
| `FilledRectangle` | `(pos: Vector2, size: Vector2, color: Color3, transparency: number)` |
| `Quad` | `(a: Vector2, b: Vector2, c: Vector2, d: Vector2, color: Color3, thickness: number, transparency: number)` |
| `FilledQuad` | `(a: Vector2, b: Vector2, c: Vector2, d: Vector2, color: Color3, transparency: number)` |

### Text

| Function | Signature |
|---|---|
| `Text` | `(text: string, pos: Vector2, size: number, color: Color3, transparency: number, font?)` |
| `OutlinedText` | `(text: string, pos: Vector2, size: number, color: Color3, outlineColor: Color3, transparency: number, font?)` |

## vs. Standard Drawing

| | `Drawing` | `DrawingImmediate` |
|---|---|---|
| Persistence | Retained across frames | Per-frame only |
| Objects returned | Yes | No |
| Cleanup needed | Yes (`:Remove()`) | No |
| Use case | Static/tracked overlays | High-frequency ESP, per-frame HUD |
