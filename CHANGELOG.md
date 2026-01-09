> `Changelog:`
> - All significant changes to this project will be documented here.
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