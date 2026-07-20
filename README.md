# lmkd psi mod(ified)

**A module that optimizes how Android manages background apps (lmkd, psi)**

## Overview

An extension of the SkyScene Add-on, where it achieves the effect of improve how the system manages background apps by modifying memory management mechanisms (lmk, psi). And by improving background process management, it's possible to achieve a smoother and more energy-efficient system

If you want an optimization that improves the kernel's memory management behavior, check out the [SkyScene Add-on](https://github.com/WeirdMidas/SkySceneAddon), it specifically handles this aspect, such as swapping, reclaim, and others

It was intended to be a fork of [LMKD-PSI-Activator](https://github.com/lululoid/LMKD-PSI-Activator) that optimizes the lmkd psi part more efficiently and better for Android multitasking. However, it became an original project due to the stark difference in optimization between the two modules

### Features

- **📂 Pure optimization, no placebo** - Pure memory management optimization module, not containing other placebo and supporting all mainstream platforms like Qualcomm, MediaTek, and many other platforms
- **🧣 Align with Google's behavior and standards** - Follow the lmkd guidelines and standards based on AOSP/Google, while manually tuning some parameters, making lmkd more accurate and efficient based on the upstream
- **🦺 Activate and use PSI, the modern mechanism for managing background processes** - Activate and utilize the lmkd background process kill mechanism, psi (pressure stall information). This allows lmkd to be dynamic most of the time, while maintaining minfree assistance on low-memory devices
- **🥼 Clean up inefficient ROM settings** - In certain lmkd properties, a cleanup is performed to prevent the ROM or other modules via device_config from modifying our settings, allowing us to overwrite harmful changes
- **🗾 Tune for Go devices and for Non-Go devices** - Tune the behavior of lmkd for both Go and regular devices, ensuring that each device's memory capabilities are respected
- **🔄 Improve lmkd behavior based on swap and swapping algorithm** - Configure the psi thresholds relative to swap based on the swapping algorithm used, allowing lmkd to be more accurate regarding the memory reclaim capacity of the LRU or MGLRU
- **📊 Safe, efficient, and tested multiple times** -  SELinux can still be enabled

## Requirement

- Android 10 or higher
- Have PSI enabled in the kernel
- Have lmkd as the only LMK mechanism on the device
- Having ZRAM enabled in the kernel
- 3GB or more of RAM (Optional)

## Installation

- Install this module, restart your phone, wait 20 seconds before the final optimizations are applied, and voila, you can have fun with your device
- For lmkd, the algorithms below have these compression rates:
  - lz4, lzo, lz4kd, lz4k, lzo-rle: Android 15 algorithms have a compression of 2x/3x, while Android 16 and later versions have a compression of 2.8x/3.1x
  - Lz4hc, deflate: Android 15 algorithms have a compression of 3x/4x, while Android 16 and later versions have a compression of 3.1x/4.2x
  - Zstd, Zstdn: Android 15 algorithms have a compression of 4x/5x, while Android 16 and later versions have a compression of 4.2x/5.4x
  - Other algorithms: Android 15 algorithms have 2x compression, while Android 16 and later versions have 2.8x compression
    - Note: the first is lru and the second is mglru (becoming LRU/MGLRU), just so you already know which ones they are for each swapping algorithm
  - On Android 16 and later, devices with 6GB of RAM or less do NOT have the relaxation in the free ZRAM/Swap check. However, devices with 8GB or more do have this relaxation, allowing them to fully utilize their ZRAM/Swap
- Other LMKs are not compatible, only lmkd is compatible
- For Android 14 devices with 4GB of RAM (or less), the psi + minfree + new strategy model is used; for devices with 6GB of RAM (or more) or Android 15 and higher (regardless of RAM threshold), the pure psi model is used

## FAQ

### Sources

- Official information about [LMKD (Low Memory Killer Daemon)](https://source-android-com.translate.goog/docs/core/perf/lmkd?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc) provided by Google

### Suggestions for Complementary Modules

- [NoSwipeToKill](https://github.com/dantmnf/NoSwipeToKill): lsposed module by [dantmnf](https://github.com/dantmnf) to reduce the aggressiveness of HyperOS/MIUI in killing processes, recommended for users of Xiaomi ROMs that use lsposed
- [A1Memory](https://github.com/OneB1ank/A1Memory): A memory management module that implements an OEM-style memory management framework in the system server, allowing you to control certain parts of memory management more efficiently than modern Android. Exclusive to Android 8-14

## Credit

@Doug Hoyte  
@topjohnwu  
@卖火炬的小菇凉--改进在红米K20pro上的zram兼容性  
@钉宫--模块配置文件放到更容易找到的位置  
@予你长情i--发现与蝰蛇杜比音效共存版magisk模块冲突导致panel读写错误  
@choksta --协助诊断v4版FSCC固定过多文件到内存  
@yishisanren --协助诊断v5版FSCC在三星平台固定过多文件到内存  
@方块白菜 --协助调试在联发科X10平台ZRAM相关功能  
@Simple9 --协助诊断在Magisk低于19.0的不兼容问题  
@〇MH1031 --协助诊断位于/system/bin二进制工具集的不兼容问题  
@yc9559 -- Obvious credits that I forgot to put, SkyScene only exists because of him, the GOAT of the 2018-2020 modules      
@Iamlooper -- For the magisk MMT Reborn template. Thanks to the template, I was able to replace the old qti-mem-opt template and keep all the features without extra additions! Also now the cpu usage of the module has reduced by 2%, little but useful      
