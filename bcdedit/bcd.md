---

## 🔧 Optional: Bootloader & Timer Optimizations (bcdedit)

The following `bcdedit` commands adjust low-level system behavior for better **timing precision**, **boot performance**, and **compatibility** - especially useful on custom hardware (e.g. ARM devices or non-standard UEFI setups).

---

### 🕰 Platform Clock Activation

cmd
```
bcdedit /set useplatformclock true
```
Forces Windows to use the hardware platform timer (HPET or equivalent) instead of other timer sources (like TSC or ACPI timers).
✅ May improve timing accuracy and stability, especially on systems with jittery clocks (e.g. emulated/virtualized or ARM SoCs).
⚠️ Can slightly increase power usage or DPC latency in rare cases.

🔇 Disable Dynamic Tick
```
bcdedit /set disabledynamictick yes
```
Disables Dynamic Ticks, which normally allow the system timer to pause when idle.
✅ Improves responsiveness and timer precision, especially useful for real-time tasks or media processing.
⚠️ Can slightly increase background CPU usage - not critical on modern systems.

🔁 Enhanced TSC Synchronization
```
bcdedit /set tscsyncpolicy Enhanced
```
Forces Windows to use the Enhanced TSC Sync Policy, improving how it synchronizes Time Stamp Counters (TSCs) across CPU cores.
✅ Reduces drift or desync between cores - important on multi-core or ARM devices with irregular timing behavior.
📌 This setting is especially recommended for ARM64 platforms running Windows via hacks or dual-boot.

🧭 Optional: Legacy Boot Menu
```
bcdedit /set bootmenupolicy legacy
```
Enables the classic text-based Windows Boot Manager instead of the newer graphical one.
✅ Useful if you experience display issues during boot (e.g. no image until login), or want easier access to Safe Mode via F8.
💡 Optional - only set if needed.

⏸ Add a Pause (for scripts)
cmd
```
pause
```
Holds the command window open after execution - helpful in .bat files so you can see the result before the window closes.
