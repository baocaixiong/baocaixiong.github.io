---
title: Deskmini310安装黑苹果
date: 2019-02-20 18:15:27
tags:
- 黑苹果
- Deskmini310
---



# 主机配置

- deskmini 310 主机带电源
- i3 8100 淘宝散片
- 阿斯加特 256G SSD，NVME
- 两条威刚XPG笔记本内存，8G 2440
- ID-COOLING IS40X 散热器
- BCM94352Z DW1560无线网卡，直接免驱

### 安装

### 刻录U盘镜像

可以使用balenEtcher工具进行刻录，镜像使用原版或黑果小兵的增强版本

{% asset_img lalenaEtcher.png This is an example image %}

### BIOS设置

> （bios版本v3.1,升级3.4可能会装不上！）

1. Load UEFI Defaults
2. Advanced
   - Onboard HD Audio: Enabled
   - USB Configuration, XHCI Hand-off, Enabled
   - Super IO Configuration, Serial Port, Disabled（必须）
3. Security Secure Boot, Disabled(by default)
4. CSM打开 ，仅UEFI
5. 设置U盘第一位启动

# 资源下载

EFI ：[Deskmini310_final_BCM94352z_AppleALC_CLOVER](https://www.chenweikang.top/wp-content/uploads/2018/11/Deskmini310_final_BCM94352z_AppleALC_CLOVER.zip)

基于上边的EFI增加HDMI输出的配置：[Deskmini310_DP+HDMI_CLOVER](https://www.chenweikang.top/wp-content/uploads/2018/11/Deskmini310_DPHDMI_CLOVER.zip)

系统：[macOS Mojave 10.14.1(18B75) Installer with Clover 4726.dmg](https://mirrors.dtops.cc/iso/MacOS/daliansky_macos/)

参考了：https://github.com/YCF/Hackintosh-EFI-for-deskmini-310-i3-8100

**最后感谢 camgame及 群友们共同的努力，远景传送**：<http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1799808&extra=page%3D1%26filter%3Dtypeid%26typeid%3D1332%26typeid%3D1332>

欢迎加入Deskmini310 交流群：580456695



转自[左手代码右手诗](https://www.chenweikang.top/) » [华擎 Deskmini 310 黑苹果 Hackintosh Mojave 10.14.x 完美EFI](https://www.chenweikang.top/?p=613)，留下记录随时翻阅