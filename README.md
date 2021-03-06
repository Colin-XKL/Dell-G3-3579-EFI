# Dell-G3-3579-EFI
Hackintosh - EFI for Dell G3 3579

# Brief Introduction 
This is the EFI file for Dell G3 3579 laptop.

> **CPU**:  Intel i5-8300H & UHD 630   
> **GPU**:  Nvida GTX 1050Ti  (Not work in mojave)  
> **HDD**:  Western Blue 1TB (SATA3)  
> **SSD**:  HP EX920 256GB (NVME)  
> **Audio**：   Realtek ALC236  
> **Wireless**: Intel Wireless AC 9462 (Not work)  
> **Tested Mac OS Version**:   10.14.2

# 简介
Dell G3 3579的EFI文件，分享给折腾黑苹果的朋友。机型相同的可以直接拿去用，硬件相似的可以参考。我也会把部分折腾过程记录下来，感兴趣的朋友可以一起交流学习下。

有兴趣的朋友可以到站点 **黑苹果笔记** <http://hackintosh.colinx.one> 学习相关知识


# 现状
> **CPU**：OK  (识别√  变频√)    
> **显示**：  OK  (UHD 630  VRAM 2048M)  
> **声卡**：  OK  (扬声器√ 笔记本麦克风√ 耳机√ 耳机麦克风×)  
> **有线网卡**：  OK  
> **无线网卡**：  无法驱动，需更换  
> **蓝牙**：  无法驱动，需更换  
> **鼠标**：  OK  
> **触控板**：  OK (基本手势√  苹果高级手势√)  
> **键盘**：  OK  (基本功能键√ 音量控制√ 媒体控制√ 亮度控制√)  
> **USB**：  OK  (右侧USB2.0√  左侧USB3.0√)  
> **睡眠**：OK  
> **电量显示**：OK  
> **HDMI**：  *未解决*  
> **读卡器**：  *未解决*  


# 说明
虽然我折腾黑苹果是从最小EFI开始的，但是当时并没有上Git。大概2019年初开始正式折腾mojave黑苹果，2019年暑假又折腾了一番解决了亮度快捷键和触控板的问题，2019年末才上的Git。Git上的历史记录只能追溯到2019年末的版本，Release里可以追溯到解决亮度快捷键之前的版本。有需要的朋友可以到Release里查找较早版本的EFI。

目前的黑苹果驱动情况已经完全可以满足日常使用了。不过结合我实际体验来看，不是很推荐外出的时候使用黑苹果系统，一是本机型并非轻薄本，外出携带比较笨重，续航不足。二是无线网络的支持欠佳。

## 无线网络无法使用的几种替代方案：
|方案|优点|缺点|
|---|---|---|
|选择USB 无线Wifi |方便，不折腾|不美观，信号不稳定|
|选择更换掉内置的Intel无线网卡 |美观、稳定|拆机折腾、贵 |
|用手机作USB网络分享* |成本低|线缆束缚|
|使用有线网络|快速、稳定|受环境制约|


_*需要安装RnDIS驱动，本EFI已内置_
## 屏幕扩展的几种替代方案
|方案|优点|缺点|
|---|---|---|
|使用USB转接HDMI/DP|方便|分辨率限制在2K*，部分转接器不支持mac|
|降级到10.13安装驱动|兼容性好、稳定|折腾|
|升级到10.15用iPad作副屏|兼容、稳定|需要iPad|
|使用Duet Display用iPad作副屏|不折腾|需要iPad、购买Duet|
|使用屏幕分享软件等|成本低|兼容性差、延迟高|


_*市面上的USB3.0转HDMI/DP的最大传输分辨率受USB3.0的传输带宽制约，只能到2K。4K的只有原生Type-C口转接_

# 已知问题
- Kext更新后的第一次启动有可能会启动失败，需要手动重启一下
- 触控板是可以正常使用的，如果发现突然不能用了，看一下是不是碰到了PrintScreen快捷键，这个按键现在是触控板的开关了
- 如果出现偶现的开机黑屏，不要慌张，等待大约三分钟即可。这个时候无论系统是启动成功还是失败，都会有反馈结果。而当你听到了系统开机的音效，则说明系统已经启动成功



# 黑苹果笔记 & 更新历史

## v1.2 2019.3.14 **声卡**
ALC236 LayoutID：13+Hackintool处理 = 声音播放+麦克风
笔记本键盘OK
触控板->鼠标
## V1.3 **USB网络共享**
RNDIS OK
## V2.0  **核显**
UHD630 OK

## V2.1 2019.3.15

EDID 修补  
CPU 变频正常，无需处理

## V2.2  **USB修补**
### 注意:
使用`hackintool`修补usb时导出kext和dsdt补丁前会要求修改`config.plist`,修改会导致异常，应略过此步骤
### 问题：
靠下的USB3.0无法使用USB 2.0  
Hub需接上部的USB3.0
### 说明：
更正此问题只需更新`USBPort.kext`
### 改动：
+XHCI-unsupported.kext  
+USBPort.kext  
-USBInjectAll.kext  

## V2.3  2019.3.15
声卡`platform-id`修改为`15`，外放OK 麦克风OK 耳机OK  
耳机麦克风Failed  

待解决问题：
电量显示
触控板
读卡器
时间显示
睡眠
文件名乱码

## V3.0  
从Github上另一个EFI中学习了一下，做了很多调整。如电量显示等。

## V3.1. 19.8.6 **亮度记忆 - 修复开机自动恢复最大亮度**
删除 `drivers64UEFI` 下的 `EmuVariableUefi-64.efi` 重启两次即可保存亮度 --失败  
hotpatch：`SSDT-ALS0`  --成功  
//所有hotpatch都依赖`SSDT-RMCF`  

## V3.2 19.8.6  **亮度快捷键**
hotpatch：`SSDT-BRT6` --失败  
hotpatch：`SSDT-Dell_FN` --失败  
hotpatch：`SSDT-BKeySMEE-Dell`--失败  

### 测试：
<https://noobsplanet.com/index.php?threads/brightness-keys-remapping-f11-and-f12-for-hackintosh.131/>   
基本操作 --失败  
手动启用aml --成功  
### 优化：
去除`SSDT-BKeySMEE-Dell.aml`  --无碍  
去除DSDT重命名 --无碍  
重制为hotpatch  V1.0 --失败  
### 后续：对比正确应用补丁后的DSDT文件，修改BRT6 hotpatch
重制为hotpatch  V2.0 --失败  
重制为hotpatch  V3.0 --成功  
-查找原BRT6方法汇编代码使其失效，以启用自定义的BRT6方法  
-2019.8.11  

## V3.3  19.8.11  
RnDIS update --成功  

## V3.4 19.8.12  **触控板**
--`VoodooI2C` + `VoodooI2CHID`  
--触控板所有手势  √

## V3.5 19.8.13  读卡器
--Voodoo SDHC 1.1.2  withDMA  失败  
--Voodoo SDHC 1.1.2 withoutDMA 失败  
--取消

## V3.5 19.8.19  **Clover Configuration**
--Linux Kernel 支持  ✅  
--NvDisable=1✅  
--默认启动MAC分区✅  
--取消verbose  
--取消自动扫描Clover Tools  
  
--修复偶现开机黑屏三分钟 BootArg -cflbkltfix  待确认  
  --需取消`SSDT-PNLF-CoffeeLake.aml`,但取消后无法进行亮度调节  
  --使用AddPNLF即使到最大亮度依然很暗  
  --依目前观测结果，黑屏只有Kext缓存更新时才会触发  

## V3.6 19.8.21  
尝试解决偶现的由VoodooPS2Controller引发的Kernel Panic  
--Update VoodooPS2Control ->2.0.2[Github]
--实际未能修复，撤销此版本

## V3.6 20.2.29  精简
精简了部分不必要的网卡驱动

## V3.7 20.2.29  更新驱动
更新了`VoodooI2C`和`VoodooPS2`，解决了偶现的Kernerl Panic。同时也得益于VoodooPS2的更新，大写锁定的LED灯的显示问题也解决了  
同时发现原PrintScreen快捷键变成了触控板开关键。还是蛮意外的，因为这个机型并没有原生的切换触控板开关的快捷键

# 鸣谢
* 黑果小兵 <blog.daliansky.net>
* Clover作者
* Lilu等kext的作者
* VoodooI2C项目: <https://github.com/alexandred/VoodooI2C>
* VoodooPS2项目: <https://github.com/acidanthera/VoodooPS2>