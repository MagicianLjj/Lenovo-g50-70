# Lenovo-g50-70
The hackintosh configs and tools for Lenovo G50-70.  
此机型的配置为  
i5-4258u + hd5100  
ELAN PS/2触控板  
高通AR956x无线网卡
## 更新
精简acpi与patchs  
精简驱动 删除fakeid 系列，使用virtualSMC替换fakeSMC  
准备迁移至opencore  
## 说明
clover配置来源于网络+我自己的调整    
目前这个EFI已经比较完善了，所以分享出来  
ACPI有很多错误，我选择无视  
系统版本为10.14.6  
## 特性
usb接口基本正常  
休眠正常，长时间休眠唤醒正常   
触控板简单手势可用  
电源管理，传感器正常  
## 存在问题
WIFI可以驱动，速度有些问题，（路由器必须设置11n，才正常）驱动方法写下面。  
蓝牙冷启动问题无解，不建议使用，可以关闭，后面写方法。  
~~触控板滚动惯性基本没有~~    
usb接口没有定制，3.0存在问题  
睡眠偶有异常，还是存在唤醒问题    
## 建议
### 注意事项
~~bios设置传统引导方式，否则开机花屏，需要休眠一次才能正常~~  
bios 设置UEFI引导，8个苹果花屏消失，通过注入EDID可以修复开机花屏。  
如果开机后存在花屏问题，请注入EDID，每个人都是不一样的，我自己更换过屏幕。  
~~建议采用一键开启Hipdi的脚本（github）开启Hidpi同时注入EDID，方便。~~  
目前缓冲帧为勾选“注入intel”以及仿冒id0x04128086  
### WIFI及蓝牙
* 网卡虽然可以驱动，但是在路由器b/g/n混合模式下会导致速度异常，要设置11only才正常   
* ~~可以使用usb无线网卡，便宜而且支持5ghz，挺不错的~~  
* 可以使用手机usb共享网络，所需驱动HoRNDIS.kext,已经放入  
### 触控板
最适合这个触控板的驱动为 AppleSmartTouchpadController，这个驱动闭源并且停更很久了，但没有更好的选择  
可以在快捷键设置自己的手势，支持多指操作 
可以在驱动的plist中修改一些映射    
## 一些方法
1. 关闭蓝牙 在/System/Library/Extensions/IOBluetoothFamily.kext/Contents/PlugIns/  
BroadcomBluetoothHostControllerUSBTransport.kext/Contents/  
目录下  
使用xcode10在 Info.plist 文件中 BroadcomUSBBluetoothHCIController 下注入自己的蓝牙id  
修复权限并重启  
2. 驱动AR9565方法
需要lilu.kext支持  
网上寻找 被苹果移除的 AirPortAtheros40.kext 高通驱动，安装到系统/Library/Extensions  
ATH9KInjector.kext 安装到 /System/Library/Extensions  
ATH9KFixup.kext 放入 Clover 内 修复权限，重启即可  
可以在config.plist中添加启动参数 -ath9565 -lilubetaall  
3. 蓝牙驱动方法
通过虚拟机加载蓝牙固件，最轻便的linux系统参考TinyCore/CorePlus  
4. 修复权限软件为Kext Utility  

