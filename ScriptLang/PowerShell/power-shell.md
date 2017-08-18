[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">PowerShell</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [1. 基本的PowerShell命令](#1.baspow)
    * [1.1 文件和帮助](#1.1)
* [2. PowerShell的语法](2.synpow)
    * [2.1 选择结构](#2.1)
    * [2.2 循环结构](#2.2)
    * [2.3 比较操作](#2.3)

<h2 name="1"><span style="color: rgb(0,110,110)">1. 基本的PowerShell命令</span></h2>

<h3 name="1.1"><span style="color: rgb(110,110,0)">1.1 文件和帮助</span></h3>

``` powershell
# ls,dir
Get-ChildItem [Path]
# 获得帮助
Get-Help <cmdlet-name> [-Online]
```

<h2 name="2"><span style="color: rgb(0,110,110)">2. PowerShell的语法</span></h2>

<h3 name="2.1"><span style="color: rgb(110,110,0)">2.1 选择结构</span></h3>

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

<h3 name="2.2"><span style="color: rgb(110,110,0)">2.1 循环结构</span></h3>

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

<h3 name="2.3"><span style="color: rgb(110,110,0)">2.3 比较操作</span></h3>

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
