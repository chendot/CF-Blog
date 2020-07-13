---
title: "MacOS 调优"
date: 2020-06-15
sidebar: false
description: 折腾mac优化那些事
tags:
  - "IT"
categories:
  - "技术文档"
---

## pmset
mac 休眠模式种类：  
1. mode 0：当前状态保存在内存中，系统继续供电，唤醒速度快
2. mode 1：保留到专用磁盘空间，唤醒时需重新加载  
3. mode 3：默认模式，将当前状态保存在内存中，当电快耗尽时将当前状态保存到磁盘中，然后完全关机。
4. mode 25：与mode 3的区别在于会直接停止内存供电而不等到低电量  

模式查看及设置：
```bash
pmset -g
System-wide power settings:
Currently in use:
 standbydelaylow      10800     # 盒盖后在内存保留秒数
 standby              1         # 只有hibernatemode为3，25才工作
 halfdim              1
 hibernatefile        /var/vm/sleepimage
 proximitywake        0
 gpuswitch            2
 powernap             0
 disksleep            10    # disk进入休眠时间
 standbydelayhigh     86400
 sleep                1     # 闲置进入休眠时间，单位分钟；sleep >= disksleep >= display sleep
 hibernatemode        25
 ttyskeepawake        1
 displaysleep         2     # 显示器进入休眠时间
 tcpkeepalive         1     # 网络唤醒功能
 highstandbythreshold 50
 acwake               0
 lidwake              1
# 修改状态，需输入密码
sudo pmset -b hibernatemode 25
sudo pmset -a hibernatemode 3
sudo pmset -c hibernatemode 0
sudo pmset -b tcpkeepalive 0

# 参数含义
# -c 调节设定用于连接充电器的时候
# -b 调节设定用于使用电池（Battery）的时候
# -u 调节设定用于使用 UPS 的时候
# -a 调节设定用于全部情景

```
## 其它常规
关闭iCloud同步、日常关闭蓝牙、降低特效等


## 守护进程
#### 启动服务配置
可以通过三种方式配置：
- 系统偏好设置-账户-登陆项
- /System/Library/StartupItems 和 /Library/StartupItems/
- launchd 系统初始化进程配置

禁用服务命令：
```bash
sudo launchctl unload plist文件路径
sudo launchctl unload -w plist文件路径
# -w 选项会将plist文件中无效的key覆盖掉，建议加上
```

https://www.cnblogs.com/jinjiangongzuoshi/p/5373711.html

建议禁用的服务参考  
```bash
# 关闭索引服务
sudo mdutil -a -i off   

# 关闭mds_stores，禁用spotlight的前提
sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist
sudo launchctl unload -w /System/Library/LaunchAgents/com.apple.Spotlight.plist

# 关闭ReportCash
sudo launchctl unload -w /System/Library/LaunchAgents/com.apple.ReportCrash.plist
sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.ReportCrash.Root.plist

# airportd

# autofsd自动挂载各种网络文件系统。比如NFS, SMB, AFS等。配置文件在 /etc/auto_master和/etc/auto_home，如果你不使用任何网络文件系统，可以禁用这个服务。使用方式详见：
# http://commandlinemac.blogspot.com/2009/09/introduction-to-autofs-in-mac-os-x.html

# /usr/sbin/blued 蓝牙支持服务。如果你不想使用蓝牙，可以禁用它。

# cupsd  打印机支持。如果你不想用打印机，可以禁用该服务。
sudo launchctl unload -w /System/Library/LaunchDaemons/org.cups.cupsd.plist 
sudo launchctl unload -w /System/Library/LaunchDaemons/org.cups.cups-lpd.plist 

SharedServices.Agent
Apple的MobileMe服务，如果你不使用，可以禁用该服务。

/System/Library/LaunchAgents/com.apple.AirPortBaseStationAgent.plist 
```

## 系统完整性保护（System Intregrity Protection, SIP）

Mac OS X 系统默认开启了完整性保护（System Intregrity Protection，SIP），所以即使是root帐户也无法修改系统目录中的文件，如/System/Library/LaunchDaemons/ssh.plist。如果需要修改受保护的文件，需要禁用保护功能，步骤如下：

重启电脑，按住Command+R(直到出现苹果标志)进入Recovery Mode(恢复模式)
```bash
csrutil disable # 禁用SIP，需重启
csrutil enable  # 启用SIP
csrutil status  # 查看SIP状态
```