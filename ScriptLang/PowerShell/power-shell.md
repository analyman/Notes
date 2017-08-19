[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">PowerShell</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [1. 基本的PowerShell命令](#1-基本的powershell命令)
    * [1.1 获得Cmdlet命令的帮助](#11-获得cmdlet的帮助)
    * [1.2 新建与删除文件项目](#12-新建与删除文件项目)
    * [1.3 环境变量](#13-环境变量)

* [2. PowerShell的语法](2-powershell的语法)
    * [2.1 选择结构](#21-选择结构)
    * [2.2 循环结构](#22-循环结构)
    * [2.3 比较操作](#23-比较操作)
    * [2.4 变量及其声明](#24-变量及其声明)

## 1. 基本的PowerShell命令

### 1.1 获得Cmdlet的帮助

+ `Get-Help <cmdlet-name>`将在屏幕打印出简短的此`cmdlet`的帮助信息
+ `Get-Help <cmdlet-name> -online`将使用浏览器打开相应`Cmdlet`的详细帮助


### 1.2 新建与删除文件项目

+ `Get-ChildItem`用于获取子项目
+ `New-Item` 用于新建项目, 使用`-ItemType <directory | file>`指定项目的类型
+ `Remove-Item`用于删除项目
+ `Set-Localtion`用于指定当前的位置

**示例:**

``` powershell
Get-ChildItem -Path .      # 将返回一个`System.IO.FileSystemInfo`的数组, 并在屏幕上打印出来

New-Item -Path . -Name Google -ItemType "directory"     #新建一个名为Google的目录
New-Item -Path ./Google -ItemType "directory"           #和上一个命令产生相同的效果

Remove-Item -Path <path>    #删除一个项目

Set-Localtion $HOME         #指定当前目录为$HOME 
```

### 1.3 环境变量

**PowerShell**使用`Get-Item Env:`获取所有的环境变量, 并且返回一个`System.Collections.DictionaryEntry`对象, 使用`.Key`和`Value`属性可以取得一个字符串数组.  

+ 在获取指定的环境变量时, 可以使用`$Env:PATH`(`System.string`)
+ 同时可以使用`Get-Item Env:PATH`, 返回一个`System.Collections.DictionaryEntry`对象, 使用`Value`属性可以得到和`$Env:PATH`相同的字符串
+ 在获取不存在的环境变量时, `$Env:PATH`形式返回一个空值, `Get-Item Env:PATH`抛出一个错误信息

## 2. PowerShell的语法

### 2.1 选择结构

``` powershell
# if ... elseif ... else
if (condition1) {
	...
} elseif(conditon2) {
	...
} else {
	...
}

# switch
switch (expression) {
    const1 {
    ...
    }
    const2 {
    ...
    }
    ...
    default {
    ...
    }
}
# 单次执行,不需要break,break
# break,continue和shell没什么区别
```

### 2.1 循环结构

``` powershell
# for
for(;;;){
...
}
# 和c没什么区别


# Do ... While
Do{
...
}while(condition)
# 和c什么区别

# Do ... Until
Do{
	...
}Until(condition)
# 相似的

#foreach
```

### 2.3 比较操作

|Operator|Descripton|
|--------|----------|
|-eq|equals|
|-ne|not equal|
|-gt|greater than|
|-ge|greater than or equal to|
|-lt|less than|
|-le|less than or equal to|
|-like|wild card comparison|
|-notlike|wild card comparison|
|-match|regex comparison|
|-notmatch|regex comparison|

**示例:**

``` markdown
$true               # return True
$false              # return False

"me" -eq "me"       # return True
$SOMEVAR = "string"
$SOMEVAR -ne "ingstr"       # return True

# 其他也是相类似的
```
