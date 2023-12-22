---
title: adb常用命令记录
categories: Tools
tags: adb
date: 2023-12-22 12:00:00
toc: true
---


## 常用命令

| 指令         | 作用                 | eg |
| :---         | :---                | :--- |
|adb devices   |查看连接设备           |      |
|adb install apk路径  |安装应用              | adb install test.apk |
|adb install -r apk路径|安装apk 到sd 卡       |adb install -r demo.apk|
|adb uninstall 包名| 卸载应用，需要指定包 |     adb uninstall cn.com.test.mobile|
|adb uninstall -k 包名|卸载app 但保留数据和缓存文件|adb uninstall -k cn.com.test.mobile|
|adb shell pm list packages |列出手机装的所有app 的包名||
|adb shell pm list packages -3 |列出除了系统应用的第三方应用包名|
|adb shell pm clear cn.com.test.mobile |清除应用数据与缓存
|adb shell am start -ncn.com.test.mobile/.ui.SplashActivity |启动应用
|adb shell dumpsys package |包信息Package Information
|adb shell dumpsys meminfo |内存使用情况Memory Usage
|adb shell am force-stop cn.com.test.mobile |强制停止应用
|adb logcat |查看日志
|adb logcat -c |清除log 缓存
|adb reboot |重启
|adb get-serialno |获取序列号
|adb shell getprop ro.build.version.release |查看Android 系统版本
|adb shell top -s 10 |查看占用内存前10 的app
|adb push <local> <remote> |从本地复制文件到设备
|adb pull <remote> <local> |从设备复制文件到本地
|adb bugreport |查看bug 报告
|adb shell dumpsys battery|手机电量信息
|adb logcat -v time > D:\logs\logcat.log|输出实时日志并保存在本地文件，通过Ctrl+C来停止。抓取日志的步骤：先输入命令启动日志，然后操作App，复现bug，再ctrl+c停止日志，分析本地保存的文件|

### 系统操作指令

| 指令         | 作用                 | eg |
| :---         | :---                | :--- |
adb shell getprop ro.product.model	|获取设备型号	
adb shell getprop ro.build.version.release	| 获取设备android系统版本	
adb get-serialno	|获取设备的序列号（设备号）	
adb shell wm size	|获取设备屏幕分辨率	
adb shell screencap -p /sdcard/mms.png	|屏幕截图	
adb pull /sdcard/mms.png D:\app	|将截图导出到本地
adb shell dumpsys activity	|获取当前 Android 系统 Activity 栈中 Activity 信息
adb shell dumpsys activity top	|获取当前 Android 系统 中与用户交互的 Activity 的详细信息
adb shell dumpsys meminfo [应用包名]	|查看应用的内存使用情况
adb shell dumpsys package [应用报名]	|获取手机里面某个 apk 的应用信息、版本信息
adb shell dumpsys activity activities	|显示当前所有在运行的任务栈，并可查看栈中所有的 Activity 的列表


## 连接设备

adb [-d-e-s <serialNumber>] <command>
连接指定设备
参数：
* -d 指定当前唯一通过USB 连接的Android 设备为命令目标

* -e 指定当前唯一运行的模拟器为命令目标

* -s <serialNumber> 指定相应serialNumber 号的设备/模拟器为命令目标

command 为所需对设备执行的命令

eg:
```
$adb devices
List of devices attached
cf263b7f device
emulator-5554 offline
192.168.1.6:5555 device
$adb -s cf263b7f #连接cf264b8f 设备
```
adb devices 查看已连接的设备信息, 上面已经连接3台设备。



## adb logcat

adb logcat  
在终端窗口中，按下 Ctrl + C（Windows/Linux）或 Command + C（Mac），这会中断正在运行的命令，包括 adb logcat。

#### 保存到文件
adb logcat > logcat.txt
将设备的日志输出保存到指定的文件（logcat.txt）。这会将所有的日志信息写入文件。

#### 过滤保存
adb logcat -s TAG > logcat.txt
过滤保存，只保存特定 TAG 的日志信息。

#### 限制保存行数
adb logcat -t 1000 > logcat.txt
限制保存的行数，上述例子保存最新的1000行日志。

#### 指定时间范围

adb logcat -v time -d -t '2023-01-01 00:00:00' > logcat.txt
通过 -t 参数指定保存日志的时间范围，上述例子保存从指定时间到现在的日志。

#### 保存指定级别的日志
adb logcat *:E > logcat.txt
通过 *:E 过滤保存只包含错误级别的日志。可以使用 *:D（调试）、 *:I（信息）、 *:W（警告）等。

>> 请注意，以上命令中的 logcat.txt 是保存日志的文件名，你可以根据需要自定义文件名和保存路径。

日志等级，优先级从低到高分为以下几种：

V——Verbose（最低等级，开发调试中的一些详细信息，仅在开发中使用，不可再发布产品中）

D——Debug（调试，用于调试的信息，可以在发布产品中关闭，比较常见）

I——info（信息，一般提示性的信息）

W——Warning（警告）

E——Error（错误，已经出现可影响运行的错误，比如应用crash时输出的日志）

在 E级别中可以搜索这个关键字：fatal exception

ANR全名Application Not Responding，也就是应用无响应当操作在一段时间内系统无法处理时，系统层面会弹出ANR对话框

在日志中查询：ANR in

在查到ANR in 之后 上一行会有



## 设备的shell界面
#### 进入
adb shell
多个设备情况下：adb -s <设备序列号> shell
#### 退出
exit

## adb wifi连接
adb connect <device-ip-address>
adb disconnect 127.0.0.1:26944

## adb 模拟按键
adb 命令代替键盘操作，不同的 keycode 能实现不同的功能
adb shell input keyevent

https://developer.android.com/reference/android/view/KeyEvent

## 截屏 adb shell screencap -p /sdcard/sc.png
屏幕截图

## 录屏 adb shell screenrecord /sdcard/filename.mp4
录制 mp4 格式的视频保存到 /sdcard
