> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [4.0.0] `THE FINAL END`
>
> - Changed the module banner and added a new function `action.sh`
> - Renamed `SD.sh` to `QCOM.sh` for clearer and more accurate Qualcomm platform identification.
> - Maintained full functional compatibility with previous Snapdragon-specific optimizations.
> - Enhanced readability and maintainability by aligning naming conventions across SoC scripts.
> - Refactored and significantly expanded Mediatek-specific thermal and performance optimizations.
> - Improved termination of Mediatek thermal daemons, services, and monitoring processes.
> - Added extensive control over MTK thermal modules, DVFS, PPM, PBM, HPS, and core control mechanisms.
> - Enhanced CPU and GPU performance locking by forcing maximum frequencies and performance governors.
> - Extended thermal trip point adjustments to prevent premature throttling.
> - Implemented additional kernel and proc-level overrides for MTK power and thermal management.
> - Improved stability by excluding critical system and radio-related processes from termination.
> - Reworked execution flow for better reliability and maintainability compared to previous versions.
> - Significantly improved module security and integrity enforcement.
> - Enhanced compatibility across multiple root solutions and Android versions.
> - Increased runtime stability with better process and state management.
> - Delivered cleaner installation and uninstallation workflows.
> - Improved transparency through richer metadata and user-facing notifications.
> - Refactored service execution with PID-based process management.
> - Prevented duplicate background service instances across reboots.
> - Appended runtime status and active PID to module version string.
> - Added runtime notifications to confirm successful optimization activation.
> - Improved overall service stability and lifecycle handling.
> - Refactored uninstall logic into clear, modular functions.
> - Improved cache cleanup coverage, including app cache, shader cache, and system cache directories.
> - Ensured safe and deterministic execution using strict error handling.
> - Removed residual temporary files and runtime artifacts.
> - Enhanced reliability and maintainability of the uninstallation process.
---

> [3.0.0] `FINAL`
>
> - customize.sh: Overhauled root detection to support all Magisk variants (Stable/Canary/Kitsune/Alpha), KernelSU (Standard/Next/SukiSU Ultra), and APatch with persistent method tracking and version details.
> - Added formatted timestamp, enhanced device info display with capitalized model, root-specific icons, and streamlined SOC-based file cleanup (SD/MTK).
> - Refined module verification, introduced random devil-themed messages, and optimized post-install actions with Telegram link and reboot notification.
> - service.sh: Rewrote root detection to read persistent method files (.method) from Magisk/KernelSU/APatch, added precise version extraction, and introduced per-SOC script execution with PID tracking.
> - Enhanced module.prop with dynamic FINAL build tag, PID indicator, detailed thermal description, and Android version emoji mapping (Q to B).
> - Implemented immediate script launch without boot wait, added chipset-specific notifications with custom icons, and improved SOC detection robustness.
> - verify.sh: Enhanced verification with multi-algorithm hash fallback (SHA512/384/256/224/1), added TMPDIR fallback, auto-cleanup via trap, and detailed checksum mismatch reporting.
> - uninstall.sh: Streamlined cleanup by removing redundant legacy cache paths, added removal of KNTL*.png notification icons, and restructured into modular functions with set -e for reliability.
> - MTK.sh: Significantly expanded thermal mitigation bypass with new dedicated functions for PBM, DPT/DCT, thermal proc tweaks, CPU hard limits override, and enhanced core control disable.
> - Added extended core online forcing (cpu8-9 support), deeper HPS/PPM policy disabling, and comprehensive GPU throttling/power limit neutralization.
> - Greatly reinforced input/sched/boost disabling with additional paths (sched_boost, dynamic_boost, etc.) and improved governor locking via chattr +i.
> - Updated notification system to use KNTL-themed icons and tag, while maintaining full backward compatibility with existing Mediatek thermal daemon kill list.
> - SD.sh: Dramatically intensified thermal daemon/service extermination with new ctl.stop commands, system-wide binary discovery (/system/vendor/odm/product), and getprop-based thermal process targeting for total eradication.
> - Expanded aggressive final_kill routine and reinforced thermal sysfs lockdown with optimized permission loops for unbreakable protection.
> - Enhanced GPU throttling bypass with chattr +i immutability on throttling nodes and guaranteed performance governor/min_freq enforcement.
> - Upgraded notification system to full KNTL branding with custom icons (KNTL01/02.png) and dedicated tag, while wrapping all operations in robust main() structure.
---

> [1.5.0] `BETA`
>
> - Changes and updates to `verify.sh` to a better version than before.
> - More robust handling of module structure algorithm integration.
> - Update or change detection of architecture is easier and simpler.
> - Fixed inaccurate `SoC` detection in previous version (Don't know if it worked or not).
> - Removal of `(fast_charge)` feature in `Snapdragon`.
> - Fixed lost signal issue in `MTK` (I don't know if this fix solves it or not).
> - Added exception filters for critical processes (phone & system) in `MTK`
> - Expanded the list of thermal daemons including the latest HAL of Android 13/14 on `MTK`.
> - Still kills all thermal daemons aggressively but safely.
> - Restructured `MTK.sh` for improved readability and logical execution flow (MTK).
> - Fixed CPU core range in `mtk_force_online_cores` and `mtk_set_cpu_performance` to `cpu[0-7]` for compatibility with octa-core MTK devices (MTK).
> - Optimized `lock_thermal` with direct `find -exec` for efficiency (MTK).
> - Added file existence checks in `mtk_gpu_throttle_disable` to prevent errors on unsupported paths (MTK).
> - Removed redundant `mtk_disable_governor` function as its functionality is covered by `mtk_set_cpu_performance` (MTK).
> - Consolidated execution into a `main` function for centralized control and better debugging (MTK).
> - Maintained aggressive thermal daemon termination with safe exception filters for critical processes (MTK).
> - Organized uninstall.sh into functions (clean_cache, clean_system_dirs, remove_module, main) for better readability and maintainability.
> - Replaced rm -f with find -delete, added error suppression (2>/dev/null), and maintained set -e for robust execution.
---

> [1.0.0] `BETA`
>
> - Initial release.