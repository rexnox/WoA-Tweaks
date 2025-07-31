---

## 🖼️ DWM Tweaks for High Refresh Rate Devices (e.g. Hotdog / Vayu)

These settings are optimized for devices like the **Oneplus 7t Pro (Hotdog)** and **Xiaomi Poco X3 Pro (Vayu)** running at **90 Hz or higher**.  
They improve visual smoothness, reduce latency, and enhance DPI scaling.

**Registry Base:**  
`[HKEY_CURRENT_USER\Software\Microsoft\Windows\DWM]`

```
"MaxQueuedBuffers"=dword:00000003
```
Allows up to 3 buffered frames – ensures **smoother rendering** on high-refresh displays (60 Hz → 90 Hz+).  
✅ Especially helpful on devices with fast OLED panels and touch UI.

```
"UseDpiScaling"=dword:00000001
```
Enables DPI-aware scaling in DWM – provides **sharper visuals and better layout** on high-DPI screens.

```
"EnableAeroPeek"=dword:00000000
```
Disables Aero Peek – minor visual effect that can **slightly improve responsiveness**.

---
