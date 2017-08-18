[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">Autolisp</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [1. Autolisp Basic](#1)
    * [1.1 数据类型](#1.1)
    * [1.2 变量](#1.2)
    * [1.3 Expression](#1.3)
    * [1.4 基本的函数](#1.4)
    * [1.5 定义函数和命令](#1.5)

<h2 name="1"><span style="color:rgb(0,110,110)">1. Autolisp Basic</span></h2>

<h3 name="1.1"><span style="color:rgb(110,110,0)">1.1 数据类型</span></h3>

``` lisp
; 数据类型有编译器（解释器）进行判断

; Integer
; Autolisp 的只有有符号整数, 为32bit整数
; 当超过表示范围时, 就是浮点数了, 这也会导致精度

; Real
; 双精度浮点数,可以由科学记数法表示
; 如:   1.2e+10

; String
; "this is a string"表示一个字符串
; 一些函数支持转义符号的输出, "this is a string\n"

; List
; Autolisp可以使用List来表示点
; (1 22), (22 11 44)
; 同时List中的数据类型可以不同
; (22 2.2e+11), (11 "this is a list element")

; File Descriptors
; 由(open filenamestring ...)打开一个文件, 并返回一个File Descriptors
; (close filedescriptors)关闭一个打开的文件
```

<h3 name="1.2"><span style="color:rgb(110,110,0)">1.2 变量</span></h3>

``` lisp
; autolisp中由setq函数完成变量的赋值, 同时不需要先定义变量
(setq var1 "string variable")
(setq var2 var1)

; 可以在一个setq函数中完成多个变量的赋值
(setq var1 value1 var2 value2 ...)
(setq
    var1 value1
    var2 value2
)

; 可以在命令行中使用'!var1'显示出var1的值

; 释放内存, 将变量设为nil
(setq
    var nil
)
```

<h3 name="1.3"><span style="color:rgb(110,110,0)">1.3 Expression</span></h3>

``` lisp
; 加减乘除
(+ 1 1)         ; 2
(- 1 1)         ; 0
(* 1 2)         ; 2
(/ 2 1)         ; 2

; 调用函数基本格式
(function
    argumentlist
)

; 注释
; 以';'开头到结尾到结束认为是注释, 如:
(setq
    var1 11 ; this is comment
    var2 22 ; this is comment 2
)
; 以';| "comment" |;‘可以表示行间的注释
(setq var1 11 ;| this is coment inline |; var2 22)
```

<h3 name="1.4"><span style="color:rgb(110,110,0)">1.4 基本的函数</span></h3>

> 整数,实数(双精度浮点数)
``` lisp
; 实数(有实数参与)加减乘除函数都返回返回实数
; 整数加减乘除函数不出现超过表示范围都返回整数, 否则就返回实数
```

> 字符串
``` lisp
;strcase字符串转换字母的大小写
(setq
    string1 (strcase
        "this is Test"
    )
)
(setq
    string2 (strcase
        "This is Test"
    )
)
; string1 = "THIS IS TEST"
: string2 = "this is test"

; strcat连接字符串
(setq
    string3 (strcat
        "string1" "string2" "string3"
    )
)
; string3 = "string1string2string3"

; strlen返回字符串的长度
(setq
    string_len (strlen
        "this is a string"
    )
)
; string_len = 16

; strsub用于截取部分字符串, 第一参数字符串, 第二个参数起始位置
; 第三个位置可选, 结尾位置, 默认为结尾

(setq
    str "hello wolrd!"
)
(setq
    str2 (substr
        str 3
    )
)
(setq
    str3 (substr
        str 3 2
    )
)
; str2 = "llo world!", ;str3 = "ll"

; 简单的模式匹配wcmatch
(wcmatch
    "this is example" "this*"
)                   ; 返回T
(wcmatch
    "this is example" "is*"
)                   ; 返回nil
(wcmatch
    "this is example" "this[ ]*"
)                   ; 返回T
;wcmatch支持'[]', '*'表示任意多个的任意字符
```

> 基本的输出函数
``` lisp
; prin1, princ, print, prompt

;print, princ, print. 参数多样
(prin1 
    "hello world"
)                   ;直接打印字符串, 不支持转义字符输出
(princ
    "hello world"
)                   ;支持转义字符输出, 输出首尾不自带'"'
(print
    "hello world"
)                   ;先打印一行, 再输出

; prompt支持转义字符输出, 参数只能为字符串
(prompt
    "hello\tworld!\n"
)
(princ)             ;输出没有多余的
```

> 列表（List)
``` lisp
; 用list函数初始化List, 不可以直接将(1 2 3)赋值给list
(setq
    list1 (list
        1 2 3
    )
)
(setq               ;还可以用这种方式初始化list
    list2 '(7 8 9)
)
; list1 = (1 2 3)

; 用nth函数索引list, 从0开始
(setq
    list2 (list
        3 2 1
    )
)
(setq
    element (nth
        0 list2
    )
)

; cdr函数返回减去第一个元素的列表
; car函数返回列表的第一个元素
; (cadr list1)等于(car (cdr list1)), (cddr list1)等于(cdr (cdr list1))
; (caar list1)等于(car (car list1)), 只有list1的首个执行的car返回是list类型才不会报错

; append追加一个元素到列表末尾并返回
; cons在列表首部添加元素并返回
; subst用指定的元素替换列表中的指定元素
(append
    '(22 33) 44
)               ; 返回(22 33 44)
(cons
    11 '(22 33)
)               ; 返回(11 22 33)
(subst
    11 22 '(22 33 33 22)
)               ; 返回(11 33 33 11), 如果未匹配到元素, 则不改变
```

<h3 name="1.5"><span style="color:rgb(110,110,0)">1.5 定义函数和命令</span></h3>

> 基本格式
``` lisp
; 函数
(defun
    function_name (args / local_variables) expressions
)

; 例子:
(defun
    mmp () (prompt
        "mai ma pi\n"
    )
    (princ)
)
(mmp)           ; 输出"mai ma pi"

; 命令, 和函数几乎相同, 只要在function_name前面加'C:'即可
(defun
    C:mmp () (prompt
        "mai ma pi\n"
    )
    (princ)
)               ; 这样就可以在autocad中调用mmp命令, 允许重写内置的命令
```

> command函数
``` lisp
; 用于在autolisp中调用autocad的命令
(command
    command_name command_arguments
)               ;command_name是字符串形式的, 最后用'" "'执行命令

; command中, 如果CMDECHO为0, 则不产生输出
; command-s总是产生输出
```
