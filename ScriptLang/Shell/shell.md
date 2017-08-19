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

### 2.1 正则表达式

#### Basic Regex

+ `[``]` 用于指定某类字符, 如`[1234]`指代`1234`中的一个数
+ `^`在`[]`中使用, 如`[^<list>]`表示除了`[<list>]`外的字符
+ `-`用于`[]`中, 如`[0-9]`指代`0-9`中的一个数, `[0-z]`指代所有数字与字母, `[ascii[i]-ascii[j]]`指代位于两者间的`ASCII`字符
+ `.`用于指代除了换行符外的任意字符
+ `\{<num1>,<num2>\}`指代一个或者一类或者一组字符`<num1>-<num2>`次
+ `*`指代一个或者一类或者一组字符任意次[0, infity], 等价与`\{0,\}`
+ `\+`指代一个或者一类或者一组字符不少与一次, 等价与`\{1,\}`
+ `?`指代一个或者一类或者一组字符零次或者一次, 等价与`\{0,1\)`
+ `\(``\)`用与分组, 如`\(.*\)`, 在此分组的后面可以使用`\<num>`来表示此分组所匹配到内容(用于匹配或者替换, 第一个分组为`\1`, 以此类推
+ `\|`用于在`\(\)`中多选
+ `\<``\>`分别指代空白的左右边缘

#### Extend Regex

+ `(`, `)`, `{`, `}`, `\?`, `+`, `\|`分别表示**Basic Regex**中的`\(`, `\)`, `\{`, `\}`, `?`, `\+`, `|`

#### 一些字符族

+ `[:almum:]` == 数字和字母
+ `[:alpha:]` == 字母
+ `[:lower:]` == 小写字母
+ `[:upper:]` == 大写字母
+ `[:digit:]` == 数字
+ `[:xdigit:]` == `[0-9A-Fa-f]` 需要使用`[]`
+ `[:punct:]` == 标点符号(`! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ \` { | } ~`)
+ `[:blank:]` == 空白(空格, 制表)
+ `[:cntrl:]` == 控制字符(000-037, 177<del>)
+ `[:graph:]` == `[:almum:]` + `[:punct:]` + `空格`
+ `[:print:]` == `[:almum:]` + `[:punct:]`
+ `[:space:]` == tab, newline, vertical tab, form feed, carriage return, space

### 2.2 grep

#### 基本的选项

**命令格式:**  
`grep [OPTION] ... PATTERN [FILE] ...`

+ `PATTERN` 可以使用`-e | --regex | -f | --file |`来指定
+ 如果未输入文件或者使用管道输入, 则默认标准输入
+ 文件的指定可以使用通配符, 如`*`表示当前目录下的所有文件(`*`不可表示`/`), `*/*`表示下级目录下的所有文件

|选项|简介|
|:----:|-----|
|` -e | --regex `|正则表达式|
|`-f | --file` | 指定**Regex Pattern**文件 `-f=<file>` |
|`-E` | 使用`Extend Regex`|
|`-G` | 使用`Basic Regex` 默认|
|`-P` | 使用`Perl Regex`|
|`-s | --no-messages` | 不输出错误信息 |
|`-n  | --line-number`| 输出行号 |
|`-o | only-matching` | 只输出匹配部分 |
|`--include`|需要匹配的文件名**File_Pattern**|
|`--exclude`|排除的文件名**File_Pattern**|

#### 基本的使用

``` bash
# 匹配一级二级三级目录下的文件
grep -s -n -e "^.*google" * */* */*/*
```

### 2.3 sed
