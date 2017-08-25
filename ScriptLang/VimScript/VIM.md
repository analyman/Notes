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
		* [Lambda](#lambda)
	* [1.4 自动命令](#14-自动命令)
* [2. 变量](#2-变量)
	* [2.1 作用域](#21-作用域)
	* [2.2 类型](#22-类型)
		* [2.2.1 List](#221-list)
		* [2.2.2 Dictionary](#222-dictionary)
* [3. 表达式](#3-表达式)
* [4. 常用函数](#4-常用函数)
	* [4.1 变量处理函数](#41-变量处理函数)
		* [4.1.1 String](#411-string)
		* [4.1.2 List](#412-list)
		* [4.1.3 Dict](#413-dict)
		* [4.1.4 Float](#414-float)
		* [4.1.5 Vars Type](#415-vars-type)
	* [4.2 Buffers, windows and the argument list](#42-buffers-windows-and-the-argument-list)
		* [4.2.1 Agurment List](#421-agurment-list)
		* [4.2.2 Buffer List](#422-buffer-list)
		* [4.2.3 Windows](#423-windows)
	* [4.3 Current Buffer](#43-current-buffer)
	* [4.4 Cursor and Mark](#44-cursor-and-mark)
	* [4.5 System](#45-system)
	* [4.6 语法和高亮](#46-语法和高亮)
	* [4.7 其他](#47-其他)
		* [4.7.1 时间](#471-时间)
		* [4.7.2 CMDLINE](#472-cmdline)
* [5. 异常处理](#5-异常处理)
	* [5.1 try-catch-finally-endtry](#51-trycatchfinallyendtry)
	* [5.2 异常](#52-异常)

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

**VIMSCRIPT变量**

* g:varname     全局变量
* s:varname     脚本变量
* v:varname     VIM定义变量
* w:varname     窗口变量
* t:varname     TAB变量
* b:varname     BUF变量
* l:varname     函数局部变量
* a:varname     函数参数

**OTHERS**

* &varname      varname为option
* &g:varname    全局的
* &l:varname    局部的
* @varname      寄存器(register)的值
* $varname      环境变量

### 2.2 类型

**VIML**的比较特殊的变量类型有`List(列表)`,`Directionary(字典)`

#### 2.2.1 List
``` vim
" List
let lst = ['a', 'b', 'c', 'd']

for ls in lst
    echo "the element is ".ls
endfor

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

[Function For List](#412-list)

#### 2.2.2 Dictionary

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

[Function For Directionary](#413-dict)

## 3. 表达式

## 4. 常用函数

使用`:help functions`可以查看所有内建函数

### 4.1 变量处理函数

**getreg([{regName}[, 1[, list]]])** 获取寄存器内容

+ `1`选项指定则

**setreg([{regName}[, value[, <mode>]]])** 用于设置寄存器内容

#### 4.1.1 String

**printf({fmt}, {expr} ...)**	&rarr;	**IO()**	&rArr;  格式化输出和C语言类似

+ 格式化字符格式`%[flags][field-width][.precision]{type}`
+ 详见`:help printf()`

**match()**	&rarr;	**Type**	&rArr;	position where a pattern matches in a string

**matchend()**	&rarr;	**Type**	&rArr;	position where a pattern match ends in a string

**matchstr()**	&rarr;	**Type**	&rArr;	match of a pattern in a string

**matchstrpos()**	&rarr;	**Type**	&rArr;	match and positions of a pattern in a string

**matchlist()**	&rarr;	**Type**	&rArr;	like matchstr() and also return submatches

**stridx()**	&rarr;	**Type**	&rArr;	first index of a short string in a long string

**strridx()**	&rarr;	**Type**	&rArr;	last index of a short string in a long string

**strdisplaywidth()**	&rarr;	**Type**	&rArr;	size of string when displayed, deals with tabs

**submatch()**	&rarr;	**Type**	&rArr;	get a specific match in ":s" and substitute()

**strpart()**	&rarr;	**Type**	&rArr;	get part of a string using byte index

**strcharpart()**	&rarr;	**Type**	&rArr;	get part of a string using char index

**strgetchar()**	&rarr;	**Type**	&rArr;	get character from a string using char index

**expand()**	&rarr;	**Type**	&rArr;	expand special keywords

**iconv()**	&rarr;	**Type**	&rArr;	convert text from one encoding to another

**byteidx()**	&rarr;	**Type**	&rArr;	byte index of a character in a string

**byteidxcomp()**	&rarr;	**Type**	&rArr;	like byteidx() but count composing characters

**repeat()**	&rarr;	**Type**	&rArr;	repeat a string multiple times

**execute()**	&rarr;	**Type**	&rArr;	execute an Ex command and get the output

**nr2char({Int})** &rarr; **Char** &rArr; 和**char2nr()**相反

**char2nr({char})** &rarr; **Int** &rArr; 将字符根据编码转化为数值

**str2nr({str})** &rarr; **Nums** &rArr; 将字符串转化为数字

**str2float({Str})** &rarr; **Float** &rArr; 将字符串转化为浮点数

**escape({string})** &rarr; **String** &rArr; 将需要转义的字符转义

**shellescape({String})** &rarr; **String** &rArr; 将shell cmd转义

**fnameescape({String})** &rarr; **String** &rArr; 将文件名转义

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

**eval({string})** &rarr; **其他类型数值** &rArr; 和**String()**相反

+ eval()只能转换**Numbers, Float, String, Component of them and funcref()**

**string({vars-expr})** &rarr; **String** &rArr;  将其他类型数值转化为变量

#### 4.1.2 List

**get({List}, {index} [, default])**	&rarr;	**Type**	&rArr;  get an item without error for wrong index

**len({List | Dict})**	&rarr;	**Int**	&rArr;  number of items in a List

**empty({List})**	&rarr;	**Boolean**	&rArr;  check if List is empty

**insert({list}, {value} [, idx])**	&rarr;	**List**	&rArr;  insert an item somewhere in a List

+ `[idx]`为 0, 插入首元素
+ `[idx]`为 `len{List}`或 -1 同`add()`
+ 改变参数List的值

**add({list}, {value})**	&rarr;	**Type**	&rArr;  append an item to a List

+ 改变参数List的值

**extend()**	&rarr;	**Type**	&rArr;  append a List to a List

**remove({List | Dict}, {start | key} [, end])**	&rarr;	**List | Dict**	&rArr;  remove one or more items from a List

+ 改变参数List的值

**copy({List})**	&rarr;	**List**	&rArr;  make a shallow copy of a List

**deepcopy({List})**	&rarr;	**List**	&rArr;  make a full copy of a List

**filter({List | Dict}, {Funcref})**	&rarr;	**List | Dict**	&rArr;  remove selected items from a List

**map({List | Dict}, {Funcref})**	&rarr;	**List | Dict**	&rArr;  change each List item

**sort()**	&rarr;	**Type**	&rArr;  sort a List

**reverse()**	&rarr;	**Type**	&rArr;	reverse the order of a List

**uniq()**	&rarr;	**Type**	&rArr;	remove copies of repeated adjacent items

**split()**	&rarr;	**Type**	&rArr;	split a String into a List

**join()**	&rarr;	**Type**	&rArr;	join List items into a String

**range()**	&rarr;	**Type**	&rArr;	return a List with a sequence of numbers

**string()**	&rarr;	**Type**	&rArr;	String representation of a List

**call()**	&rarr;	**Type**	&rArr;	call a function with List as arguments

**index()**	&rarr;	**Type**	&rArr;	index of a value in a List

**max()**	&rarr;	**Type**	&rArr;	maximum value in a List

**min()**	&rarr;	**Type**	&rArr;	minimum value in a List

**count()**	&rarr;	**Type**	&rArr;	count number of times a value appears in a List

**repeat()**	&rarr;	**Type**	&rArr;	repeat a List multiple times


#### 4.1.3 Dict

**keys({dict})** &rarr; **List**    &rArr;      返回`{dict}`的所有key

**values({dict})** &rarr; **List** &rArr;     返回`{dict}`的所有value

**items({dict})** &rarr; **List** &rArr;      返回List of List, 形如"[[key, value]]"

#### 4.1.4 Float

**float2nr()**	&rarr;	**Type**	&rArr;	convert Float to Number

**abs()**	&rarr;	**Type**	&rArr;	absolute value (also works for Number)

**round()**	&rarr;	**Type**	&rArr;	round off

**ceil()**	&rarr;	**Type**	&rArr;	round up

**floor()**	&rarr;	**Type**	&rArr;	round down

**trunc()**	&rarr;	**Type**	&rArr;	remove value after decimal point

**fmod()**	&rarr;	**Type**	&rArr;	remainder of division

**exp()**	&rarr;	**Type**	&rArr;	exponential

**log()**	&rarr;	**Type**	&rArr;	natural logarithm (logarithm to base e)

**log10()**	&rarr;	**Type**	&rArr;	logarithm to base 10

**pow()**	&rarr;	**Type**	&rArr;	value of x to the exponent y

**sqrt()**	&rarr;	**Type**	&rArr;	square root

**sin()**	&rarr;	**Type**	&rArr;	sine

**cos()**	&rarr;	**Type**	&rArr;	cosine

**tan()**	&rarr;	**Type**	&rArr;	tangent

**asin()**	&rarr;	**Type**	&rArr;	arc sine

**acos()**	&rarr;	**Type**	&rArr;	arc cosine

**atan()**	&rarr;	**Type**	&rArr;	arc tangent

**atan2()**	&rarr;	**Type**	&rArr;	arc tangent

**sinh()**	&rarr;	**Type**	&rArr;	hyperbolic sine

**cosh()**	&rarr;	**Type**	&rArr;	hyperbolic cosine

**tanh()**	&rarr;	**Type**	&rArr;	hyperbolic tangent

**isnan()**	&rarr;	**Type**	&rArr;	check for not a number


#### 4.1.5 Vars Type

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

**islocked()**	&rarr;	**Type**	&rArr;	check if a variable is locked

**funcref()**	&rarr;	**Type**	&rArr;	get a Funcref for a function reference

**function()**	&rarr;	**Type**	&rArr;	get a Funcref for a function name

**getbufvar()**	&rarr;	**Type**	&rArr;	get a variable value from a specific buffer

**setbufvar()**	&rarr;	**Type**	&rArr;	set a variable in a specific buffer

**getwinvar()**	&rarr;	**Type**	&rArr;	get a variable from specific window

**gettabvar()**	&rarr;	**Type**	&rArr;	get a variable from specific tab page

**gettabwinvar()**	&rarr;	**Type**	&rArr;	get a variable from specific window & tab page

**setwinvar()**	&rarr;	**Type**	&rArr;	set a variable in a specific window

**settabvar()**	&rarr;	**Type**	&rArr;	set a variable in a specific tab page

**settabwinvar()**	&rarr;	**Type**	&rArr;	set a variable in a specific window & tab page

**garbagecollect()**	&rarr;	**Type**	&rArr;	possibly free memory


### 4.2 Buffers, windows and the argument list

#### 4.2.1 Agurment List

**argc()**	&rarr;	**Type**	&rArr;	number of entries in the argument list

**argidx()**	&rarr;	**Type**	&rArr;	current position in the argument list

**arglistid()**	&rarr;	**Type**	&rArr;	get id of the argument list

**argv()**	&rarr;	**Type**	&rArr;	get one entry from the argument list


#### 4.2.2 Buffer List

**bufexists()**	&rarr;	**Type**	&rArr;	check if a buffer exists

**buflisted()**	&rarr;	**Type**	&rArr;	check if a buffer exists and is listed

**bufloaded()**	&rarr;	**Type**	&rArr;	check if a buffer exists and is loaded

**bufname()**	&rarr;	**Type**	&rArr;	get the name of a specific buffer

**bufnr()**	&rarr;	**Type**	&rArr;	get the buffer number of a specific buffer

**tabpagebuflist()**	&rarr;	**Type**	&rArr;	return List of buffers in a tab page

**tabpagenr()**	&rarr;	**Type**	&rArr;	get the number of a tab page

**tabpagewinnr()**	&rarr;	**Type**	&rArr;	like winnr() for a specified tab page

**bufwinid()**	&rarr;	**Type**	&rArr;	get the window ID of a specific buffer

**bufwinnr()**	&rarr;	**Type**	&rArr;	get the window number of a specific buffer

**winbufnr()**	&rarr;	**Type**	&rArr;	get the buffer number of a specific window

**getbufline()**	&rarr;	**Type**	&rArr;	get a list of lines from the specified buffer


#### 4.2.3 Windows

**win_findbuf()**	&rarr;	**Type**	&rArr;	find windows containing a buffer

**winnr()**	&rarr;	**Type**	&rArr;	get the window number for the current window

**win_getid()**	&rarr;	**Type**	&rArr;	get window ID of a window

**win_gotoid()**	&rarr;	**Type**	&rArr;	go to window with ID

**win_id2tabwin()**	&rarr;	**Type**	&rArr;	get tab and window nr from window ID

**win_id2win()**	&rarr;	**Type**	&rArr;	get window nr from window ID

**getbufinfo()**	&rarr;	**Type**	&rArr;	get a list with buffer information

**gettabinfo()**	&rarr;	**Type**	&rArr;	get a list with tab page information

**getwininfo()**	&rarr;	**Type**	&rArr;	get a list with window information

**winheight()**	&rarr;	**Type**	&rArr;	get height of a specific window

**winwidth()**	&rarr;	**Type**	&rArr;	get width of a specific window

**winrestcmd()**	&rarr;	**Type**	&rArr;	return command to restore window sizes

**winsaveview()**	&rarr;	**Type**	&rArr;	get view of current window

**winrestview()**	&rarr;	**Type**	&rArr;	restore saved view of current window


### 4.3 Current Buffer

**getline()**	&rarr;	**Type**	&rArr;	get a line or list of lines from the buffer

**setline()**	&rarr;	**Type**	&rArr;	replace a line in the buffer

**append()**	&rarr;	**Type**	&rArr;	append line or list of lines in the buffer

**indent()**	&rarr;	**Type**	&rArr;	indent of a specific line

**cindent()**	&rarr;	**Type**	&rArr;	indent according to C indenting

**lispindent()**	&rarr;	**Type**	&rArr;	indent according to Lisp indenting

**nextnonblank()**	&rarr;	**Type**	&rArr;	find next non-blank line

**prevnonblank()**	&rarr;	**Type**	&rArr;	find previous non-blank line

**search()**	&rarr;	**Type**	&rArr;	find a match for a pattern

**searchpos()**	&rarr;	**Type**	&rArr;	find a match for a pattern

**searchpair()**	&rarr;	**Type**	&rArr;	find the other end of a start/skip/end

**searchpairpos()**	&rarr;	**Type**	&rArr;	find the other end of a start/skip/end

**searchdecl()**	&rarr;	**Type**	&rArr;	search for the declaration of a name

**getcharsearch()**	&rarr;	**Type**	&rArr;	return character search information

**setcharsearch()**	&rarr;	**Type**	&rArr;	set character search information


**indent({lnum})** &rarr; **Int** &rArr; 指定行的C语言规则缩进

**cursor({lnum}, {col} [, {off}]), cursor({list})** &rArr; 移动光标到指定位置

**getpos({exprpos})** &rarr; **List** &rArr; `(bufnum, lnum, col, off]`返回位置信息

**indent({lnum})** &rarr; **Int** &rArr; 指定行的缩进

**line({exprpos})** &rarr; **Int** &rArr; 根据表达式返回行数

`{exprpos}`:

+    `.`     光标处
+    `$`     末行
+    `'x`    标记`x`处
+    `w0`    可视的第一行
+    `w$`    可视的最后一行
+    `v`     visual mode 下选择的第一行

**line2byte({lnum})**返回指定行的累计byte

### 4.4 Cursor and Mark

**col()**	&rarr;	**Type**	&rArr;	column number of the cursor or a mark

**virtcol()**	&rarr;	**Type**	&rArr;	screen column of the cursor or a mark

**line()**	&rarr;	**Type**	&rArr;	line number of the cursor or mark

**wincol()**	&rarr;	**Type**	&rArr;	window column number of the cursor

**winline()**	&rarr;	**Type**	&rArr;	window line number of the cursor

**cursor()**	&rarr;	**Type**	&rArr;	position the cursor at a line/column

**screencol()**	&rarr;	**Type**	&rArr;	get screen column of the cursor

**screenrow()**	&rarr;	**Type**	&rArr;	get screen row of the cursor

**getcurpos()**	&rarr;	**Type**	&rArr;	get position of the cursor

**getpos()**	&rarr;	**Type**	&rArr;	get position of cursor, mark, etc.

**setpos()**	&rarr;	**Type**	&rArr;	set position of cursor, mark, etc.

**byte2line()**	&rarr;	**Type**	&rArr;	get line number at a specific byte count

**line2byte()**	&rarr;	**Type**	&rArr;	byte count at a specific line

**diff_filler()**	&rarr;	**Type**	&rArr;	get the number of filler lines above a line

**screenattr()**	&rarr;	**Type**	&rArr;	get attribute at a screen line/row

**screenchar()**	&rarr;	**Type**	&rArr;	get character code at a screen line/row


### 4.5 System

**glob()**	&rarr;	**Type**	&rArr;	expand wildcards

**globpath()**	&rarr;	**Type**	&rArr;	expand wildcards in a number of directories

**glob2regpat()**	&rarr;	**Type**	&rArr;	convert a glob pattern into a search pattern

**findfile()**	&rarr;	**Type**	&rArr;	find a file in a list of directories

**finddir()**	&rarr;	**Type**	&rArr;	find a directory in a list of directories

**resolve()**	&rarr;	**Type**	&rArr;	find out where a shortcut points to

**fnamemodify()**	&rarr;	**Type**	&rArr;	modify a file name

**pathshorten()**	&rarr;	**Type**	&rArr;	shorten directory names in a path

**simplify()**	&rarr;	**Type**	&rArr;	simplify a path without changing its meaning

**executable()**	&rarr;	**Type**	&rArr;	check if an executable program exists

**exepath()**	&rarr;	**Type**	&rArr;	full path of an executable program

**filereadable()**	&rarr;	**Type**	&rArr;	check if a file can be read

**filewritable()**	&rarr;	**Type**	&rArr;	check if a file can be written to

**getfperm()**	&rarr;	**Type**	&rArr;	get the permissions of a file

**setfperm()**	&rarr;	**Type**	&rArr;	set the permissions of a file

**getftype()**	&rarr;	**Type**	&rArr;	get the kind of a file

**isdirectory()**	&rarr;	**Type**	&rArr;	check if a directory exists

**getfsize()**	&rarr;	**Type**	&rArr;	get the size of a file

**getcwd()**	&rarr;	**Type**	&rArr;	get the current working directory

**haslocaldir()**	&rarr;	**Type**	&rArr;	check if current window used |:lcd|

**tempname()**	&rarr;	**Type**	&rArr;	get the name of a temporary file

**mkdir()**	&rarr;	**Type**	&rArr;	create a new directory

**delete()**	&rarr;	**Type**	&rArr;	delete a file

**rename()**	&rarr;	**Type**	&rArr;	rename a file

**system()**	&rarr;	**Type**	&rArr;	get the result of a shell command as a string

**systemlist()**	&rarr;	**Type**	&rArr;	get the result of a shell command as a list

**hostname()** &rArr; **String** 返回当前计算机名

**readfile()**	&rarr;	**Type**	&rArr;	read a file into a List of lines

**writefile()**	&rarr;	**Type**	&rArr;	write a List of lines into a file

**libcall({libname}, {functionName}, {argumetns})**返回`functionName`返回的

+ 至多只能接受一个参数
+ 如果`functionName`返回的是Int, 则使用`libcallnr()`

**libcallnr({libName}, {functionName}, {argumetns})**和`libcall()`类似

### 4.6 语法和高亮

**clearmatches()**	&rarr;	**Type**	&rArr;	clear all matches defined by |matchadd()| and the |:match| commands

**getmatches()**	&rarr;	**Type**	&rArr;	get all matches defined by |matchadd()| and the |:match| commands

**hlexists()**	&rarr;	**Type**	&rArr;	check if a highlight group exists

**hlID()**	&rarr;	**Type**	&rArr;	get ID of a highlight group

**synID()**	&rarr;	**Type**	&rArr;	get syntax ID at a specific position

**synIDattr()**	&rarr;	**Type**	&rArr;	get a specific attribute of a syntax ID

**synIDtrans()**	&rarr;	**Type**	&rArr;	get translated syntax ID

**synstack()**	&rarr;	**Type**	&rArr;	get list of syntax IDs at a specific position

**synconcealed()**	&rarr;	**Type**	&rArr;	get info about concealing

**diff_hlID()**	&rarr;	**Type**	&rArr;	get highlight ID for diff mode at a position

**matchadd()**	&rarr;	**Type**	&rArr;	define a pattern to highlight (a "match")

**matchaddpos()**	&rarr;	**Type**	&rArr;	define a list of positions to highlight

**matcharg()**	&rarr;	**Type**	&rArr;	get info about |:match| arguments

**matchdelete()**	&rarr;	**Type**	&rArr;delete a match defined by |matchadd()| or a |:match| command

**setmatches()**	&rarr;	**Type**	&rArr;restore a list of matches saved by getmatches()

### 4.7 其他

#### 4.7.1 时间

**getftime()**	&rarr;	**Type**	&rArr;get last modification time of a file

**localtime()**	&rarr;	**Type**	&rArr;get current time in seconds

**strftime()**	&rarr;	**Type**	&rArr;	convert time to a string

**reltime()**	&rarr;	**Type**	&rArr;	get the current or elapsed time accurately

**reltimestr()**	&rarr;	**Type**	&rArr;	convert reltime() result to a string

**reltimefloat()**	&rarr;	**Type**	&rArr;	convert reltime() result to a Float

#### 4.7.2 CMDLINE

**getcmdline()**	&rarr;	**Type**	&rArr;	get the current command line

**getcmdpos()**	&rarr;	**Type**	&rArr;	get position of the cursor in the command line

**setcmdpos()**	&rarr;	**Type**	&rArr;	set position of the cursor in the command line

**getcmdtype()**	&rarr;	**Type**	&rArr;	return the current command-line type

**getcmdwintype()**	&rarr;	**Type**	&rArr;	return the current command-line window type

**getcompletion()**	&rarr;	**Type**	&rArr;	list of command-line completion matches

## 5. 异常处理

### 5.1 try-catch-finally-endtry

一个简单的例子:

``` vim
function! s:mmm()
    try
        if !(has('g:test_var'))
            throw "test_error"
        endif
        echo "ok"
    catch /^test_error$/
        echo "test error appear, how to deal with it?"
        echo "catch " . v:exception . " in ". v:throwpoint. "!"
    catch /^.*$/
        echo "Unknow Exception in function mmm()!"
        echo "catch " . v:exception . " in ". v:throwpoint. "!"
    finally
        echo "test finish"
    endtry
endfunction
```

+ 使用`throw`抛出异常
+ 内建变量`v:exception`表示最近抛出且未`finally`的异常
+ 内建变量`v:throwpoint`为抛出异常的位置

### 5.2 异常

VIM中的异常只是个字符串, 使用`v:exception`储存最后一次抛出的未被`finally`的异常, 使用`v:throwpoint`表示此次异常的抛出位置
