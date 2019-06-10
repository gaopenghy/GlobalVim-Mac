# GlobalVim

二进制dmg包: [GlobolVim.dmg](https://github.com/einsxiao/GlobalVim-Mac/blob/master/GlobalVim.dmg?raw=true)

程序键盘监听需要额外权限, 使用python可以使用root权限, 而二进制安装需要将程序添加到 System Preferences > Security & Privacy > Privacy > Accessibility 列表中.

GlobalVim能让您在任意环境下使用vim模式编辑。强大易用的GeeKey热键方案能提供丰富灵活的键盘定制和键盘编程能力，让您从从容处理大量的重复输入/操作。

## vim模式 —— 把所有辑器和输入框都变成vim

GlobalVim的vim模式并不只是简单的vim键位映射，它还支持vim的各种模式以及常用命令：

#### vim模式在任何编辑器和输入框中均生效。
#### vim模式支持寄存器机制，支持录制包含键盘和鼠标事件的广义宏。
#### vim模式表达式寄存器“= 上可对python表达式求值。
#### vim模式支持完全的的正则表达式替换功能



### vim常用操作，入门介绍（可参考详细的vim教程）


#### normal 常规模式
在启动vim模式后，vim所在模式即为normal模式。该模式下我们可以通过由字符或字符组合命令实现光标移动或者编辑操作。
normal模式不能直接输入。该模式下按i即可进入插入模式。

#### insert 插入模式
normal模式下，按下 i/a 键进入插入模式，可以在当前模式插入字符，插入模式下，按esc进入normal模式
插入模式与常用的无模式编辑的状态一致。

#### visual 可视模式
在normal模式下，按 v 即可进入visual模式，然后移动光标选择范围。visual模式下，按 v 或者 esc 退出到 normal 模式。
visual模式下，可对选中的范围执行正则替换命令

#### command 命令模式
在normal或者visual模式下，按：进入命令模式，光标在提示窗口处激活，处于输入命令状态。
按esc取消当前命令。
按enter执行当前命令。

GlobalVim支持vim大部分常用命令

### 寄存器
GlobalVim支持以下寄存器

""      默认寄存器
"=     表达式寄存器 "=
"a-z  命名寄存器 
"A-Z 追加寄存器
"0     拷贝寄存器
"1-9  删除寄存器     

查看寄存器值命令：    reg
搜索(调用当前环境的搜索功能）：  /

#### 正则替换
vim模式支持正则替换，
替换命令支持范围指定，支持偏移量，不支持 c 标志
替换当前行：
```
:s/xx/yy/  或者 :.s/xx/yy/gi
```
替换当前后前后3行：
```
:.-3,.+3s/xx/yy/g
```
替换全文：
```
:%s/xx/yy/g
```

#### "=表达式寄存器
表达式寄存器支持对python表达式求值：
在当前位置插入0-99的序列
```
“=' '.join( map(str, range(100) ) )【回车】p
```

### vim模式开启/关闭

通过在程序面板：单击 v 键 
通过快捷键：GeeKey+v （需要开启geekey热键）

### vim模式特殊设定

在normal状态下，按下esc键会向系统发送esc，而visual和insert模式下，esc会被拦截，vim状态返回normal状态。
基于windows下普遍的输入特性，append(a) 命令不在表示在当前字符之后插入 而是和 insert(i) 命令一样都是在当前位置插入。
为了大部分输入环境的行为一致，GlobalVim不支持r/R操作。

#### 对中文输入的特别支持

命令模式下，按键事件会先被GlobalVim捕获，不会发送给输入法。

## GeeKey 热键

GeeKey方案提供了强大的快捷键方案，让日常重复的输入工作变得更容易。


GeeKey热键支持两种模式：
1. 长按阻塞, 短按状态下，GeeKey行使原按键功能。长按或者组合键则阻塞原按键功能。
2. 阻塞，始终阻塞GeeKey原按键功能。

通过热键，最常用编辑操作（上下左右，Home/End，PageUp/PageDown）都不用移动手掌，只需要GeeKey+相应按键即可完成。
CapsLock 与 Esc, ~ , Tab, Shift, Ctrl, Win Alt 的按键位置可以通过程序面板进行交换（但需要以管理员模式运行程序才能操作，重启生效）。其余与热键连用的映射则可以随时通过相应方式方便地进行修改。

GeeKey新版本对空格档和录制功能键盘操作序列进行了优化，取消原来以复杂组合按键的形式，代之以类vim的按键序列的形式。

### 空档功能
GeeKey+space 【x】&        &-可以触发x的空挡绑定

### 录制操作序列
GeeKey+q  【x】  开始录制绑定到x的操作宏
GeeKey+q  space 【x】  开始录制绑定到x的空挡的操作宏

### 前置倍增操作算符

GeeKey+Space  【N】  【X】&        &-操作X重复操作N次

## 其它

### vim模式命令自定义

GlobalVim定制自由度很大。软件启动的所有配置信息都在文件 %安装文件夹%/config/default.ini 中。
当配置出现错误，软件不能启动时，用户需要删除default.ini，并重启软件。
配置项的内容可以通过宏录制来得到。录制结果的第二个参数为重放速率，0为无限快，1为原样速率。

### normal模式 自定义命令
修改default.ini中的vim_map_【按键序列】::

### 命令模式 自定义命令
修改default.ini中的vim_cmd_map_【命令名字】::

用户修改配置文件之后，需要重新载入才能生效，否则配置文件的修改会被覆盖。

### 修复鼠标硬件错误导致的错误双击
GlobalVim窗口 选项>配置 中可以设置 修复 鼠标双击硬件错误
当勾选此项时，鼠标左键抬起操作引发的额外左键按下抬起操作会被忽略。



### 已知问题
键盘numlock开启，可能会导致vim模式启动后，shift一直按下的情况

### 当出现键盘状态错误时
点击主界面左上方Clear按键，可以重置所有按键的状态。

### 升级须知
当用户升级后，新功能不能使用，或者软件不能启动时，可删除用户家目录下的GlobalVim/default.ini文件，然后重启

3.2.1.0&    &增加部分vim指令, 修复指示器颜色bug, vim常规模式F1-12功能按键直接放行
3.1.2.0&    &修复vim宏和 GeeKey宏bug
3.1.1.0&    &修复按键事件丢失bug，GeeKey可以选择任意多个按键
2019.05.17&   &取消取色器功能，增加状态重设按钮用于键盘状态错误时，重新设置状态。
2019.05.16.2&   &修复当以Esc为GeeKey时候与vim模式的冲突。
2019.05.16.1&   &增加GeeKey长短按模式。
2019.05.16&   &寄存器鲁棒性加强，visual模式替换bug修复，支持GeeKey热键自定义。移除安装文件权限要求。
2019.05.14&   &修复寄存器bug，增加正则替换功能，增加命令模式中文支持。
2019.05.11&   &添加寄存器机制,支持宏录制, 支持命令reg, register。
2019.05.07&   &GlobalVim模式查找命令修改。
