---
title: CSharpLua
categories: Tools
tags: Charp Lua
date: 2021-06-17 12:00:00
toc: true
---


# CSharpLua 

一个翻译c#为Lua的工具 
Git地址[Charp.lua](https://github.com/yanghuan/CSharp.lua.git)

## 参数

```

D:\>dotnet CSharp.Lua.Launcher.dll -h
Usage: CSharp.lua [-s srcfolder] [-d dstfolder]
Arguments
-s              : can be a directory where all cs files will be compiled, or a list of files, using ';' or ',' to separate
-d              : destination directory, will put the out lua files

Options
-h              : show the help message and exit
-l              : libraries referenced, use ';' to separate
                  if the librarie is a module, whitch is compield by CSharp.lua with -module arguemnt, the last character needs to be '!' in order to mark  

-m              : meta files, like System.xml, use ';' to separate
-csc            : csc.exe command argumnets, use ' ' or '\t' to separate

-c              : support classic lua version(5.1), default support 5.3
-a              : attributes need to export, use ';' to separate, if ""-a"" only, all attributes whill be exported
-e              : enums need to export, use ';' to separate, if ""-e"" only, all enums will be exported
-ei             : enums is represented by a variable reference rather than a constant value, need to be used with -e
-p              : do not use debug.setmetatable, in some Addon/Plugin environment debug object cannot be used
-metadata       : export all metadata, use @CSharpLua.Metadata annotations for precise control
-module         : the currently compiled assembly needs to be referenced, it's useful for multiple module compiled
-inline-property: inline some single-line properties
-include        : the root directory of the CoreSystem library, adds all the dependencies to a single file named out.lua
-noconcurrent   : close concurrent compile

```

打开 CSharp.lua.sln 
自己可编译 我这里选择 Release Build

![截图](/images/csharplua/2.png)

红色标记处为编译成功后
 

这里新建一个文件夹讲红色标记文件拷出

![截图](/images/csharplua/3.png)

cmd测试： dotnet CSharp.lua.Launcher.dll -h

![截图](/images/csharplua/1.png)
