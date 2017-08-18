[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">VIML</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [0. 基本操作](#0)
    * [0.1 操作](#0.1)
    * [0.2 Ex命令](#0.2)

* [1. VIML基本语法](#1-VIML基本语法)
    * [1.1 条件语句](#11-条件语句)
    * [1.2 循环语句](#12-循环语句)
    * [1.3 函数](#13-函数)
    * [1.4 自动命令](#14-自动命令)

* [2. 变量](#2-变量)
    * [2.1 作用域](#21-作用域)
    * [2.2 种类](#22-种类)
    * [2.3 例子](#23-例子)

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

> List(列表)
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

> Dictionary(字典)
``` vim
```
