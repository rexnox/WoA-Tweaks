⚙️ Windows Registry Tweaks für Performance & Optimierung
Diese Registry-Datei wurde speziell für Windows-Systeme mit ARM- oder schwächerer x86-Hardware angepasst – etwa Geräte mit wenig RAM, schwächerem Storage oder optimierungsfreudigen Bastlern. Ziel: mehr Direktzugriff, weniger Overhead, bessere Reaktionszeiten.

🔧 Cache & Kernel Tuning
reg
Kopieren
Bearbeiten
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management]
"SecondLevelDataCache"=dword:00001C00
Stellt die L2-Cache-Größe manuell auf 1.8 MB (1C00h = 7168 KB). Gilt nur, wenn Windows die CPU-Cache-Größe nicht korrekt erkennt – bei modernen CPUs oft ignoriert, aber bei älteren oder exotischen Systemen (z. B. Snapdragon SoCs) manchmal relevant.

reg
Kopieren
Bearbeiten
"LargeSystemCache"=dword:00000001
Aktiviert den Systemcache-Modus, in dem Windows mehr RAM für Systemprozesse statt für Benutzeranwendungen priorisiert – sinnvoll auf Geräten mit schneller SSD und RAM > 4 GB.

r
Kopieren
Bearbeiten
"DisablePagingExecutive"=dword:00000001
Verhindert, dass Kernel-Treiber und -Komponenten in die Auslagerungsdatei verschoben werden. Halten diese im RAM → schnellerer Systemzugriff (mehr RAM vorausgesetzt).

reg
Kopieren
Bearbeiten
"IoPageLockLimit"=dword:00200000
Erlaubt dem Kernel, 2 MB für I/O-Operationen zu reservieren – z. B. für USB- oder Netzwerk-Datenströme. Gerade bei RNDIS/USB-C-Adapter kann das Spikes glätten.

r
Kopieren
Bearbeiten
"ClearPageFileAtShutdown"=dword:00000000
Deaktiviert das Löschen der Auslagerungsdatei beim Herunterfahren – beschleunigt das Shutdown, sicherheitsrelevant nur bei sensiblen Systemen.

reg
Kopieren
Bearbeiten
"NonPagedPoolQuota"=dword:00000000
Lässt Windows den NonPaged Pool (RAM-Bereich für kritische Prozesse) automatisch verwalten – empfohlen.

⏱ PerformanceScheduler
reg
Kopieren
Bearbeiten
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\PriorityControl]
"Win32PrioritySeparation"=dword:00000026
Justiert die Balance zwischen Reaktionszeit (foreground) und Durchsatz (background). 0x26 = optimiert für schnelle UI-Reaktion, ideal für Desktop-Nutzung oder Touch-Systeme.

💾 NTFS-Tuning (für SSDs)
reg
Kopieren
Bearbeiten
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem]
"NtfsDisableLastAccessUpdate"=dword:00000001
Deaktiviert das Speichern des letzten Zugriffszeitpunkts auf Dateien. Spart Schreibzyklen – empfehlenswert für SSDs.

reg
Kopieren
Bearbeiten
"NtfsMemoryUsage"=dword:00000002
Erhöht den NTFS-Cache, was Dateioperationen beschleunigt – bei viel RAM sinnvoll.

🌐 Netzwerk-Tweaks (für USB-Ethernet & RNDIS)
reg
Kopieren
Bearbeiten
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters]
"TcpTimedWaitDelay"=dword:0000001E
Verkürzt die Wartezeit für alte TCP-Verbindungen auf 30 Sekunden – reduziert Port-Blockaden bei schnellen Verbindungswechseln.

reg
Kopieren
Bearbeiten
"MaxUserPort"=dword:0000FFFE
Hebt die höchste nutzbare Portnummer auf 65534 an – mehr gleichzeitige Verbindungen möglich, z. B. bei P2P, Servern oder Web-APIs.

r
Kopieren
Bearbeiten
"Tcp1323Opts"=dword:00000001
Aktiviert TCP-Zeitstempel (RFC 1323), was Paketverluste besser erkennt. Vorsicht bei alten Geräten oder Routern.

reg
Kopieren
Bearbeiten
"DefaultTTL"=dword:00000040
Setzt die Time-to-Live für IP-Pakete auf 64 – Standardwert, der bei Routing-Problemen oder speziellen Netzwerken nützlich sein kann.

reg
Kopieren
Bearbeiten
"EnablePMTUDiscovery"=dword:00000001
Erlaubt Windows, optimale Paketgrößen (MTU) selbst zu erkennen – erhöht Effizienz.

reg
Kopieren
Bearbeiten
"EnableTCPA"=dword:00000000
Deaktiviert TCP-Autotuning – sinnvoll, wenn Probleme mit USB-LAN-Adaptern oder aggressiver Firewalls auftreten.

🖼 DWM-Tweaks (FrameBuffer & UI-Performance)
reg
Kopieren
Bearbeiten
[HKEY_CURRENT_USER\Software\Microsoft\Windows\DWM]
"MaxQueuedBuffers"=dword:00000002
Begrenzt die Anzahl gepufferter Frames auf 2 – reduziert Latenz, ideal für niedrige FPS-Geräte oder Touchscreens.

reg
Kopieren
Bearbeiten
"EnableAeroPeek"=dword:00000000
Deaktiviert Aero Peek – kleine Visual-Spielerei, spart minimale Ressourcen.

🗂 Explorer-Optimierung
reg
Kopieren
Bearbeiten
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced]
"DisableThumbnailCache"=dword:00000001
Verzichtet auf Miniaturansichten-Cache → schnelleres Browsen, vor allem auf schwachen Geräten mit vielen Dateien.

reg
Kopieren
Bearbeiten
"IconsOnly"=dword:00000001
Zeigt nur Symbole statt Miniaturbildern – reduziert RAM/CPU.

reg
Kopieren
Bearbeiten
"TaskbarAnimations"=dword:00000000
"ListviewAlphaSelect"=dword:00000000
"ListviewShadow"=dword:00000000
Alle Animationen & Effekte in Datei-Explorer und Taskleiste werden deaktiviert → spürbar flüssiger auf leistungsschwacher Hardware.

🛑 Dienste drosseln
reg
Kopieren
Bearbeiten
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SysMain]
"Start"=dword:00000004
Deaktiviert Superfetch/SysMain – auf SSDs oder Systemen mit ausreichend RAM meist eher störend als nützlich.

r
Kopieren
Bearbeiten
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DiagTrack]
"Start"=dword:00000004
Stoppt Diagnosedaten-Tracking („Connected User Experiences“) – bringt Datenschutz und spart RAM/CPU.

📝 Hinweis
Diese Einstellungen sind nicht für alle Nutzer sinnvoll. Wer z. B. viele Hintergrunddienste nutzt oder auf maximale Kompatibilität mit Unternehmensnetzwerken angewiesen ist, sollte einzelne Tweaks mit Bedacht anwenden.

✅ Empfehlung: Sicherung & Rücksetzpunkt
Bevor du die .reg-Datei einspielst:

Erstelle einen Wiederherstellungspunkt

Exportiere ggf. einzelne Registry-Zweige vorab als Backup

Reboot nach Anwendung, um Effekte zu sehen

