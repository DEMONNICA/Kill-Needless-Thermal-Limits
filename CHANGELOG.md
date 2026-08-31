> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [6.6.6]
>
> - Added a periodic re-enforcement loop to `MTK`, `QCOM`, and `UNIV` — re-runs daemon termination every 60 seconds to catch thermal services that spawn after the initial run.
> - Added `VortexSU` and `ReSukiSU` to `detect_root_all()` KernelSU variant detection in `customize.sh`.
> - Added `Kokoro Mask` and `WeaveMask` to Magisk variant detection in `customize.sh`.
> - Added `FolkLite` to APatch variant detection in `customize.sh`.
> - Added `aapt`-based spoofed variant fallback to `detect_root_all()` in `customize.sh`, checked before the generic `ksud` fallback.
> - Added `UNIV` as a fallback thermal-override target in `customize.sh` for SoCs other than Snapdragon and Mediatek.
> - Added new chipset entries to `socs.json`.
> - Added a `sys.boot_completed` wait loop to `service.sh` before running the main thermal-override logic.
> - Added `UNIV` to the thermal-override script loop in `service.sh`, with `SOC_NAME` fallback to `Unknown`.
> - Added `restrict_temp_nodes()` — locks temperature nodes under `/sys/devices` via `chmod 000`, except the standard `thermal_zone` path (credit: [@HoyoSlave](https://t.me/HoyoSlave)).
> - Added `boottime` property handling to `modify_thermal_properties()` in `MTK` — resets to empty, checked before `disable`.
> - Added `MODDIR="$1"` to `MTK` for consistency with the `MODDIR`-as-argument convention.
> - Added `MODDIR="$1"` to `QCOM` for consistency with the `MODDIR`-as-argument convention.
> - Added `boottime` property handling to `modify_thermal_properties()` in `QCOM` — resets to empty, checked before `disable`.
> - Added `backup_val()` to `action.sh`, `MTK`, and `QCOM` — backs up the original sysfs value or property before the first overwrite, saved to `$MODDIR/backup`.
> - Added a `MODDIR` fallback to `action.sh` — uses the manager-exported value, falling back to a scan by `id` and `author`.
> - Added restore logic to `uninstall.sh` — reads `$MODDIR/backup` and writes every original sysfs value and property back before the module directory is removed.
> - Added `MODDIR` resolution and `backup_val()` to `post-fs-data.sh` — original trip point values are now backed up before being overwritten.
> - Added thermal-node permission restoration to `uninstall.sh` — `chmod 644` on `/sys/devices/virtual/thermal` files and `chmod +r` on `/sys/devices` `temp` nodes.
> - Changed license from GNU General Public License to Apache License 2.0.
> - Changed `detect_root_all()` structure in `customize.sh` — replaced `if/elif` chains with loop-based detection using `pkg:label` entries.
> - Changed root detection order in `customize.sh` — now APatch → KernelSU → Magisk (previously KernelSU → Magisk → APatch).
> - Changed APatch KernelPatch version fetch in `customize.sh` — uses `curl --insecure`, falls back to cached `.method` line 5 instead of `?` when the request fails.
> - Changed APatch `.method` file format in `customize.sh` — expanded from 4 to 5 lines, adds `APATCH_VER` on line 2.
> - Changed `display_current_time()`, `display_device_info()`, `display_display_info()`, `display_ram_info()`, `check_android_version()`, and `display_kernel_info()` in `customize.sh` — merged into a single `device_info()` function.
> - Changed Android codename format in `customize.sh` — bracket style (e.g. `[Q]`); SDK 32 relabeled from `Snow Cone v2 (S_V2)` to `Snow Cone [SL]`.
> - Changed `set_permissions()` in `customize.sh` — added `service.sh` to the executable permission loop.
> - Changed `post_install_actions()` in `customize.sh` — re-reads `NAME_MODULE` via `grep_prop` instead of relying on the value set earlier in the script.
> - Changed `MODDIR` detection in `service.sh` — now scans `/data/adb/modules/*/module.prop` by `id` and `author`, falling back to `$0`-based detection.
> - Changed root method check order in `service.sh` — now APatch → KernelSU → Magisk (previously KernelSU → Magisk → APatch).
> - Changed thermal-override script launch in `service.sh` — `MODDIR` is now passed as an argument to `MTK`/`QCOM`/`UNIV`.
> - Changed thermal property normalization in `action.sh` — boottime-property cleanup now handled in the same loop as `disable`/value normalization, checked first.
> - Changed the process-kill exclusion list in `thermal_kills()` in `MTK` — expanded to cover camera, audio, bluetooth, wifi, gnss, nfc, codec, and `vendor.mediatek.hardware` processes.
> - Changed `lock_thermal()` in `QCOM` — uses `find -exec` instead of `for file in $(find ...)`, matching `MTK`.
> - Changed the process-kill exclusion lists in `thermal_kill_services()` and `thermal_list()` in `QCOM` — added protection for camera, audio, bluetooth, wifi, gnss, nfc, codec, and `vendor.qti.hardware` processes.
> - Changed `MODDIR` detection in `uninstall.sh` — scans by `id` and `author`, falling back to `$0`-based detection.
> - Changed the description text in `module.prop` and the runtime description written by `service.sh` — shortened and extended to cover chipsets beyond Snapdragon and MediaTek.
> - Changed the module banner image in `module.prop`.
> - Fixed Android SDK detection in `customize.sh` — now aborts if `ANDROID_SDK` is empty or non-numeric instead of proceeding with an invalid value.
> - Fixed SoC name display in `customize.sh` — `\uXXXX` unicode escapes from `socs.json` (e.g. trademark/registered symbols) are now decoded instead of leaking as raw text.
> - Fixed a `sh` syntax error in `MTK` and `QCOM` — replaced non-POSIX process substitution with a variable-based exclusion list.
> - Fixed `pgrep` calls in `MTK` and `QCOM` — removed the `-i` flag, which Toybox's `pgrep` doesn't support.
> - Fixed `pgrep -fl` in `customize.sh` — changed to `pgrep -fa` for Toybox compatibility.
> - Fixed APatch `.method` reading in `service.sh` — realigned to the 5-line format; previously misread `ROOT_VERSION`'s line as `APATCH_VER_CODE` and `APATCH_VER_CODE`'s line as `VER_KERNEL`.
> - Fixed `action.sh` exiting with `exit 1` on successful completion — now exits `0`.
> - Fixed `uninstall.sh` exiting with `exit 1` on successful completion — now exits `0`.
> - Fixed thermal daemon termination in `MTK`, `QCOM`, and `UNIV` — now also kills the actual PID via `init.svc_debug_pid` when the running process name doesn't match its registered service label.
> - Removed `zip=$(clean_path "$zip")` from `extract()` in `verify.sh`.
> - Removed the display resolution and refresh rate output from `device_info()` in `customize.sh`.
> - Removed the separate `awk`-based boottime property cleanup pass from `action.sh`.
> - Removed `mtk_disable_boosting()`, `mtk_disable_sched_features()`, and `mtk_set_cpu_performance()` from `MTK` — outside the module's thermal scope.
> - Removed `cpu_governor_max()` from `QCOM` — outside the module's thermal scope.
> - Removed the full `/system /vendor /odm /product` partition scan from `thermal_list()` in `QCOM` — heavy per-boot cost.
> - Removed the generic `code_cache`/`shader_cache`/`dalvik-cache`/`dropbox`/`tombstones` cleanup from `uninstall.sh` — unrelated to thermal restore.
> - Removed the shared root-manager `.method` file cleanup from `uninstall.sh` — those files are shared across modules, not owned by KNTL.
> - Removed `TMPDIR` fallback and `trap` cleanup from `verify.sh`.
> - Removed `SKIPUNZIP=1` and `DEBUG=false` from `customize.sh`.
> - Removed `display_soc_info()` from `customize.sh` — remote SoC lookup/display via a GitHub-hosted `socs.json` cache no longer shown during install.
> - Removed redundant `mkdir -p "$TMPDIR/.vunzip"` from `customize.sh` — the directory is already created when `verify.sh` is sourced.
> - Removed the "NEXT" tag from the live version indicator written to `module.prop` by `service.sh`.
---

> [6.0.0]
>
> - Added handling for properties containing `disable` — force-resets them safely.
> - Added cleanup for thermal-related boottime properties — prevents reinitialization.
> - Added execution delay before launching the post-action intent.
> - Added support for additional root implementations — `FolkPatch` and `Kitsune Mask`.
> - Added display information output — resolution category and refresh rate.
> - Added SoC information detection via `socs.json` — offline chipset identification.
> - Added kernel information output during installation.
> - Added SoC name persistence via `/data/local/tmp/soc_name.txt`.
> - Added cleanup for temporary SoC detection files after execution.
> - Changed thermal property parsing logic — more consistent detection and modification.
> - Changed property override handling — expanded to support numeric, boolean, state, and service flags.
> - Changed normalization of property values — covers on/off, enabled/disabled, and active/inactive.
> - Changed sysfs thermal node locking — safer iteration approach.
> - Changed thermal override behavior for more reliable and consistent runtime execution.
> - Changed root detection logic for KernelSU, Magisk, and APatch — refined version parsing.
> - Changed spoofed-root detection — more reliable across KernelSU-based environments.
> - Changed RAM detection — categorized memory labels.
> - Changed Android codename support — extended up to SDK 37.
> - Changed module file extraction list — includes `post-fs-data.sh` and `socs.json`.
> - Changed SoC detection logic — relies on structured JSON mapping instead of heuristic matching.
> - Changed permission handling — covers new module components.
> - Changed installation output — clearer device information reporting.
> - Changed installation flow for greater reliability and maintainability.
> - Changed runtime execution — uses `setsid` instead of `nohup` for more reliable background process handling.
> - Changed chipset labeling — displays actual SoC name instead of generic platform names.
> - Changed module description update logic in `module.prop` — simplified.
> - Changed PID management for MTK and QCOM runtime scripts.
> - Changed runtime flow — reduced notification dependency, simplified.
> - Changed service execution flow — overall stability and consistency.
> - Changed Mediatek thermal override logic — simplified to reduce script complexity.
> - Changed DVFS/PPM/PBM/HPS control layers — reduced aggressiveness to improve stability.
> - Changed execution flow for more predictable runtime behavior.
> - Changed compatibility handling for newer Mediatek kernels and thermal implementations.
> - Changed Qualcomm thermal suppression flow — improved stability.
> - Changed sysfs override operations — reduced to avoid kernel conflicts.
> - Changed CPU and GPU performance enforcement logic on Snapdragon devices — streamlined.
> - Changed compatibility handling for newer Qualcomm thermal HAL behavior.
> - Changed script structure for cleaner, more predictable runtime execution.
> - Removed Android emoji indicator from module description — cleaner metadata output.
> - Removed multiple legacy MTK thermal control routines and redundant daemon kill paths.
> - Removed unused MTK power-management hooks and legacy sysfs targets.
> - Removed several legacy Snapdragon thermal override routines and redundant daemon termination logic.
> - Removed unused thermal-engine and power-management hooks from older implementations.
---

> [5.0.0]
>
> - Added `resetprop` as a fallback alongside `setprop` for broader compatibility.
> - Added persistent storage of detected root method and version — cross-script consistency.
> - Added new system properties for more stable optimization.
> - Changed thermal property handling — cleaner, more reliable parsing logic.
> - Changed thermal state override logic — reduced unnecessary verbosity while preserving effectiveness.
> - Changed thermal locking execution flow — faster and more consistent.
> - Changed root detection — expanded support for KernelSU variants, Magisk flavors, and APatch.
> - Changed spoofed/forked root environment handling — more accurate identification.
> - Changed device information reporting — includes kernel and RAM status.
> - Changed installation safety checks — strengthened Android version validation.
> - Changed SoC detection logic — accurately distinguishes Snapdragon (QCOM) and Mediatek (MTK) devices.
> - Changed Qualcomm-specific thermal and throttling overrides for Snapdragon-based devices.
> - Changed handling of thermal services, sysfs nodes, and kernel-level restrictions on QCOM platforms.
> - Changed CPU and GPU performance locking for sustained performance under load.
> - Changed execution flow for better stability and compatibility across Snapdragon SoCs.
> - Changed Mediatek-specific thermal and throttling overrides — expanded for Dimensity and Helio platforms.
> - Changed handling of MTK thermal services, daemons, and background controllers.
> - Changed CPU and GPU performance locking on MTK devices — reduces aggressive downscaling.
> - Changed control over MTK DVFS, PPM, PBM, and HPS mechanisms.
> - Changed execution stability and compatibility across a wider range of Mediatek SoCs.
> - Fixed thermal sysfs node locking — now persists safely and prevents reactivation.
> - Removed redundant system property entries.
---

> [4.0.0]
>
> - Added a new `action.sh`.
> - Added extensive control over MTK thermal modules — DVFS, PPM, PBM, HPS, and core control mechanisms.
> - Added kernel and proc-level overrides for MTK power and thermal management.
> - Added runtime status and active PID to the module version string.
> - Added runtime notifications to confirm successful optimization activation.
> - Changed the module banner.
> - Changed `SD.sh` — renamed to `QCOM.sh` for clearer, more accurate Qualcomm platform identification; full functional compatibility with previous Snapdragon-specific optimizations maintained.
> - Changed naming conventions across SoC scripts for better readability and maintainability.
> - Changed Mediatek-specific thermal and performance optimizations — refactored and significantly expanded.
> - Changed termination of Mediatek thermal daemons, services, and monitoring processes.
> - Changed CPU and GPU performance locking — forces maximum frequencies and performance governors.
> - Changed thermal trip point adjustments — extended to prevent premature throttling.
> - Changed process termination — excludes critical system and radio-related processes for stability.
> - Changed execution flow for better reliability and maintainability.
> - Changed module security and integrity enforcement.
> - Changed compatibility handling across multiple root solutions and Android versions.
> - Changed runtime stability — better process and state management.
> - Changed installation and uninstallation workflows — cleaner overall.
> - Changed transparency — richer metadata and user-facing notifications.
> - Changed service execution — refactored with PID-based process management.
> - Changed overall service stability and lifecycle handling.
> - Changed uninstall logic — refactored into clear, modular functions.
> - Changed cache cleanup coverage — includes app cache, shader cache, and system cache directories.
> - Changed execution to use strict error handling for safe, deterministic behavior.
> - Changed reliability and maintainability of the uninstallation process.
> - Fixed duplicate background service instances spawning across reboots.
> - Removed residual temporary files and runtime artifacts.
---

> [3.0.0]
>
> - Added a formatted timestamp to installation output.
> - Added random devil-themed verification messages.
> - Added precise version extraction and per-SoC script execution with PID tracking to `service.sh`.
> - Added dynamic FINAL build tag, PID indicator, detailed thermal description, and Android version emoji mapping (Q–B) to `module.prop`.
> - Added chipset-specific notifications with custom icons.
> - Added multi-algorithm hash fallback (SHA512/384/256/224/1) to `verify.sh`.
> - Added `TMPDIR` fallback and `trap`-based auto-cleanup to `verify.sh`.
> - Added removal of `KNTL*.png` notification icons to `uninstall.sh`.
> - Added dedicated functions to `MTK.sh` for PBM, DPT/DCT, thermal proc tweaks, CPU hard limit overrides, and enhanced core control disable.
> - Added extended core online forcing (cpu8–9 support), deeper HPS/PPM policy disabling, and comprehensive GPU throttling/power limit neutralization.
> - Added a `main()` function wrapping all notification-system operations.
> - Changed `customize.sh` root detection — overhauled to support all Magisk variants (Stable/Canary/Kitsune/Alpha), KernelSU (Standard/Next/SukiSU Ultra), and APatch, with persistent method tracking and version details.
> - Changed device info display — capitalized model, root-specific icons; streamlined SoC-based file cleanup (SD/MTK).
> - Changed module verification and post-install actions — refined verification, optimized post-install flow with Telegram link and reboot notification.
> - Changed `service.sh` root detection — reads persistent `.method` files from Magisk/KernelSU/APatch.
> - Changed script launch to immediate execution without boot wait; improved SoC detection robustness.
> - Changed checksum mismatch reporting in `verify.sh` — more detailed.
> - Changed `uninstall.sh` cleanup — restructured into modular functions with `set -e`.
> - Changed input/sched/boost disabling — reinforced with additional paths (`sched_boost`, `dynamic_boost`, etc.); improved governor locking via `chattr +i`.
> - Changed notification system — KNTL-themed icons and tag, full backward compatibility with the existing Mediatek thermal daemon kill list maintained.
> - Changed `SD.sh` thermal daemon/service termination — intensified with new `ctl.stop` commands, system-wide binary discovery, and getprop-based thermal process targeting.
> - Changed `final_kill` routine — expanded; thermal sysfs lockdown reinforced with optimized permission loops.
> - Changed GPU throttling bypass — `chattr +i` immutability on throttling nodes, guaranteed performance governor/`min_freq` enforcement.
> - Changed notification system branding — full KNTL branding with custom icons (`KNTL01/02.png`) and dedicated tag.
> - Removed redundant legacy cache paths from `uninstall.sh`.
---

> [1.5.0]
>
> - Added exception filters for critical processes (phone & system) on `MTK`.
> - Added file existence checks in `mtk_gpu_throttle_disable` to prevent errors on unsupported paths (MTK).
> - Added a `main` function consolidating execution for centralized control and better debugging (MTK).
> - Added error suppression (`2>/dev/null`) to `uninstall.sh`.
> - Changed `verify.sh` to a more robust version.
> - Changed module structure algorithm integration — more robust handling.
> - Changed architecture detection — easier and simpler.
> - Changed the `MTK` thermal daemon list — expanded to include the latest HAL for Android 13/14; still terminates all thermal daemons aggressively but safely.
> - Changed `MTK.sh` structure — improved readability and logical execution flow (MTK).
> - Changed `lock_thermal` — uses direct `find -exec` for efficiency (MTK).
> - Changed `uninstall.sh` — organized into `clean_cache`, `clean_system_dirs`, `remove_module`, and `main` functions.
> - Changed `uninstall.sh` deletion — replaced `rm -f` with `find -delete`.
> - Fixed inaccurate `SoC` detection from the previous version.
> - Fixed a lost-signal issue on `MTK`.
> - Fixed the CPU core range in `mtk_force_online_cores` and `mtk_set_cpu_performance` to `cpu[0-7]` for compatibility with octa-core MTK devices (MTK).
> - Removed the `fast_charge` feature for `Snapdragon`.
> - Removed the redundant `mtk_disable_governor` function — functionality covered by `mtk_set_cpu_performance` (MTK).
---

> [1.0.0]
>
> - Initial release.