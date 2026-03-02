# Crypt

Cryptographic functions for encryption, hashing, and random generation.

## Encryption

### `crypt.encrypt(data: string, key: string, iv?: string, mode?: string): (string, string)`
Encrypts `data` with `key`. Returns `(ciphertext, iv)`. Default mode: AES-CBC.

### `crypt.decrypt(data: string, key: string, iv: string, mode?: string): string`
Decrypts ciphertext. Must use the same key/iv/mode as encrypt.

```lua
local key = crypt.generatekey()
local cipher, iv = crypt.encrypt("secret", key)
local plain = crypt.decrypt(cipher, key, iv)
print(plain) -- "secret"
```

### `crypt.generatekey(): string`
Generates a random AES-compatible key.

### `crypt.generatebytes(count: number): string`
Generates `count` cryptographically random bytes.

## Hashing

### `crypt.hash(data: string, algorithm: string): string`
Supported algorithms: `"sha1"`, `"sha224"`, `"sha256"`, `"sha384"`, `"sha512"`, `"md5"`.
```lua
local hash = crypt.hash("hello", "sha256")
```

### `crypt.hmac(data: string, key: string, algorithm: string): string`
HMAC authentication tag using the given algorithm.
```lua
local tag = crypt.hmac("message", "secret_key", "sha256")
```

## Random

### `crypt.random(min: number, max: number): number`
Cryptographically secure random integer in `[min, max]`.

## Encoding (also in Encoding library)
- `crypt.base64encode(data)` / `base64encode(data)` — Base64 encode
- `crypt.base64decode(data)` / `base64decode(data)` — Base64 decode
- `crypt.lz4compress(data)` / `lz4compress(data)` — LZ4 compress
- `crypt.lz4decompress(data)` / `lz4decompress(data)` — LZ4 decompress
