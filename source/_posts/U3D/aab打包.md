---
title: AAB
categories: AAB
tags: AAB
date: 2021-06-14 12:00:00
toc: true
---

[官方文档](https://developer.android.com/guide/app-bundle/asset-delivery)

## AndroidAppBundle
> googlePlay上一种新的上传格式，以前是传apk,现在可以传Bundle。google play通过dynamic Delevery从Bundle中现在特定的配置给用户。

## Play Asset Delivery

Play Asset Delivery (PAD) 将 app bundle 的优势带到游戏中。它允许超过 150 MB 的游戏替换旧版扩展文件 (OBB)，方法是将包含游戏所需的所有资源的单个工件发布到 Play。PAD 提供了灵活的分发模式、自动更新、压缩和增量修补功能，并且可免费使用。使用 PAD，所有资源包均在 Google Play 上托管和提供，因此您无需使用内容分发网络 (CDN) 向玩家提供游戏资源。

Play Asset Delivery 使用资源包，资源包由资源（如纹理、着色器和声音）组成，但不包含可执行代码。通过 Dynamic Delivery，您可以按照以下三种分发模式自定义如何以及何时将各个资源包下载到设备上：安装时分发、快速跟进式分发和按需分发。

#### install-time

资源包在用户安装应用时分发。这些资源包以拆分 APK（APK 集的一部分）的形式提供。它们也称为“预先”资源包；您可以在应用启动时立即使用这些资源包。这些资源包会增加 Google Play 商店上列出的应用大小。用户无法修改或删除这些资源包。

#### fast-follow 

资源包会在用户安装应用后立即自动下载；用户无需打开应用即可开始 fast-follow 下载。此类下载不会阻止用户访问应用。这些资源包会增加 Google Play 商店上列出的应用大小。

#### on-demand 

资源包会在应用运行时下载。

Google Play 商店会以归档文件（而非拆分 APK）的形式提供配置为 fast-follow 和 on-demand 的资源包。这些资源包随后会在应用的内部存储空间中展开。您可以使用 Play Core API 查询以这种方式提供的资源包的位置。应用无法假设这些文件的存在或其位置，因为它们可能会被用户删除，或由 Play Core SDK 在游戏会话之间移动。尽管这些文件可由应用写入，您也应将其视为只读文件，因为资源包补丁程序依赖于这些文件的完整性。


每个 fast-follow 和 on-demand Asset Pack 的下载大小上限为 512 MB。
所有 install-time Asset Pack 的总下载大小上限为 1 GB。
一个 Android App Bundle 中的所有 Asset Pack 的总下载大小上限为 2 GB。
一个 Android App Bundle 中最多可以使用 50 个资源包。

也就是从install-time 我们可以放比较多的重要资源

fast-follow 和 on-demand 放二级资源

我们项目目前有将近4G 的资源 最新的assetbundle（3.75G）

从PAD中可以处理将近2G的资源，仍需有将近2G的资源从cdn下载。

### PAD需要处理的工作

1. 打包时记录所有的AssetPack信息, 测试分支已经写好。（每个pack的文件和大小信息等。）加入自动打包也已改好。
2. 根据记录的pack信息 在应用启动时对PAD做资源完整检查;
3. 每个分包的PlayAssetPack的处理（分包里的assetbundle 或其它资源，需要先加载此AssetPack 再从assetPack里加载assetbundle）这里包含任何分发模式的资源。
4. 加载AssetBundle的逻辑修改这里主要是是 以及AssetPack在内存中的依赖维护。

```

  //异步加载
  PlayAssetPackRequest playAssetPackRequest = PlayAssetDelivery.RetrieveAssetPackAsync(packName);
   //异步加载
  AssetBundleCreateRequest request = playAssetPackRequest.LoadAssetBundleAsync(abPath)

  //目前的加assetbundle     
  AssetBundleCreateRequest request = AssetBundle.LoadFromFileAsync(AssetBundleFullPath);

```
### 在 Play 上测试 app bundle
https://developer.android.com/guide/app-bundle/test

### 本地测试流程

[官方测试参考文档](https://developer.android.com/guide/app-bundle/test)

[下载BundleTool](https://github.com/google/bundletool/releases)


将aab装成课本第测试的apks 此步骤以自动加入到打包流程。
```
bundletool build-apks --local-testing
  --bundle my_app.aab
  --output my_app.apks
```

安装到测试机(模拟器需要abd 先链接模拟器，比如夜神模拟器：adb connect 127.0.0.1:62001)

```
bundletool install-apks --apks my_app.apks
```