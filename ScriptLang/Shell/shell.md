[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">SHELL</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [1. 语法](#1-语法)
    * [1.1 控制流](#11-控制流)
    * [1.2 test命令](#12-test命令)
    * [1.3 函数](#13-函数)
    * [1.4 输入输出重定向](#14-输入输出重定向)
* [2. 基础文本处理工具](#2-基础文本处理工具)
    * [2.1 正则表达式](#21-正则表达式)
    * [2.2 grep](#22-grep)
    * [2.3 sed](#23-sed)

## 1. 语法

### 1.1 控制流

> **if-then-elseif-then-else-fi**
``` bash
#!/usr/bin/env bash

#基本格式
if condtion1		# if-then-fi是必需有的,if-then可以在同一行用";"隔开
then
	dosth1
elseif condition2	# condition是shell command的返回值,0时表示执行
then
	dosth2
...
else
	dosthn
fi
```

> **case-in---esac语句**
``` bash
#!/usr/bin/env bash

#基本格式
case <value> in			# case语句不需要break语句跳出
const1)
	dosth1;;
const2|const3)
	dosth2;;
...
*)				# 默认的情况
	dosthn;;
esac
```

> **for语句**
``` bash
#!/usr/bin/env bash

#基本格式
for <forvar> in <STH>		# <STH>可以是:
do				#字符串,"cat ls make"
	dosth			#变量,list,list="cat ls make"
done				#文本文件,以每一行为一个变量
				#通配符的路径,以每个文件作为一个变量

				#可以通过修改IFS变量修改字符串的分割符
				#IFS=$'\n: :\t:;'
#C风格的for
for ((varinit;condit;iteration process))
do
	dosth
done
```

> **while语句**
``` bash
#!/usr/bin/env bash

#基本格式
while conditon			# easy
do
	dosth
done
```

> **until语句**
``` bash
#!/usr/bin/env bash

#基本格式
until condition			# easy
do
	dosth
done
```

> **break and continue语句**
``` bash
#!/usr/bin/env bash

# ex1				# 可以指定跳出或忽略的层数
for((i=0;i<10;i++))		# break n
do				# continue n
	if [ i -gt 7 ]
	then
		break
	fi
	echo "This is "${i}" iteration"
done
# ex2
for((i=0;i<10;i++))		# break n
do				# continue n
	if [ i -gt 7 ]
	then
		continue
	fi
	echo "This is "${i}" iteration"
done
#两个的输出一样
```

## 1. 基础文本处理工具

### 1.1 正则表达式

### 1.2 grep

### 1.3 sed
