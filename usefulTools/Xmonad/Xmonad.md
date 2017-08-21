## Xmonad

## Table of contents

* [1. Short Ref](#1-short-ref)
    * [1.1 简介](#11-简介)
    * [1.2 安装](#12-安装)
    * [1.3 简单使用](#13-简单使用)
    * [1.4 xmobar](#14-xmobar)

* [2. xmonad.hs](#2-xmonadhs)

## 1. Short Ref

### 1.1 简介

[官方简介](http://xmonad.org/about.html)  

**About:**  

Xmonad is a tiling window manager for X. Windows are 
arranged automatically to tile the screen without gaps 
or overlap, maximising screen use. All features of 
the window manager are accessible from the keyboard
: a mouse is strictly optional. Xmonad is written and 
extensible in Haskell. Custom layout algorithms, and 
other extensions, may be written by the user in config 
files. Layouts are applied dynamically, and different 
layouts may be used on each workspace. A guiding principle 
of the user interface is predictability: users should 
know in advance precisely the window arrangement that 
will result from any action, leading to an intuitive 
user interface.

### 1.2 安装

+ xmonad
+ xmobar
+ dmenu
+ gmrun

### 1.3 简单使用

+ **xmonad**的有9个工作区, 每个打开了窗口的工作区都有一个`master window`
+ `master window`在多个窗口同时可见的状态下以垂直和水平占据屏幕的方式

**快捷列表:**  

|快捷键|描述|
|:----:|----|
|<kbd>mod</kbd><kbd>shift</kbd><kbd>return</kbd>|打开一个新的`Term`, 并且将此窗口设为`master window`|
|<kbd>mod</kbd><kbd>return</kbd>|将当前`focus`窗口设置为`master window`|
|<kbd>mod</kbd><kbd>space</kbd>|循环切换当前窗口排布(独占, 垂直, 水平)|
|<kbd>mod</kbd><kbd>shift</kbd><kbd>space</kbd>|切换当前窗口布局为默认|
|<kbd>mod</kbd><kbd>shift</kbd><kbd>c</kbd>|关闭当前窗口|
|<kbd>mod</kbd><kbd>shift</kbd><kbd>q</kbd>|关闭xmond|
|<kbd>mod</kbd><kbd>p</kbd>|如果安装了`dmenu`, <kbd>mod</kbd><kbd>p</kbd>会在`Xmonad`顶端上打开个输入栏用于打开应用|
|<kbd>mod</kbd><kbd>shift</kbd><kbd>p</kbd>|如果安装了`gmrun`, 在屏幕中央打开输入栏用于打开应用|
|<kbd>mod</kbd><kbd>number</kbd>|<kbd>number</kbd>为`1-9`用于在`1-9`工作区切换|
|<kbd>mod</kbd><kbd>shift</kbd><kbd>number</kbd>|<kbd>number</kbd>为`1-9`, 将当前工作区的`master window`切换到<kbd>number</kbd>工作区(未切换工作区)|
|<kbd>mod</kbd><kbd>j</kbd>|可以在当前工作区切换`focus window`|
|<kbd>mod</kbd><kbd>k</kbd>|可以在当前工作区切换`focus window`|
|<kbd>mod</kbd><kbd>comma</kbd>|增加与`master window`平齐的窗口|
|<kbd>mod</kbd><kbd>period</kbd>|减少与`master window`平齐的窗口|
|<kbd>mod</kbd><kbd>shift</kbd><kbd>j</kbd>|切换窗口顺序|
|<kbd>mod</kbd><kbd>shift</kbd><kbd>k</kbd>|切换窗口顺序|
|<kbd>mod</kbd><kbd>h</kbd>|减小`master window`所占屏幕比例|
|<kbd>mod</kbd><kbd>l</kbd>|增加`master window`所占屏幕比例|
|<kbd>mod</kbd><kbd>button</kbd>|同时拖动窗口使其变为悬浮模式|
|<kbd>mod</kbd><kbd>t</kbd>|将窗口平铺|

### 1.4 xmobar
