<div align="center">

# antigravity-autorun-fix

**Fixes the "Always Proceed" terminal policy in [Antigravity IDE](https://antigravity.dev) — so it actually works.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Antigravity](https://img.shields.io/badge/Antigravity-v1.107.0+-blue.svg)](https://antigravity.dev)
[![Works on](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)]()

*One command. Restart. Done.*

</div>

---

## The Problem

You go to **Settings → Agent → Terminal Execution → "Always Proceed"**.  
You turn it on.  
Antigravity **still asks you to click "Run All" on every single command.**

The setting saves. The dropdown shows the right value. It just **does nothing**.

---

## The Fix

```bash
node patch.js
```

Then restart Antigravity. That's it. No more clicking.

---

## What It Does

Antigravity's source has an `onChange` handler that fires when you *manually switch* the dropdown on a step — but **no `useEffect`** to check the saved policy when a new step mounts.

This fix injects the missing `useEffect`:

```js
// WHAT WAS MISSING — fires on every new step mount:
useEffect(() => {
    if (policy === EAGER && !secureMode) confirm(true)
}, [])
```

It uses **regex pattern matching** to locate the correct code, so it works regardless of how variables are minified — and across different Antigravity versions.

---

## Usage

```bash
# Apply the fix
node patch.js

# Check if it's applied
node patch.js --check

# Revert to original
node patch.js --revert

# Custom install location
node patch.js --path "D:\Antigravity"
```

**Auto-detect** finds Antigravity through: current directory → PATH → Windows Registry → default install locations.

---

## What Gets Patched

| File | Location |
|------|----------|
| `workbench` | `resources/app/out/vs/workbench/workbench.desktop.main.js` |
| `jetskiAgent` | `resources/app/out/jetskiAgent/main.js` |

**Both files are backed up** as `.bak` before any changes. Fully reversible.

---

## Example Output

```
╔══════════════════════════════════════════════════╗
║  Antigravity "Always Proceed" Auto-Run Fix       ║
║  github.com/Noor881/antigravity-autorun-fix      ║
╚══════════════════════════════════════════════════╝

📍 C:\Users\you\AppData\Local\Programs\Antigravity
📦 Version: 1.107.0 (IDE 1.20.5)

  📋 [workbench] Found onChange at offset 12362782
     callback=Mt, enum=Dhe, confirm=b
     policyVar=u, secureVar=d
     useEffect=mn (confidence: 30 hits)
  ✅ [workbench] Patched (+43 bytes)

  📋 [jetskiAgent] Found onChange at offset 8388797
     callback=ve, enum=rx, confirm=F
     policyVar=d, secureVar=f
     useEffect=At (confidence: 55 hits)
  ✅ [jetskiAgent] Patched (+42 bytes)

✨ Done! Restart Antigravity.
```

---

## Safety

- ✅ **Automatic backups** — originals saved as `.bak` before patching
- ✅ **One-command revert** — `node patch.js --revert`
- ✅ **Non-destructive** — only adds code, never removes anything
- ✅ **Version-resilient** — structural regex matching, not hardcoded names

---

## Requirements

- [Node.js](https://nodejs.org) (any modern version)
- Antigravity IDE v1.107.0+ (other versions likely work too)

---

## Credits

> Original bug discovery and initial patch concept by **[Kanezal](https://github.com/Kanezal/better-antigravity)** via the `better-antigravity` npm package.  
> This repo is a cleaner, standalone version — no npm install required, just `node patch.js`.  
> Full credit to Kanezal for finding the root cause and writing the core patcher logic.

---

## License

[MIT](LICENSE)
