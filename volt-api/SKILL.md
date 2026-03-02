---
name: volt-api
description: Complete reference and coding assistant for the Volt.bz Roblox executor scripting API. Use when writing, debugging, or explaining Volt executor scripts that use any Volt-specific globals such as hookfunction, hookmetamethod, Drawing, DrawingImmediate, request, getgenv, getrenv, filtergc, loadstring, saveinstance, WebSocket, crypt, debug library extensions, filesystem functions, signals, actors, closures, metatable manipulation, reflection, console, input simulation, cache manipulation, or any other Volt API. Triggers on any Volt scripting task.
---

# Volt API Skill

Volt is a Roblox script executor. Its environment extends standard Luau with many privileged globals. Docs: https://docs.volt.bz/docs

## Reference Files

Load the relevant file(s) when working in a specific domain. All files are one level from this SKILL.md.

| File | When to load |
|---|---|
| `references/actors.md` | Parallel Luau, actors, run_on_actor, comm channels, LuaStateProxy |
| `references/cache.md` | Instance cache manipulation |
| `references/closures.md` | hookfunction, hookmetamethod, newcclosure, clonefunction, etc. |
| `references/console.md` | rconsole* functions for custom debug console |
| `references/crypt.md` | Encryption, hashing, HMAC, random bytes |
| `references/debug.md` | debug.* library extensions (constants, upvalues, protos, stack) |
| `references/drawing.md` | Persistent screen-overlay Drawing objects |
| `references/drawingimmediate.md` | Per-frame immediate-mode screen drawing |
| `references/encoding.md` | base64encode/decode, lz4compress/decompress |
| `references/environment.md` | getgenv, getrenv, getreg, getgc, filtergc, gettenv |
| `references/filesystem.md` | readfile, writefile, appendfile, listfiles, makefolder, etc. |
| `references/input.md` | keypress, keyclick, mouse1click, mousemoveabs, etc. |
| `references/instances.md` | cloneref, fireclickdetector, gethui, getinstances, etc. |
| `references/metatable.md` | getrawmetatable, makewritable, setnamecallmethod, etc. |
| `references/miscellaneous.md` | request, saveinstance, queueonteleport, setclipboard, setfflag, etc. |
| `references/oth.md` | oth.hook / oth.unhook — thread-safe C function hooking |
| `references/reflection.md` | gethiddenproperty, setthreadidentity, isnetworkowner, etc. |
| `references/scripts.md` | getscripts, getsenv, loadstring, getscriptclosure, etc. |
| `references/signals.md` | firesignal, getconnections, replicatesignal |
| `references/voltsignal.md` | VoltSignal custom event class |
| `references/websocket.md` | WebSocket.connect, Send, OnMessage, OnClose |

## Key Volt Concepts

- **Thread identity**: Volt scripts run at identity 8 (maximum). Use `getthreadidentity()` / `setthreadidentity(level)` to read/change.
- **Global env**: `getgenv()` returns Volt's global environment (shared across executions). `getrenv()` returns the game's env.
- **Workspace folder**: All filesystem paths are relative to Volt's sandboxed workspace folder.
- **sUNC standard**: Most function names follow the sUNC (senS' Unified Naming Convention) — many have aliases (e.g. `hookfunction` = `replaceclosure`).
- **Drawing vs DrawingImmediate**: `Drawing.new()` creates persistent objects; `DrawingImmediate` draws per-frame inside a `GetPaint` event callback.
- **oth vs hookfunction**: `oth.hook` runs the hook callback on a separate thread (safer for C functions); `hookfunction` runs inline.
