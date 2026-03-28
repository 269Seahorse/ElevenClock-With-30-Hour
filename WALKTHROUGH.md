# ElevenClock 30-Hour Clock Mod

## What Was Done

Patched ElevenClock's `tools.py` to display a **30-hour clock** — after midnight (00:00–05:59), the clock shows 24:00–29:59 instead of resetting to 0.

### Modified File
- [`elevenclock/tools.py`](file:///C:/Users/Seahorse/Documents/ElevenClock/elevenclock/tools.py) — Added `apply_30hour_format()` function

### How It Works
The `apply_30hour_format()` function is called at the end of `getClockText()`. When the current hour is 0–5 (midnight to 5:59 AM), it:
1. Detects hour numbers in the formatted time string
2. Adds 24 to them (e.g., `01:53` → `25:53`)
3. Preserves all other formatting (date, AM/PM markers, seconds, etc.)

### Build & Install
1. Rebuilt `ElevenClock.exe` from modified source using PyInstaller
2. Backed up original exe as `elevenclock.exe.bak`
3. Replaced installed exe at `AppData\Local\Programs\ElevenClock\`

### Persistence
✅ **Survives reboots** — the installed exe itself is patched

### Reverting
To restore the original clock:
```powershell
Stop-Process -Name "elevenclock" -Force
cd "$env:LOCALAPPDATA\Programs\ElevenClock"
Copy-Item "elevenclock.exe.bak" "elevenclock.exe" -Force
Start-Process "elevenclock.exe"
```

> [!NOTE]
> If ElevenClock auto-updates, you'll need to re-patch. Consider disabling auto-updates in ElevenClock settings.
