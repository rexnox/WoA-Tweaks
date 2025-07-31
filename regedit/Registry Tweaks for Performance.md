# ⚙️ Windows Registry Tweaks for Performance & Optimization

This registry file is specifically tailored for Windows systems running on **ARM or lower-end x86 hardware** - such as devices with limited RAM, slower storage, or for tuning enthusiasts.  
The goal: **more direct memory access, lower overhead, faster response times.**

---

## 📁 Cache & Kernel Tuning

**Registry Base:**

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management`
```
"SecondLevelDataCache"=dword:00001C00
``` 
Manually sets the L2 cache size to **1.8 MB** (1C00h = 7168 KB). Often ignored on modern CPUs, but useful on older or exotic systems (e.g. Snapdragon SoCs) where Windows may not detect it correctly.

```
"LargeSystemCache"=dword:00000001
```  
Enables **System Cache Mode**, prioritizing RAM usage for system processes instead of user apps - recommended for systems with SSDs and >4 GB RAM.

```
"DisablePagingExecutive"=dword:00000001
```
Prevents kernel drivers from being paged to disk. Keeps them in RAM → faster system access (if enough RAM is available).

```
"IoPageLockLimit"=dword:00200000 
```
Allows the kernel to lock **2 MB** for I/O operations. Improves USB/network throughput, especially for RNDIS or USB-C.

```
"ClearPageFileAtShutdown"=dword:00000000
```
Disables clearing the page file at shutdown. Speeds up system shutdowns - only relevant in security-sensitive environments.

```
"NonPagedPoolQuota"=dword:00000000
```
Allows Windows to auto-manage the NonPaged Pool - safe and recommended setting.

---

## ⏱ Performance Scheduler

**Registry Base:**  
`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\PriorityControl`

```
"Win32PrioritySeparation"=dword:00000026
```
Adjusts scheduling balance between UI responsiveness and background processing.  
`0x26` favors fast user interface response - ideal for desktops and touch devices.

---

## 💾 NTFS Tuning (SSD-Optimized)

**Registry Base:**  
`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem`

```
"NtfsDisableLastAccessUpdate"=dword:00000001
```
Disables updating of "last accessed" timestamps - reduces write cycles, prolongs SSD lifespan.

```
"NtfsMemoryUsage"=dword:00000002
```
Increases the memory usage for NTFS caching - can improve file access speed on systems with more RAM.

---

## 🌐 Network Stack Tweaks (USB Ethernet & RNDIS)

**Registry Base:**  
`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`

```
"TcpTimedWaitDelay"=dword:0000001E
```
Reduces TIME_WAIT duration for closed TCP connections to 30 seconds - helpful for fast reconnects or limited port availability.

```
"MaxUserPort"=dword:0000FFFE
```
Increases the highest user port number to **65534** - allows more concurrent network connections.

```
"Tcp1323Opts"=dword:00000001
```
Enables TCP timestamp and window scaling (RFC 1323) - useful for high-latency connections. May cause issues on legacy routers.

```
"DefaultTTL"=dword:00000040
```
Sets packet TTL (Time To Live) to **64** - good default for most environments.

```
"EnablePMTUDiscovery"=dword:00000001
```
Lets Windows auto-detect optimal packet sizes (MTU) - increases efficiency and reduces fragmentation.

```
"EnableTCPA"=dword:00000000
```
Disables TCP auto-tuning - helps with stability on flaky USB adapters or limited embedded network stacks.

---

## 🖼 DWM (Desktop Window Manager) UI Tweaks

**Registry Base:**  
`HKEY_CURRENT_USER\Software\Microsoft\Windows\DWM`

```
"MaxQueuedBuffers"=dword:00000002
```
Limits buffered frames to 2 - reduces input latency, useful on low-FPS systems or touch interfaces.

```
"EnableAeroPeek"=dword:00000000
```
Disables Aero Peek - a visual effect that can be safely turned off for better responsiveness.

---

## 🗂 Explorer UI Performance

**Registry Base:**  
`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced`

```
"DisableThumbnailCache"=dword:00000001
```
Disables caching of image thumbnails - speeds up file browsing and reduces SSD wear.

```
"IconsOnly"=dword:00000001
```
Explorer will show only icons instead of thumbnails - saves RAM and CPU cycles.

```
"TaskbarAnimations"=dword:00000000
```
Disables taskbar animations - makes the taskbar more responsive.

```
"ListviewAlphaSelect"=dword:00000000
```
Turns off alpha blending when selecting list items - improves responsiveness.

```
"ListviewShadow"=dword:00000000
```
Removes drop shadows from selected items - minor improvement, but visually cleaner and snappier.

---

## 🛑 Disable Unnecessary Services

**Registry Base:**  
`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SysMain`

```
"Start"=dword:00000004
```
Disables **Superfetch/SysMain** - unnecessary on SSDs and can cause CPU usage spikes.

**Registry Base:**  
`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DiagTrack`

```
"Start"=dword:00000004
```
Disables **Connected User Experiences and Telemetry (DiagTrack)** - helps with privacy and reduces background activity.

---

## 📝 Notes & Recommendations

These tweaks aim for performance, not universal compatibility.  
Test them individually on production machines, and evaluate side effects before wide deployment.

---

## ✅ Before Applying

- 🔁 **Create a system restore point**
- 💾 **Backup** affected registry keys manually if needed
- 🔄 **Reboot** after importing to ensure all changes are active

---

## 📥 How to Use

1. Copy all registry entries from this README
2. Paste them into a `.reg` file (e.g. `win-tweaks.reg`)
3. Double-click the file or use:

   ```cmd
   reg import win-tweaks.reg
