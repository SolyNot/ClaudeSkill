# WebSocket

Real-time bidirectional WebSocket connections.

## Constructor

### `WebSocket.connect(url: string): WebSocket`
Opens a WebSocket connection to `url`. Blocks until connected (or errors).
```lua
local ws = WebSocket.connect("ws://localhost:8080")
```

## Properties

### `WebSocket.OnMessage: Signal`
Fires when a message is received from the server. Handler receives `(message: string)`.
```lua
ws.OnMessage:Connect(function(msg)
    print("Received:", msg)
end)
```

### `WebSocket.OnClose: Signal`
Fires when the connection is closed (by either side). No arguments.
```lua
ws.OnClose:Connect(function()
    print("Connection closed")
end)
```

## Methods

### `WebSocket:Send(message: string)`
Send a text message to the server.
```lua
ws:Send("Hello server!")
ws:Send(game:GetService("HttpService"):JSONEncode({ action = "ping" }))
```

### `WebSocket:Close()`
Gracefully close the connection.
```lua
ws:Close()
```

## Full Example

```lua
local ws = WebSocket.connect("ws://localhost:8080")

ws.OnMessage:Connect(function(msg)
    print("Server says:", msg)
end)

ws.OnClose:Connect(function()
    print("WebSocket disconnected")
end)

ws:Send("Hello!")

-- Keep alive loop
while task.wait(1) do
    ws:Send("ping")
end
```
