# X79主板OpenCore_EFI文件

## 特别感谢
- **[xiaoleGun](https://github.com/xiaoleGun)**
- **[峨眉山市雅铭网络工作室](https://github.com/wy414012)**

## 设备硬件参数
- **主板:HUANANZHI X79 (Q67芯片组)**
- **CPU:E5-2690 v2**
- **GPU:华硕580_2048SP (570VBIOS)**
- **声卡:ALC897 (layout-id:12)**
- **网卡:RealtekRT8111**
- **硬盘：Unknown**
- **other：Unknown，懒得写了**

## EFI基本信息
- **当前OpenCore版本为0.9.9**
- **debug状态：启动参数无硬件加速、有日志输出**
- `-amd_no_dgpu_accel`禁用硬件加速，`-v`日志输出（跑码）
- **IvyBridge-EP平台不支持AVX2.0，但Apple在Ventura以及往上版本删除了对没有AVX2.0指令集芯片的支持，所以启动参数`-crypt_force_avx`以及NoAVXFSCompressionTypeZlib-AVXpel已默认启用**
- **对应机型：MacPro2019（标识：MacPro7,1，对应board-id：Mac-27AD2F918AE68F61），建议就用这个不要改就行了，使用iMacPro1,1会出现PS2键盘无效的问题，USB键盘请忽略**
- **当前已知最低版本为macOS11.6，最高版本为macOS14.3.1，其他更低或更高版本没测**
- **硬件详细信息请参考[B站视频](https://www.bilibili.com/video/BV1e1421d7wa/)中的简介**

## 注意
- **本人不是专门折腾黑苹果的，如有错误请谅解并及时告知**
- **「芯片组为H61/Q63/65/67等非原x79核心请注意」：如果系统是macOS12以及往后版本，CPU有10核心及更多的情况下，用此EFI仍然出现多核心内核恐慌问题的话，请关闭几个核心（建议变成8或6核心都行）再参考下面这条。如果只打算用macOS11且并不升级可以忽略**
- **多核心恐慌参考，我的EFI中的DSDT文件不清楚能不能通用，这是修复恐慌的，所以默认启用；在启用情况下仍然出现恐慌请[点击跳转参考贴尾部的故障排除及解决方案](https://www.hackintosh-forum.de/forum/thread/55510-install-monterey-big-sur-on-any-x79-motherboard-huananzhi-chinese-gigabyte-etc-a/)**
- **1.显卡免驱问题导致需要关闭硬件加速（macOSVentura及其往上版本，显卡输出黑屏或无信号）、2.变频问题修复参考、3.TSC同步核心驱动来源：[huaNan_x79_e5_2670_v1_c2](https://github.com/wy414012/huaNan_x79_e5_2670_v1_c2)**
- **变频修复两种方案：1.使用上面这个（请启用SSDT-CPUM并关闭CPUFriend两个驱动，不是2690v2的用方法2）；2.使用CPUFriend驱动，禁用SSDT-CPUM，仿冒机型是使用MacPro7,1（对应board-id：Mac-27AD2F918AE68F61）机型的无需再生成**
- **DP参数中有本人显示器EDID（AAPL00,override-no-connect）和显卡VBIOS的风扇调用数据（PP_PhmSoftPowerPlayTable），如不可用请删除**
- **EFI已默认修复M.2固态硬盘识别为外置移动存储的问题，如果没有此问题请禁用或删除SSDT-NVMe**
- **EFI中的SSDT-RX580文件仅仅是对显卡进行性能优化，并无其他特定问题要修复，不是对应显卡的建议禁用或删除**

## 相关开源
- **[OpenCore](https://github.com/acidanthera/OpenCorePkg)**
- **[OpenCore-Legacy-Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher)**
- **[CpuTscSync](https://github.com/wy414012/CpuTscSync)**
