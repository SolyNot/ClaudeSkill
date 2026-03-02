# Encoding

Encode/decode data. Functions available both as standalone globals and under `crypt.*`.

## Base64

### `base64encode(data: string): string`
Aliases: `crypt.base64encode`, `base64_encode`
```lua
local encoded = base64encode("Hello World")  -- "SGVsbG8gV29ybGQ="
```

### `base64decode(data: string): string`
Aliases: `crypt.base64decode`, `base64_decode`
```lua
local decoded = base64decode("SGVsbG8gV29ybGQ=")  -- "Hello World"
```

## LZ4 Compression

### `lz4compress(data: string): string`
Aliases: `crypt.lz4compress`. Compresses using LZ4 algorithm. Returns binary string.

### `lz4decompress(data: string): string`
Aliases: `crypt.lz4decompress`. Decompresses LZ4-compressed data.

```lua
local original = string.rep("hello world ", 1000)
local compressed = lz4compress(original)
local restored = lz4decompress(compressed)
print(#compressed, "vs", #original)  -- much smaller
```
