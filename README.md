🚀 Performance Tweaks for Windows on ARM (WoA)

Running Windows on an ARM-based device like the Surface Pro X or a Snapdragon-powered laptop? Then you probably already know — with the right tweaks, you can squeeze out a lot more performance than what comes out of the box.

This guide shows you some practical optimizations to make your WoA setup noticeably faster and smoother — especially for devices based on Snapdragon 8cx, Hotdog, Vayu and similar platforms.
1. Native Vulkan Support (Important for Snapdragon 8cx users)

If you're using Windows 23H2 or earlier, you're likely missing the vulkan-1.dll file — which can cause apps like PPSSPP or other Vulkan-based emulators to fail.

To fix that, follow this guide to add native Vulkan support for Snapdragon 8cx:
👉 Enable Vulkan on Snapdragon 8cx

    ⚠️ If you're already running Windows 24H2 (Build 26100) or newer, you can safely skip this step — Vulkan support is already built in.

2. DWM Registry Tweaks — Unlock Better Visual Performance

The Desktop Window Manager (DWM) can become a bottleneck on ARM devices. With a few smart Registry edits, you can improve system responsiveness and reduce unnecessary visual overhead.

👉 Check out the DWM performance tweaks here:
🔧 DWM Tweaks for WoA

These tweaks are especially useful for low-power ARM devices, helping reduce system lag and visual stutter during multitasking or UI transitions.
3. Extra Registry Tweaks for High Refresh Rate Displays

If your device supports 90Hz or 120Hz refresh rates, this set of registry tweaks helps you take full advantage of that smoother display experience.

📈 Performance Tweaks for High Refresh Rate Devices

They help ensure your system doesn't lock itself to 60Hz and make animations and scrolling feel a lot more fluid.
4. bcdedit Optimizations — Boost CPU Responsiveness

Last but not least:
Using bcdedit, you can modify system boot and CPU-related behavior. Personally, I noticed a performance improvement when enabling CPU time tracking — it might not work the same on every device, but it's worth trying.

🧩 bcdedit Tweak Guide

    🧠 Note: Results may vary depending on your specific device and use case — test and tweak to see what works best for you.

Final Thoughts — Small Tweaks, Big Gains

Windows on ARM has huge potential — and these simple tweaks can go a long way toward making your device feel snappier, smoother, and more responsive.

Whether you're gaming, emulating, or just browsing, every bit of performance matters. Try these out and feel the difference.

Got feedback, questions, or your own tweaks to share?
Open an issue or send a pull request — contributions are always welcome!

Happy tweaking 💻⚡

🔗 Repo: WoA-Tweaks by rexnox
