# Lenovo-g50-70
The hackintosh configs and tools for Lenovo G50-70.  
此机型的配置为  
i5-4258u + hd5100  
ELAN PS/2触控板  
高通AR956x无线网卡  
## 说明
clover配置来源于网络+我自己的调整，我并不能解决很多问题  
经过我自身的反复尝试，目前这个EFI已经比较完善了，所以分享出来，给需要的人  
系统版本为10.14.6  
## 特性
所有usb接口，usb2.0/3.0 正常  
休眠正常，长时间休眠唤醒正常  
外接usb网卡、鼠标也可以休眠  
触控板简单手势可用  
电源管理，传感器正常  
## 存在问题
WIFI可以驱动，但没必要，驱动方法写下面。  
蓝牙冷启动问题无解，不建议使用，可以关闭，后面写方法。  
触控板滚动惯性基本没有  
开机第二阶段8苹果花屏闪一下  
## 建议
### 务必注意
bios设置传统引导方式，否则开机花屏，需要休眠一次才能正常  
如果开机后存在花屏问题，请注入EDID，每个人可能都是不一样的，我自己更换过屏幕。  
建议采用一键开启Hipdi的脚本（github）开启Hidpi同时注入EDID，方便。  
### WIFI及蓝牙
* 网卡虽然可以驱动，但是限速严重基本只有100kb/s速度,建议换网卡，资料自寻。  
* 可以使用usb无线网卡  
* 可以使用手机usb共享网络，所需驱动HoRNDIS.kext,已经放入  
### 触控板
最适合这个触控板的驱动为 AppleSmartTouchpadController，这个驱动闭源并且停更很久了，但没有更好的选择  
可以在快捷键设置自己的手势，支持三指上下左右，四指按压  
## 一些方法
1. 关闭蓝牙 在/System/Library/Extensions/IOBluetoothFamily.kext/Contents/PlugIns/BroadcomBluetoothHostControllerUSBTransport.kext/Contents/
目录下  
使用PlistEdit pro 这个软件在 Info.plist 文件中 BroadcomUSBBluetoothHCIController 下注入自己的蓝牙id  
修复权限并重启就可以关闭蓝牙  
2. 驱动AR9565方法
需要lilu.kext支持  
网上寻找 被苹果移除的 AirPortAtheros40.kext 高通驱动，安装到系统/Library/Extensions  
ATH9KInjector.kext 安装到 /System/Library/Extensions  
ATH9KFixup.kext 放入 Clover 内 修复权限，重启即可，蓝牙无解  
可以在config.plist中添加启动参数 -ath9565 -lilubetaall  
3. 修复权限软件为Kext Utility  

