---
title: JetBrains快捷键
categories: Tools
tags: JetBrains
date: 2023-12-22 12:00:00
toc: true
---


==Ctrl==

Ctrl + A 全选
Ctrl + B 快速打开光标处的类或方法(等同于 Ctrl + 鼠标点击)
Ctrl + C 复制（不选定内容的话默认会复制光标所在整行）
Ctrl + D 复制行或是块（不选定内容的话默认复制当前行到下一行）
Ctrl + E 最近打开的文件
Ctrl + F 当前代码中查找
Ctrl + G 跳到指定行
Ctrl + H 显示类层次图
Ctrl + J 自动代码提示（提示的是自己定义的代码格式）
Ctrl + K git 或 VCS 提交项目
Ctrl + L 查看变量的下一个位置（需要先 Ctrl + F 激活查找）
Ctrl + M 将光标所在的行移到屏幕中间（连同光标一块移动到屏幕中间）
Ctrl + N 查找类
Ctrl + O 选择可覆盖/继承的方法
Ctrl + P 方法参数提示显示（只显示入参的）
Ctrl + Q 鼠标放在变量/类名/方法名等上面（也可以在提示补充的时候按），显示文档内容。（入参，返回值，所属模块等）
         同类似的功能还有一个 Ctrl + Shift + I，直接显示函数定义处的内容（所以 Ctrl + P，Ctrl + Q 和 Ctrl + Shift + I 
         的查看是一个渐进详细的过程）
Ctrl + R 替换
Ctrl + S 保存
Ctrl + T git 或 VCS 更新项目
Ctrl + U 前往父类的方法/父类
Ctrl + V 粘贴
Ctrl + W 选中光标所在的单词 ，连续按会有其他效果 (相反的是Ctrl+Shift+W)
ctrl + X 剪切行
Ctrl + Y 删除行
Ctrl + Z 撤销


Ctrl + F1 显示错误
Ctrl + F3 调转到所选中的词的下一个同名位置
Ctrl + F7 Find Usages in File（可以同时查找多个变量）
Ctrl + F8 打开或关闭行断点
Ctrl + F9 编译
Ctrl + F11 弹出一个小框来指定式添加书签(可以对文件或文件夹起作用)
Ctrl + F12 当前编辑的文件中快速导航(可以直接键入字母，会筛选你输入的来匹配对应是否有的方法，来快速定位)(类似结构图)
Ctrl + Tab 编辑窗口切换 (如果在切换的过程又加按上 delete,则是关闭对应选中的窗口) 
Ctrl + delete 删除光标后面的单词（delete 只是删除单个字符哟！）
Ctrl + home/end 跳到文件头文件尾
Ctrl + BackSpace 删除光标前面的单词
Ctrl + [ 或 ] 移动光标到块的初/末括号地方
Ctrl + / 或 Ctrl+Shift+/ 注释（// 或者/*…*/ ）
Ctrl + 1，2，3，4…. 快速定位到书签代码处(必须先 Ctrl + Shift + 1,2,3,4…添加书签
Ctrl + 小键盘+/- 折叠/展开代码
Ctrl + 鼠标单击编辑窗口的文件标题 弹出该文件路径,可以通过这个打开文件所在地方(相当于Ctrl + Alt + F12)
Ctrl + ← 或 → 光标跳到上/下个单词
Ctrl + ↑ 或 ↓ 相当于你用鼠标滑滚轮(为了方便鼠标党)
Ctrl + ` 快速切换常用设置

==Alt==

Alt + 1 切换到 Project 模块
Alt + 2 切换到 Favorites 模块
Alt + 3 切换到 Find 模块
Alt + 4 切换到 Run 模块
Alt + 5 切换到 Debug 模块
Alt + 6 切换到 Problems 模块
Alt + 7 切换到 Structure 模块
Alt + 8 切换到 Services 模块
Alt + 9 切换到 Git 模块
Alt + Q Context Info（上下文信息，可以快速帮你定位当前位置的上下文）
Alt + F1 弹出文件选择目标，这个很好用的
Alt + F2 多个浏览器预览
Alt + F3 选中文本，逐个往下查找相同文本，并高亮显示（类似于 Ctrl + C， Ctrl + F）。
Alt + F4 关闭软件
Alt + F7 查看该方法/变量/类被调用的地方
Alt + F8 在debug 的状态下，选中某些变量或是对象，按此快捷键弹出可输入变量、方法的调试框，指定查看该内容的 debug 情况
Alt + F12 进入终端
Alt + Home 跳到文件导航bar
Alt + Insert 生成代码(如 get,set 方法,构造函数等)
Alt + ← 或 → 切换当前打开的代码文件视图
Alt + ↑ 或 ↓ 在方法间快速移动定位
Alt + Enter 快速修复(可以用来导入单个包)
Alt + ` VCS快捷选项

==Shift==

Shift + F6  重构：重新命名
Shift + F9 debug 当前程序，相当于点击 debug 按钮
Shift + F10 Run(运行)当前程序，相当于点击 run 按钮
Shift + F11 查看书签
Shift + end 选中从光标到end 处
Shift + home 选中从光标到 home 处
Shift + Enter 光标所在行下空出一行，光标跳下
Shift + 单击 可以关闭文件
Shift + 滚轮 横向滚动轴滚动(非常强大，现在好多文本编辑器都默认有这个功能了)

==Ctrl+Alt==

Ctrl + Alt + A git add (需要先配置 git)
Ctrl + Alt + B 跳到具体的实现方法，查找接口/抽象方法的具体实现很好用(相反行为的快捷键是Ctrl+b)
Ctrl + Alt + C 快速引进一个常量
Ctrl + Alt + F 快速引进一个实例变量
Ctrl + Alt + I 选中部分自动缩进行（有点类似格式化，但是只是整理行格式而已）
Ctrl + Alt + L 格式化代码
Ctrl + Alt + M 方法抽取/重构
Ctrl + Alt + N 将方法内联化
Ctrl + Alt + O 优化导入的类和包
Ctrl + Alt + P 参数抽取
Ctrl + Alt + S 快速打开设置 Settings
Ctrl + Alt + T 选中的地方代码环绕提示 例如 ：try/catch 选中的一块代码
Ctrl + Alt + V 快速引进一个变量名
Ctrl + Alt + W 关闭所有编辑的快捷键（自己添加，再 close all）
Ctrl + Alt + Y 从磁盘重载
Ctrl + Alt + Z git rollback (需要先配置 git)
Ctrl + Alt + F5 Attach to Process
Ctrl + Alt + F7 寻找被该类或是变量被使用的地方，用弹出框的方式找出来，，也类似于 Ctrl + 鼠标 左击。跟 Alt+F7 效果一样，但是因为是弹出框，选中了一个位置就会消失。
Ctrl + Alt + F12 文件路径
Ctrl + Alt + Enter 光标所在行上空出一行，光标跳上
Ctrl + Alt + home 弹出跟当前文件有关联的文件目录(比如jsp 里面有导入几个js 和 css,这些文件就是关联文件)
Ctrl + Alt + ← 或 →  退回/前进到上一个操作的地方
Ctrl + Alt + ↑ 或 ↓ 在 Find 模式下，挑到上/下个查找的文件
Ctrl + Alt + 空格 类名或接口名提示(可能会和输入法快捷键冲突)

==Ctrl+Shift==

Ctrl + Shift + A Find Action
Ctrl + Shift + B 变量类型声明
Ctrl + Shift + C 复制当前文件磁盘路径到剪贴板
Ctrl + Shift + E 最近更改的文件
Ctrl + Shift + F 全局查找文件（通过某个词，指定要搜索的文件类型，目录。注意：这个也可能会和 Windows 的简繁切换快捷键相冲突哟！！！）
Ctrl + Shift + I 在方法名或是类名下，按此快捷键显示该方法或是类的源码结构，无需点击进去查看源码（当然了，必须是你已经导入源码的情况下才看得到）
Ctrl + Shift + J 自动将下一行合并到当前行末尾
Ctrl + Shift + K git push
Ctrl + Shift + M 光标位置在括号前后切换
Ctrl + Shift + N 通过输入文件名和行号（可以输入部分名称，支持模糊）来定位查找文件
Double + Shift (快速双击 Shift)搜索最近打开的文件，我也是经常误触才发现他这个功能
Ctrl + Shift + P 表达式的类型信息
Ctrl + Shift + R 搜索指定范围文件，替换文字
Ctrl + Shift + T 如果在常规类下按它，弹出已写好的，可选择的对应 Test 类，如果在该 Test 类下按它，则直接回到源类。
Ctrl + Shift + U // 大/小写都是这个快捷键
Ctrl + Shift + V 粘贴最近复制过的一些信息（从历史记录粘贴）
Ctrl + Shift + W Ctrl + W 的逆向操作
Ctrl + Shift + Y Code With Me
Ctrl + Shift + Z 取消撤销（恢复上一次操作）
Ctrl + Shift + F7 高亮显示所有该选中文本，按 Esc 高亮消失。
Ctrl + Shift + F8 查看断点
Ctrl + Shift + F12 编辑器全屏
Ctrl + Shift + Del 删除环绕的标签
Ctrl + Shift + 1，2，3… 快速添加书签
Ctrl + Shift + Space 自动补全代码（智能提示）
Ctrl + Shift + Enter 自动给末尾加;完成代码
Ctrl + Shift + ↑ 或 ↓ 移动光标所在 statement 域移动到上/下 (Alt + Shift + ↑ 或 ↓ 移动光标所在行到上/下)
Ctrl + Shift + [ 或 ] 选中从光标所在位置到它的父级区域(界面上层导航可能更开)
Ctrl + Shift + 小键盘 + 或 – 折叠/展开所有代码
Ctrl + Shift + ← 或 →  选中临边左/右的单词或是符号
Ctrl + Shift + / 块注释（使用 =begin block =end 进行注释）
Ctrl + Shift + Backspace(退格)  回到上次修改的地方(跟 Ctrl+Alt+左右方向键不一样的地方是，只回退到修改的地方，而不是过去光标放的地方)

==Alt+Shift==

Alt + Shfit + B 查看当前行对应的 commit 提交记录详情
Alt + Shift + C 查看最近操作项目的变化情况列表(在版本控制下，显示比较缓慢)
Alt + Shift + F 添加到收藏夹
Alt + Shift + G 进入多行选取模式并将光标放在所选行的末尾(简单理解就是，选中多行之后使用这个快捷键，你可以同时往这多行末尾添加相同的内容，感觉和列模式有些像，但列模式不同行的光标都在同一列，这块不同行的光标可以不在同一列 —— 都在各自行的末尾)
Alt + Shift + J 取消选中（有点像 Ctrl + Alt + Shift + J 的逆操作，不过 Alt + Shift + J 每次只取消选中一个地方）
Alt + Shift + L 加载上下文
Alt + Shift + N 添加任务
Alt + Shift + S 保存上下文
Alt + Shift + T 切换任务
Alt + Shift + U 驼峰命名法和蛇形命名法切换(需要先选中方法名对应的字符串)
Alt + Shift + W 关闭活跃任务
Alt + Shift + X 清理上下文
Alt + Shift + F9  弹出debug 运行菜单，提供选择性debug 哪个(这个需要自己尝试下，按后会有弹出框，记得查看)
Alt + Shift + F10 弹出run 菜单，提供选择性run 哪个(这个需要自己尝试下，按后会有弹出框，记得查看)
Alt + Shift + ↑ 或 ↓ 移动光标所在行到上/下
Alt + Shift + Insert 切换到列选择模式（再次可切换回行选择模式）
Alt + Shift + 鼠标左键单击不放,拖动 可以直接方块区域选择（也叫列选或块选，批量修改列的时候很有用）

==Ctrl+Alt+Shift==  （用得不多，因为总感觉手指头不太够用）

Ctrl + Alt + Shift + C 复制参考信息(方法的继承关系，或文件相对路径及当前所在行号)
Ctrl + Alt + Shift + D 以 UML 的形式显示改动
Ctrl + Alt + Shift + L 格式化文件
Ctrl + Alt + Shift + J 选中所有用到当前方法的地方（这个用来统一修改函数名和调用点函数名之类的很有用，就不用单独一个个去修改了）
Ctrl + Alt + Shift + N 查找类中的方法或变量
Ctrl + Alt + Shift + T 选择重构方式
Ctrl + Alt + Shift + V 不带格式的简单黏贴
Ctrl + Alt + Shift + X Deployment -> Upload to (上传文件改动到指定服务器，对于将本地文件改动快速同步到远端服务器的时候很好用)
Ctrl + Alt + Shift + F7 Find Usages Settings
Ctrl + Alt + Shift + F8 添加临时行断点
