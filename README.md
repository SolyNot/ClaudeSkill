# ClaudeSkill

A collection of skills for [Antigravity](https://antigravity.google) — Google's agentic AI coding assistant. Skills are structured reference packages that give the AI specific domain knowledge it doesn't have by default.

Think of them as onboarding docs written for an AI, not a human.

---

## What's in here

### `volt-api`

A full reference skill for the [Volt.bz](https://volt.bz) Roblox script executor API.

Volt extends standard Luau with a bunch of privileged globals — `hookfunction`, `Drawing`, `request`, `getgenv`, `firesignal`, `saveinstance`, and a lot more. These aren't in any Roblox docs, so without this skill, the AI constantly has to guess or look them up from scratch.

This skill covers every category from the [official Volt docs](https://docs.volt.bz/docs):

| Category | What it covers |
|---|---|
| Actors | Parallel Luau, `run_on_actor`, `LuaStateProxy`, comm channels |
| Cache | `cache.replace`, `cache.invalidate`, `cache.iscached` |
| Closures | `hookfunction`, `hookmetamethod`, `newcclosure`, `clonefunction` |
| Console | `rconsoleshow`, `rconsoleprint`, `rconsoleinput`, etc. |
| Crypt | AES encryption, SHA hashing, HMAC, random bytes |
| Debug | `debug.getconstants`, `getupvalues`, `getprotos`, `getstack` |
| Drawing | Persistent screen overlay objects (`Line`, `Circle`, `Text`, `Image`, etc.) |
| DrawingImmediate | Per-frame immediate-mode drawing via `GetPaint` event |
| Encoding | `base64encode/decode`, `lz4compress/decompress` |
| Environment | `getgenv`, `getrenv`, `getgc`, `filtergc`, `getreg` |
| Filesystem | `readfile`, `writefile`, `listfiles`, `makefolder`, etc. |
| Input | `keyclick`, `mouse1click`, `mousemoveabs`, `mousescroll` |
| Instances | `cloneref`, `fireclickdetector`, `gethui`, `getinstances` |
| Metatable | `getrawmetatable`, `makewritable`, `hookmetamethod` patterns |
| Miscellaneous | `request()`, `saveinstance`, `setfflag`, `setclipboard` |
| oth | Thread-safe C function hooking (`oth.hook` / `oth.unhook`) |
| Reflection | `gethiddenproperty`, `setthreadidentity`, `isnetworkowner` |
| Scripts | `getscripts`, `getsenv`, `loadstring`, `getscriptclosure` |
| Signals | `firesignal`, `getconnections`, `replicatesignal` |
| VoltSignal | Volt's custom event class |
| WebSocket | `WebSocket.connect`, `Send`, `OnMessage`, `OnClose` |

---

## How skills work

Antigravity loads skills in three stages:

1. The `description` field in `SKILL.md` frontmatter is always in context — this is what triggers the skill.
2. The body of `SKILL.md` loads when the skill is relevant to the current task.
3. Individual `references/*.md` files load on demand, only when that specific domain is needed.

So if you ask about `hookfunction`, it reads `SKILL.md` + `closures.md`. It doesn't load all 21 reference files at once.

---

## Limitations

- This skill covers the Volt API only. It doesn't add general Roblox scripting knowledge.
- Function signatures are based on the docs as of early March 2026. Volt updates frequently and the docs occasionally lag behind the actual implementation.
- Some functions have undocumented options or behavior that isn't captured here.
- The `Drawing` type-specific property lists may be incomplete — the official docs don't always enumerate every property per type.

---

## Adding more skills

Each skill is a folder with a `SKILL.md` and optional `references/`, `scripts/`, and `assets/` subdirectories. Drop a new folder in here and it works.

The `.skill` files are just zipped versions of the folder — you don't need them to use the skill, but Antigravity can install them directly.

---

## Source

Volt docs: [docs.volt.bz/docs](https://docs.volt.bz/docs)
