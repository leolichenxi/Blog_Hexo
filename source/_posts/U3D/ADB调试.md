---
title: ADB调试
categories: U3D
tags: 工具
date: 2021-06-14 12:00:00
toc: true
---

## adb 链接设备
adb connect 127.0.0.1:62001
## 查看设备链接
adb devices

## 查看内存
adb shell top | grep app_name
adb shell top | grep com.bilibili.hcshjxaz
## 链接Unity

adb forward tcp:34999 localabstract:包名
