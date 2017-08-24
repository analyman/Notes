[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">VIML</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [0. 基本操作](#0-基本操作)
    * [0.1 操作](#01-操作)
    * [0.2 Ex命令](#02-ex命令)
    * [0.3 Buffer](#03-buffer)
    * [0.4 tabPage](#04-tabpage)

* [1. VIML基本语法](#1-viml基本语法)
    * [1.1 条件语句](#11-条件语句)
    * [1.2 循环语句](#12-循环语句)
    * [1.3 函数](#13-函数)
    * [1.4 自动命令](#14-自动命令)

* [2. 变量](#2-变量)
    * [2.1 作用域](#21-作用域)
    * [2.2 种类](#22-种类)
        * [2.2.1 List](#list)
        * [2.2.2 Dictionary](#dictionary)
    * [2.3 例子](#23-例子)

* [3. 表达式](#3-表达式)

## 0. 基本操作

### 0.1 操作

### 0.2 Ex命令

### 0.3 Buffer

### 0.4 tabPage

## 1. VIML基本语法

### 1.1 条件语句

**VIML**的条件语句有`if ... [ elseif ... ] [ else ... ] endif`语句

``` vim
" if语句的例子
if has("gui_running")
    echo "Gvim is running"
else
    echo "vim run in terminal"
endif
```

### 1.2 循环语句

**VIML**的循环语句有`while ... endwhile`,`for <var> in <list> ... endfor`

``` vim
" while语句的例子
let i = 0
let Max = 100
while i < Max
    echo "The variable i is ".i
    let i = i + 1
endwhile

" for语句的例子
let list = ["li", "zhou", "wu", "wang"]
for froname in list
    echo froname
endfor
```

### 1.3 函数

**VIML**的函数定义方式和调用方式
``` vim
" 定义个函数
function s:example()
"function! s:example()        表示假如之前已经存在example()的定义，则覆盖它
    echo "This is a example function"
endfunction

" 调用函数
call s:example()
```

**函数参数**

``` vim
" 至多20个的命名参数
function s:mmp(name, age)
    echo "the name is " . a:name
    echo "the age is " . a:age
endfunction

" 可以接受不定长参数的
function s:mmpyou(...)
    echo "args list is " . a:000
    echo "first extra arg is " . a:1
endfunction

function s:mmpme(name, age, ...)
    ...
endfunction
```

+ 函数中使用`a:argn`来调用命名的参数
+ 使用`a:1 , a:2, ... `来调用额外的不定长参数
+ `a:000`表示不定长参数List

#### Lambda

**例子**

``` vim
let result = {x, y -> x * y}(22, 33)
" result = 726
```

### 1.4 自动命令

主要就是`autocmd`和`autogroup`
``` vim
" 定义一个autocmd
" au[tocmd] [group] {event} {pat} [nested] {cmd}
autocmd BufWritePost * excute ':echo "autocmd example"'

" 删除autocmd的定义
autocmd! [group] {event} {pat}          "删除匹配到<event>和<pat>的autocmd
autocmd! [group] * {pat}                "删除所有匹配<pat>的autocmd
autocmd! [group] {event}                "删除匹配到<event>的autocmd
autocmd! [group]                        "删除所有的autocmd 

" 列出autocmd的定义
autocmd [group] {event} {pat}           "列出匹配到<event>和<pat>的autocmd
autocmd [group] * {pat}                 "列出所有匹配到<pat>的autocmd
autocmd [group] {event}                 "列出匹配到<event>的autocmd
autocmd [group]                         "列出所有的autocmd 

" 总结:
"       可以看做autocmd[!] [group] [event [pat [nested] [cmd]]]
"       移除autocmd的命令就是强制将<event>或<pat>的cmd变为什么都不做
"       列出显示就是不加强制!的删除

" autogroup
" 将autocmd分组用于执行和删除
" example
augroup[!] example_group
    au ...
    au ...
augroup end
" or
au example ...
au example ...

" 移除augroup
augroup! <name>                         "删除分组及分组的autocmd

" 执行autocmd
do[autocmd] [<nomodeline>] [group] {event} [fname]
" 执行匹配到<event>的，并且在[group]中的autocmd，应用与<fname>中；
" 其中<group>和<fname>是可选的,<group>没给出默认为全部的group
" <fname>没给出默认为当前文件

" doautoa[ll]和autocmd相似，只是应用于所有buffer中
```

## 2. 变量

### 2.1 作用域

> VIMSCRIPT变量

* g:varname     全局变量
* s:varname     脚本变量
* v:varname     VIM定义变量
* w:varname     窗口变量
* t:varname     TAB变量
* b:varname     BUF变量
* l:varname     函数局部变量
* a:varname     函数参数

> OTHERS

* &varname      varname为option
* &g:varname    全局的
* &l:varname    局部的
* @varname      寄存器(register)的值
* $varname      环境变量

### 2.2 类型

**VIML**的比较特殊的变量类型有`List(列表)`,`Directionary(字典)`

#### List
``` vim
" List
let lst = ['a', 'b', 'c', 'd']

for ls in lst
    echo "the element is ".ls
endfor

" List function(函数)
add(list, element)          " add elememt to list, change the value of list
insert(list, element, index)" insert element to list before list[index], like add()
extend(list1, list2)        " like + operate
get(list, index, default)   " get the element of list by index, if index is over the list, then return default)
getline(line1,line2)        " retuen a list, from the line1 to line2 in buffer
append(lines, list)         " 将list中的元素一行一个的追加到第几行lines后面,'$'表示最后一个
index(list, indexelement)   " get the index of list by indexelement, if the indexelement isn't exist in list, return -1
len(list)                   " return the length of list
empty(list)                 " equal len(list) == 0
join(list, [seprate])       " join the all element of list into a string, and seprated by seprate(default is space), don't change the value of list
split(list, [seprate])      " reverse to join()
min(list)                   " min vaule
max(list)                   " max vaule
reverse(list)               " reverse the list, change the value of list, 反序
sort(list)                  " sort the list, change the value of list, 排序
uniq(list)                  " uniq the list, change the value of list
remove(list, index1[, index2])  "remove the element in index1 to index2, like unlet operate
filter(list, 'v:val !~ "x") " remove items with an 'x', 移除有'x'的元素

" operate of list (list的操作)
let list[0] = '0'           " 将list[0]赋为'0'
let list = list1 + list2    " list2 接在list1 后面
echo list[0]                " 首个元素
echo list[-1]               " 最后一个元素
echo list[11111]            " index过大导致vim报错,建议用get()
echo list[1:]               " 从第二个元素开始
echo list[:]                " 全部元素
let [var1, var2 ; rest] = list      " 将list中的元素赋值给var1...rest
let [var1, var2] = list             " 当list元素个数与var个数不同会报错,无论多或者是少
unlet list[index1[:index2]]         " 和remove函数一样
```

#### Dictionary

**简单赋值的例子:**

``` vim
let dict1 = {me:"my name", you:"you name"}

" empty dictionary
let dict_empty = {}
```

**在Dictionary中使用Key获取和设置Value**

``` vim
" 设定特定Key的Value
"" 第一种形式
let dict1["she"] = "she name"
"" 第二种形式
let dict1.he = "he name"

" 由Key获取Value
"" 类似于以上设置值的形式
let shename = dict1.she
let hename = dict1["he"]
"" 获取不存在的Key会导致错误
```

**删除和修改Key:Value**

``` vim
" 修改
"" 和设定值的形式一样

" 删除
unlet dict1.she
unlet dict1["he"]
let i = remove(dict1, 'you')
"" i为dict1.you的值
```

**Dictionary Functions**

``` vim
"类似于方法
let dict1 = {'me':'me name', 'he':'he name', 'she':'she name'}

function dict1.len()
    return len(self)
endfunction

" 或者
function s:mylen() dict
    return len(self)
endfunction

let dict2 = {'len':function('s:mylen'), 'name':'my name'}
```

**Functions for Dictinaryes**

``` vim
has_key(dict, 'key')      "dict 存在 'key'则返回 True
empty(dict)               "True if dict is empty
len(dict)                 "Number of items in dict
max(dict)                 "maximum value in dict
min(dict)                 "minimum value in dict
count(dict, 'x')          "count nr of times 'x' appears in dict
string(dict)              " to string
map (dict, '">> ".v:val') "map
```
这些函数同样可以用在**List**中

## 3. 表达式

## 4. 常用函数

使用`:help functions`可以查看所有内建函数

### 4.1 Buffer

**indent({lnum})** &rarr; **Int** &rArr; 指定行的C语言规则缩进

**cursor({lnum}, {col} [, {off}]), cursor({list})** &rArr; 移动光标到指定位置

**getpos({exprpos})** &rarr; **List** &rArr; `(bufnum, lnum, col, off]`返回位置信息

**indent({lnum})** &rarr; **Int** &rArr; 指定行的缩进

**line({exprpos})**根据表达式返回行数

`{exprpos}`:
    `.`     光标处
    `$`     末行
    `'x`    标记`x`处
    `w0`    可视的第一行
    `w$`    可视的最后一行
    `v`     visual mode 下选择的第一行

**line2byte({lnum})**返回指定行的累计byte


### 4.2 List, Dict, String函数

#### List

#### Dict

**keys({dict})** &rarr; **List**    &rArr;      返回`{dict}`的所有key

**values({dict})** &rarr; **List** &rArr;     返回`{dict}`的所有value

**items({dict})** &rarr; **List** &rArr;      返回List of List, 形如"[[key, value]]"

#### String

**char2nr({char})** &rarr; **Int** &rArr; 将字符根据编码转化为数值

**nr2char({Int})** &rarr; **Char** &rArr; 和**char2nr()**相反

**str2nr({str})** &rarr; **Nums** &rArr; 将字符串转化为数字

**str2float({Str})** &rarr; **Float** &rArr; 将字符串转化为浮点数

**tolower({String})** &rarr; **String** &rArr; 转化为小写

**toupper({String})** &rarr; **String** &rArr; 转化为大写

**strtrans({String})** &rarr; **String** &rArr; 转化字符串, 使其都是可见的字符

**tr({String}, {Str2}, {Str3})** &rarr; **String** &rArr; 将`String`各个字符在`Str2`中的使用`Str3`中的对应位置字符替代

**substitute({String}, {pat}, {sub}, {flags})** &rarr; **String** &rArr; 字符串替代

+ `flags`为 `""`或者`"g"`, `"g"`表示匹配到的全替换, `""`只替换一次
+ `{pat}, {sub}`使用`''`比较好

**strlen({String})** &rarr; **Int** &rArr; 字符串byte长度

**strchars({String})** &rarr; **Int** &rArr; 字符串字符个数

**strwidth({String})** &rarr; **Int** &rArr; 显示占位

**escape({string})** &rarr; **String** &rArr; 将需要转义的字符转义

**shellescape({String})** &rarr; **String** &rArr; 将shell cmd转义

**fnameescape({String})** &rarr; **String** &rArr; 将文件名转义

**eval({string})** &rarr; **其他类型数值** &rArr; 和**String()**相反

+ eval()只能转换**Numbers, Float, String, Component of them and funcref()**

**string({vars-expr})** &rarr; **String** &rArr;  将其他类型数值转化为变量

### 4.3 功能型函数

**getreg([{regName}[, 1[, list]]])** 获取寄存器内容

+ `1`选项指定则

**setreg([{regName}[, value[, <mode>]]])** 用于设置寄存器内容

**empty({expr})** &rarr; `List, Dict, Num(0)`

**type({expr})** &rarr; **Int** &rArr; 用于获取变量的类型

|类型|Value|内建变量|
|----|:---:|--------|
|Number |0|v:t_number|
|String |1|v:t_string|
|Funcref|2|v:t_func|
|List   |3|v:t_list|
|Dictionary|4|v:t_dict|
|Float|5|v:t_float|
|Boolean|6|v:bool|
|None|7|v:t_none|
|Job|8|v:t_job|
|Channel|9|v:t_channel|

### 4.4 管理函数

**hostname()** &rArr; **String** 返回当前计算机名

**libcall({libname}, {functionName}, {argumetns})**返回`functionName`返回的

+ 至多只能接受一个参数
+ 如果`functionName`返回的是Int, 则使用`libcallnr()`

**libcallnr({libName}, {functionName}, {argumetns})**和`libcall()`类似

### 4.5 其他

**deepcopy({expr}[, noref])** &aArr; 复制变量

**trunc({Num-float})** &rarr; **Int** &rArr; 取不大于`{Num-float}`的整数
