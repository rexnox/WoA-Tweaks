Windows Registry Editor Version 5.00

; === Cache & Kernel Tuning ===
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management]
"SecondLevelDataCache"=dword:00001C00
"LargeSystemCache"=dword:00000001
"DisablePagingExecutive"=dword:00000001
"IoPageLockLimit"=dword:00200000
"ClearPageFileAtShutdown"=dword:00000000
"NonPagedPoolQuota"=dword:00000000

; === PerformanceScheduler ===
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\PriorityControl]
"Win32PrioritySeparation"=dword:00000026

; === NTFS Tuning ===
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem]
"NtfsDisableLastAccessUpdate"=dword:00000001
"NtfsMemoryUsage"=dword:00000002

; === Netzwerk-Optimierung ===
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters]
"TcpTimedWaitDelay"=dword:0000001E
"MaxUserPort"=dword:0000FFFE
"Tcp1323Opts"=dword:00000001
"DefaultTTL"=dword:00000040
"EnablePMTUDiscovery"=dword:00000001
"EnableTCPA"=dword:00000000

; === DWM (UI-Effekte) ===
[HKEY_CURRENT_USER\Software\Microsoft\Windows\DWM]
"MaxQueuedBuffers"=dword:00000002
"EnableAeroPeek"=dword:00000000

; === Explorer-Optimierung ===
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced]
"DisableThumbnailCache"=dword:00000001
"IconsOnly"=dword:00000001
"TaskbarAnimations"=dword:00000000
"ListviewAlphaSelect"=dword:00000000
"ListviewShadow"=dword:00000000

; === Dienste deaktivieren ===
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SysMain]
"Start"=dword:00000004

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DiagTrack]
"Start"=dword:00000004
