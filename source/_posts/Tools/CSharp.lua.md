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

### 编译源码

打开 CSharp.lua.sln 
自己可编译 我这里选择 Release Build

![截图](/images/csharplua/2.png)

红色标记处为编译成功后
 

这里新建一个文件夹将上图红色标记文件拷出

![截图](/images/csharplua/3.png)

cmd测试： dotnet CSharp.lua.Launcher.dll -h

![截图](/images/csharplua/1.png)


### 编译c# 工程

lua 使用的 5.3 版本

新建 CompileScript Console工程,新增文件夹Core
创建测试脚本 

Test.cs
```
using System;

namespace CompileScript.Core
{
    public class Test
    {
        public int a;
        public int b;

        public Test()
        {
            
        }

        public void Debug()
        {
            Console.WriteLine(a + b);
        }

    }
    
    
}

```
TestClass2.cs

```
namespace CompileScript.Core
{
    class TestClass2
    {
        public void Debug()
        {
            Test t = new Test();
            t.Debug();
        }

    }
}

```

> 命令行： dotnet CSharp.lua.Launcher.dll -s ../CompileScript/CompileScript/CompileScript/Core -d ../Export


在Export 下创建lua工程
将![截图](/images/csharplua/4.png) copy 到工程，新建main.lua

```
require("All")()
require("manifest")()

local baseTime = System.DateTime(1970, 1, 1)
print(baseTime:ToString())

local t = CompileScript.Core.Test()
t.a = 10
t:Debug()
```
运行 可以

将![截图](/images/csharplua/5.png) copy 到工程，新建main.lua


### 第三方库引用

CompileScript 工程添加Newtonsoft库

```
using System;
using Newtonsoft.Json;
namespace CompileScript.Core
{
    public class Test
    {
        public int a;
        public int b;

        public Test()
        {
            
        }

        public void Debug()
        {
          
            Console.WriteLine(a + b);

            Console.WriteLine(JsonConvert.SerializeObject(this));
        }

    }
    
}

```
编译指令

> G:\Learning\CsharpLua\CSharpLuaTools>dotnet CSharp.lua.Launcher.dll -s ../CompileScript/CompileScript/CompileScript/Core -d ../Export -l ../3rd/Newtonsoft.Json.dll

运行代码 报错

![截图](/images/csharplua/6.png)


> 这里第三方库dll的实现需要自己适配

这里适配 NewtonsoftJson.JsonConvert.SerializeObject(this)


新建 NewtonsoftJson.lua


```
Newtonsoft = {}
Newtonsoft.Json = {}
Newtonsoft.Json.JsonConvert = {}
Newtonsoft.Json.JsonConvert.SerializeObject = function (obj)
     return "todo"
end

return Newtonsoft
```

return "todo"可修改为lua相关的json库，比如cjson


### 注意事项

* 第三方库的依赖尽量少依赖
* 如果有需要查看适配结果，多测试
* 核心库CoreSystem.Lua 文件夹下的适配了多数System。

### Tip

如果手写Lua 需要调用翻译的lua class 时，如果不知道如何new对象等，参考TestClass2, 创建一个专门的class 用来测试 翻译出的如何new 对象。


### 适配踩坑

Unity工程适配 ToLua支持，Xlua 实际测试不支持，如果在Xlua 使用，不得依赖UnityEngine 相关库。

