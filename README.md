# ASUS Splendid Wake Fix

A lightweight, automated background utility designed to fix the common issue where ASUS laptops lose their **ASUS Splendid** screen color calibration profile upon waking from sleep or unlocking the screen.

---

## The Problem
On many ASUS laptops (VivoBook, ZenBook, ROG, TUF), waking up from sleep or unlocking the screen causes the display colors to reset to a flat, uncalibrated state. In MyASUS, the Splendid mode (e.g. Normal) remains selected, forcing users to manually switch back and forth (e.g., *Normal -> Vivid -> Normal*) each time to restore color calibration.

## How This Tool Works
1. **Event-Driven:** Hooks into Windows Win32 power and session events (`PowerModes.Resume` and `SessionSwitchReason.SessionUnlock`).
2. **Safe Delay:** Waits 1.5–2 seconds after waking up to allow the display controller and GPU driver to finish reinitializing.
3. **Dynamic Mode Sync:** Reads your active MyASUS Splendid configuration (`*_my_sp_data.sys`) dynamically. Whichever mode you select in MyASUS (Normal, Vivid, Eye Care, etc.) is automatically preserved.
4. **Hardware LUT Re-apply:** Silently executes `AsusSplendid.exe` to re-upload the hardware Look-Up Table (LUT) to your GPU.
5. **Completely Silent:** Runs as a windowless background process (`winexe`) consuming **0% CPU** while idle and only ~20 MB of RAM.

---

## Installation
1. Download or extract the release files.
2. Double-click **`install.bat`**.
3. That's it! The utility will copy itself to `%LOCALAPPDATA%\ASUS_SplendidFix`, add itself to your startup programs (`HKCU\...\Run`), and start running immediately in the background.

## Uninstallation
To completely remove the utility at any time, simply double-click **`uninstall.bat`**.

---

## Compiling from Source
If you wish to build the executable yourself using the built-in Microsoft .NET Framework C# compiler:
```cmd
C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe /target:winexe /optimize+ /out:SplendidWakeFix.exe SplendidWakeFix.cs
```

---

## Compatibility
- Works on Windows 10 & Windows 11.
- Compatible with all ASUS laptops with ASUS System Control Interface v2/v3 and MyASUS.
- No administrator privileges required for installation or execution.
