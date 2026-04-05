<div align="center">

# 🚀 antigravity-autorun-fix

**Fixes the "Always Proceed" terminal policy in [Antigravity IDE](https://antigravity.dev) — so it actually auto-runs commands.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Antigravity](https://img.shields.io/badge/Antigravity-v1.107.0+-blue.svg)](https://antigravity.dev)
[![Works on](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)]()
[![Node.js](https://img.shields.io/badge/Node.js-Any%20Modern%20Version-green)](https://nodejs.org)

*One command. Restart. Done. No coding skills needed.*

</div>

---

## 📖 Table of Contents

- [What is the Problem?](#-what-is-the-problem)
- [What Does This Fix Do?](#-what-does-this-fix-do)
- [Before You Start — Requirements](#-before-you-start--requirements)
- [Step-by-Step Installation Guide](#-step-by-step-installation-guide)
  - [Windows](#windows)
  - [macOS](#macos)
  - [Linux](#linux)
- [How to Undo the Fix](#-how-to-undo-the-fix)
- [How to Check If It's Working](#-how-to-check-if-its-working)
- [Troubleshooting](#-troubleshooting)
- [How It Works (Technical)](#-how-it-works-technical)
- [FAQ](#-faq)
- [Credits](#-credits)

---

## ❓ What is the Problem?

When you use **Antigravity IDE**, it has a setting called **"Always Proceed"** under:

> **Settings → Agent → Terminal Execution → "Always Proceed"**

What this setting is *supposed* to do:
> Every time the AI wants to run a terminal command, it should just **run it automatically** without asking you to click anything.

What actually happens **without this fix**:
> Even with "Always Proceed" turned on, Antigravity **still shows a "Run All" button** and **waits for you to click it manually** on every single command.

The setting appears to save. The dropdown shows the correct value. But **it does absolutely nothing**. Every command still requires a manual click to proceed.

---

## 🔧 What Does This Fix Do?

This is a **one-time patch** that edits two JavaScript files inside your Antigravity installation to add the missing piece of code.

The fix is **safe**, **reversible**, and **non-destructive**:
- ✅ It **automatically creates backups** of the original files before changing anything
- ✅ You can **undo it instantly** with a single command
- ✅ It only **adds** a few bytes of code — it never removes anything
- ✅ It uses **smart pattern matching** so it works across different Antigravity versions

---

## ✅ Before You Start — Requirements

You need **two things** installed on your computer:

### 1. Antigravity IDE
- Download from [antigravity.dev](https://antigravity.dev)
- Version 1.107.0 or newer (other versions likely work too)

### 2. Node.js
- Download from [nodejs.org](https://nodejs.org)
- Click the big green **"LTS"** button (recommended version)
- Install it like any normal program (Next → Next → Finish)
- Any modern version works — v16, v18, v20, etc.

**How to check if Node.js is already installed:**

Open a terminal (Command Prompt / PowerShell on Windows, Terminal on Mac/Linux) and type:
```
node --version
```
If it shows something like `v20.11.0`, you're good. If it says "command not found", install Node.js first.

---

## 📋 Step-by-Step Installation Guide

### Step 1 — Download this fix

**Option A: Using Git (if you have it)**
```bash
git clone https://github.com/Noor881/antigravity-autorun-fix.git
cd antigravity-autorun-fix
```

**Option B: Download ZIP (no Git needed)**
1. Click the green **"Code"** button at the top of this page
2. Click **"Download ZIP"**
3. Extract the ZIP file somewhere easy to find (like your Desktop)
4. Open a terminal and navigate into the extracted folder

---

### Windows

**Opening a terminal in the right folder:**
1. Open the folder where you extracted/cloned this fix in File Explorer
2. Click on the address bar at the top (where it shows the folder path)
3. Type `powershell` and press Enter — this opens PowerShell in that folder

**Running the fix:**
```powershell
node patch.js
```

You should see output like this:
```
╔══════════════════════════════════════════════════╗
║  Antigravity "Always Proceed" Auto-Run Fix       ║
║  github.com/Noor881/antigravity-autorun-fix      ║
╚══════════════════════════════════════════════════╝

📍 C:\Users\YourName\AppData\Local\Programs\Antigravity
📦 Version: 1.107.0 (IDE 1.21.9)

  📋 [workbench] Found onChange at offset 12460103
     callback=tt, enum=YD, confirm=E
     policyVar=d, secureVar=h
     useEffect=pi (confidence: 70 hits)
  ✅ [workbench] Patched (+42 bytes)

  📋 [jetskiAgent] Found onChange at offset 8510660
     [similar output...]
  ✅ [jetskiAgent] Patched (+42 bytes)

✨ Done! Restart Antigravity.
💡 Run with --revert to undo.
⚠️  Re-run after Antigravity updates.
```

**Final step:** Close and reopen Antigravity IDE. The "Always Proceed" setting will now work correctly.

---

### macOS

1. Open **Terminal** (press `Cmd + Space`, type "Terminal", press Enter)
2. Navigate to the folder:
   ```bash
   cd ~/Downloads/antigravity-autorun-fix
   ```
   *(adjust the path to wherever you put the folder)*
3. Run the fix:
   ```bash
   node patch.js
   ```
4. Restart Antigravity.

---

### Linux

1. Open a terminal
2. Navigate to the folder:
   ```bash
   cd ~/antigravity-autorun-fix
   ```
3. Run the fix:
   ```bash
   node patch.js
   ```
4. Restart Antigravity.

---

## ↩️ How to Undo the Fix

Changed your mind? Want to go back to the original files? One command:

```bash
node patch.js --revert
```

This restores the original files from the backups that were created automatically. Then restart Antigravity.

---

## 🔍 How to Check If It's Working

**Before applying the fix:**
```bash
node patch.js --check
```
Shows: `⬜ [workbench] NOT PATCHED (patchable)` — means the fix can be applied.

**After applying the fix:**
```bash
node patch.js --check
```
Shows: `✅ [workbench] PATCHED (backup exists)` — means everything is working.

---

## 🗂️ All Available Commands

| Command | What it does |
|---------|-------------|
| `node patch.js` | Apply the fix |
| `node patch.js --check` | Check if the fix is applied or not |
| `node patch.js --revert` | Undo the fix and restore original files |
| `node patch.js --path "C:\My\Antigravity"` | Manually specify where Antigravity is installed |

---

## 🔎 Troubleshooting

### ❌ "Antigravity installation not found!"

The script couldn't find where Antigravity is installed. Tell it manually:

**Windows:**
```powershell
node patch.js --path "C:\Users\YourName\AppData\Local\Programs\Antigravity"
```

**macOS:**
```bash
node patch.js --path "/Applications/Antigravity.app/Contents/Resources"
```

**Linux:**
```bash
node patch.js --path "/usr/share/antigravity"
```

*To find the correct path on Windows: right-click the Antigravity shortcut on your desktop → Properties → look at "Start in" or "Target".*

---

### ❌ "'node' is not recognized as a command"

Node.js is not installed or not in your PATH.
1. Go to [nodejs.org](https://nodejs.org) and download the LTS version
2. Run the installer
3. **Restart your terminal** after installation
4. Try again

---

### ⚠️ "Some patches failed. Check output above."

One of the two files couldn't be patched. This usually means:
- You have an unusual Antigravity version with a different code structure
- Please [open an issue](https://github.com/Noor881/antigravity-autorun-fix/issues) and paste the full output — it will be fixed quickly.

---

### ⚠️ "Fix stopped working after Antigravity updated"

This is expected! When Antigravity updates itself, it overwrites the patched files with fresh originals. Simply re-run:
```bash
node patch.js
```

---

### ❌ "Permission denied" / "Access is denied"

On Windows, try running PowerShell **as Administrator**:
1. Press `Win + S`, type "PowerShell"
2. Right-click → **"Run as administrator"**
3. Navigate to the folder and run `node patch.js`

---

## ⚙️ How It Works (Technical)

Antigravity's UI contains a React component that renders a "Run command" step. Inside it:

1. There's an `onChange` handler that fires when you **manually** click the dropdown and change the policy — this calls `confirm(true)` when you switch to `EAGER` (Always Proceed).

2. But there's **no `useEffect`** that checks the saved policy when a **new step mounts**. So when the AI generates a new command step, the component mounts, reads the saved `EAGER` policy... and then does nothing with it.

This fix injects the missing `useEffect`:

```js
// What was missing — fires on every new step mount:
useEffect(() => {
    if (policy === EAGER && !secureMode) confirm(true)
}, [])
```

Because Antigravity's source is **minified** (variable names are scrambled), this script uses **regex pattern matching** to find the correct code structure regardless of what the variables are named. This makes it work across versions.

### Files patched

| Internal Label | File Location |
|----------------|--------------|
| `workbench` | `resources/app/out/vs/workbench/workbench.desktop.main.js` |
| `jetskiAgent` | `resources/app/out/jetskiAgent/main.js` |

Both files receive a backup (`.bak` extension) before any changes are made.

---

## ❓ FAQ

**Q: Is this safe?**
Yes. It only adds ~42 bytes of code. Backups are created automatically. You can revert any time.

**Q: Will it break anything?**
No. The injected `useEffect` only calls `confirm(true)` when the policy is already set to "Always Proceed" AND secure mode is off. It changes no other behavior.

**Q: Do I need to be a developer to use this?**
No. Just install Node.js, download this repo, and run one command.

**Q: What if Antigravity updates?**
The patch gets overwritten. Re-run `node patch.js` after any Antigravity update.

**Q: Does this work on older Antigravity versions?**
It's tested on v1.107.0 (IDE 1.21.9+). Older versions likely work too since the pattern matching is flexible.

**Q: Can I use this fix in a script to automate patching after updates?**
Absolutely. `node patch.js` is fully non-interactive and exits with code `0` on success.

---

## 🙏 Credits

> Original bug discovery and initial patch concept by **[Kanezal](https://github.com/Kanezal/better-antigravity)** via the `better-antigravity` npm package.
> This repo is a cleaner, standalone version — no npm install required, just `node patch.js`.
> Full credit to Kanezal for finding the root cause and writing the core patcher logic.
>
> Regex fix for Antigravity IDE v1.21.9+ (optional chaining support) by **[Noor](https://github.com/Noor881)**.

---

## 📄 License

[MIT](LICENSE) — do whatever you want with this.
