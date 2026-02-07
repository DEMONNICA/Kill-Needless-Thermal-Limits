> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [6.0.0] `NEXT`
>
> - Improved thermal property parsing logic for more consistent detection and modification.
> - Expanded property override handling to support numeric, boolean, state, and service flags.
> - Added handling for properties containing "disable" to force-reset them safely.
> - Improved normalization of property values such as on/off, enabled/disabled, and active/inactive.
> - Added cleanup for thermal-related boottime properties to prevent reinitialization.
> - Refactored sysfs thermal node locking using a safer iteration approach.
> - Added execution delay before launching the post-action intent.
> - Improved runtime reliability and consistency of thermal override behavior.
> - Refactored root detection logic for KernelSU, Magisk, and APatch environments with improved version parsing.
> - Added support for additional root implementations including FolkPatch and Kitsune Mask.
> - Improved spoofed-root detection reliability across KernelSU-based environments.
> - Added display information output (resolution category and refresh rate).
> - Added SoC information detection using `socs.json` for offline chipset identification.
> - Improved RAM detection with categorized memory labels.
> - Extended Android version codename support up to SDK 37.
> - Added kernel information output during installation.
> - Improved module file extraction list, including `post-fs-data.sh` and `socs.json`.
> - Refined SoC detection logic to rely on structured JSON mapping instead of heuristic matching.
> - Improved permission handling for new module components.
> - Enhanced installation output clarity and device information reporting.
> - Improved overall installation reliability and maintainability.
> - Refactored runtime execution to use `setsid` instead of `nohup` for more reliable background process handling.
> - Added support for SoC name persistence using `/data/local/tmp/soc_name.txt`.
> - Improved chipset labeling to display the actual SoC name instead of generic platform names.
> - Simplified module description update logic in `module.prop`.
> - Removed Android emoji indicator from module description for cleaner metadata output.
> - Improved PID management for MTK and QCOM runtime scripts.
> - Added cleanup for temporary SoC detection files after execution.
> - Reduced notification dependency and simplified runtime flow.
> - Improved overall service stability and execution consistency.
> - Removed multiple legacy MTK thermal control routines and redundant daemon kill paths.
> - Simplified Mediatek thermal override logic to reduce script complexity.
> - Removed unused MTK power-management hooks and legacy sysfs targets.
> - Reduced aggressive DVFS/PPM/PBM/HPS control layers to improve stability.
> - Streamlined execution flow for more predictable runtime behavior.
> - Improved compatibility with newer Mediatek kernels and thermal implementations.
> - Removed several legacy Snapdragon thermal override routines and redundant daemon termination logic.
> - Simplified Qualcomm thermal suppression flow for improved stability.
> - Reduced excessive sysfs override operations that could cause kernel conflicts.
> - Streamlined CPU and GPU performance enforcement logic on Snapdragon devices.
> - Removed unused thermal-engine and power-management hooks from older implementations.
> - Improved compatibility with newer Qualcomm thermal HAL behavior.
> - Optimized script structure for cleaner and more predictable runtime execution.
---

> [5.0.0] `NEXT`
>
> - Refined thermal property handling with cleaner and more reliable parsing logic.
> - Improved compatibility by supporting both `setprop` and `resetprop` as fallback mechanisms.
> - Reduced unnecessary verbosity while preserving effective thermal state overrides.
> - Streamlined execution flow for faster and more consistent thermal locking.
> - Ensured persistent and safe locking of thermal sysfs nodes to prevent reactivation.
> - Significantly improved root detection with expanded support for KernelSU variants, Magisk flavors, and APatch.
> - Enhanced handling of spoofed and forked root environments for more accurate identification.
> - Added persistent storage of detected root method and version for cross-script consistency.
> - Improved device information reporting, including kernel and RAM status.
> - Strengthened Android version validation and overall installation safety checks.
> - Refined SoC detection logic to accurately distinguish Snapdragon (QCOM) and Mediatek (MTK) devices.
> - Improved Qualcomm-specific thermal and throttling overrides for Snapdragon-based devices.
> - Enhanced handling of thermal services, sysfs nodes, and kernel-level restrictions on QCOM platforms.
> - Improved CPU and GPU performance locking for sustained performance under load.
> - Refined execution flow for better stability and compatibility across Snapdragon SoCs.
> - Expanded Mediatek-specific thermal and throttling overrides for Dimensity and Helio platforms.
> - Improved handling of MTK thermal services, daemons, and background controllers.
> - Enhanced CPU and GPU performance locking to reduce aggressive downscaling on MTK devices.
> - Refined control over MTK DVFS, PPM, PBM, and HPS mechanisms.
> - Improved execution stability and compatibility across a wider range of Mediatek SoCs.
> - Adjusted and reorganized system properties by removing redundant entries and adding new ones for more stable optimization.
---