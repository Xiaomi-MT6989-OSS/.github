# rothko LineageOS 协作仓库

Redmi K70 Ultra（`rothko`）的非官方 LineageOS 23.2 设备适配源码与构建协作入口。

## 设备与构建仓库

| 仓库 | 用途 | 当前内容边界 |
| --- | --- | --- |
| [`android_device_xiaomi_rothko`](https://github.com/Xiaomi-MT6989-OSS/android_device_xiaomi_rothko) | rothko 设备树：设备配置、硬件服务、overlay、SELinux 策略和提取工具 | 当前设备树的源码部分；stock 二进制需本地提取 |
| [`proprietary_vendor_xiaomi_rothko`](https://github.com/Xiaomi-MT6989-OSS/proprietary_vendor_xiaomi_rothko) | vendor 构建规则和 stock 文件来源账本 | 不含原厂 vendor/ODM 二进制；参与者需自行准备匹配固件并提取 |
| [`rothko-kernel-extraction`](https://github.com/Xiaomi-MT6989-OSS/rothko-kernel-extraction) | 从指定 stock 固件提取内核材料 | 当前是校验和固定的提取配方，不是可编译的 Linux 内核源码 |
| [`rothko-lineage-integration`](https://github.com/Xiaomi-MT6989-OSS/rothko-lineage-integration) | 将设备树与 Android 源码组合起来 | 固定 manifest、平台补丁、提取和构建说明、已知问题及验证范围 |

## 源码基线

- Android 源码：LineageOS 23.2 / Android 16。
- 设备固件基线：HyperOS `OS3.0.307.0.WNNCNXM`。
- stock vendor：Android 14 / API 34。
- integration manifest 固定 1,167 个项目；另应用 13 组平台补丁，共 74 个提交。

## 其他必需的上游仓库

这些仓库由固定 manifest 拉取，不需要复制进 rothko 设备树：

- [`LineageOS/android_hardware_mediatek`](https://github.com/LineageOS/android_hardware_mediatek)，源码路径 `hardware/mediatek`。
- [`LineageOS/android_hardware_xiaomi`](https://github.com/LineageOS/android_hardware_xiaomi)，源码路径 `hardware/xiaomi`。
- [`LineageOS/android_device_mediatek_sepolicy_vndr`](https://github.com/LineageOS/android_device_mediatek_sepolicy_vndr)，源码路径 `device/mediatek/sepolicy_vndr`。

硬件仓库的固定提交和 rothko 所需补丁记录在 `rothko-lineage-integration`。其中 `hardware/mediatek` 当前有 5 个通用 Thermal HAL 修复提交，集成仓库以可重放补丁系列维护；其余上游仓库直接使用 manifest 固定版本。

只下载设备树不足以复现完整系统。请从 `rothko-lineage-integration` 开始，按其中的 `BUILD.md` 检出固定版本，并在本机准备 stock 固件输入。

## 当前状态

这是非官方的设备适配与公开协作项目。当前源码组合尚未通过独立的干净同步和完整 ROM 构建；请先查看 integration 仓库的 `VALIDATION.md`、`KNOWN_ISSUES.md` 和 `baseline.json`。其他镜像上的实机结果不自动代表当前源码组合已验收。

当前没有独立的 rothko common 仓库、可编译内核源码仓库或单独的 MIUI Camera 仓库。等出现真实共享代码、完整内核源码或需要单独维护的相机组件时，再按实际依赖增加仓库。

