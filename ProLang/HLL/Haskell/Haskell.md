## Haskell

## Table of contents

## 关键字

|关键字|简述|
|:----:|----|
|module|定义一个模块|
|import|import一个模块|
|qulified|import模块避免避免命名冲突|
|as|和qulified一起使用|
|data|定义新的类型(类型构造子)|
|type|定义一个类型的别名|
|newtype|和data类似|
|Char|字符|
|String|字符串`type String = [Char]`|
|Int|`Int`类型|
|Integer|`Integer`类型|
|Word|`Word`类型|
|Float|`Float`类型|
|Double|`Double`类型|
|IO|`IO`类型构造子|

## 类型

+ 类型的名称以大写字母开头

### Bool

`Bool`**的定义:**

``` haskell
-- GHC.Types
data Bool = False | True
```

### Word, Int, Integer, Float, Double

#### 五种数值类型的定义

``` haskell
data Word = GHC.Types.W# GHC.Prim.Word#
data Int = GHC.Types.I# GHC.Prim.Int#
data Integer
  = integer-gmp-1.0.0.1:GHC.Integer.Type.S# !GHC.Prim.Int#
  | integer-gmp-1.0.0.1:GHC.Integer.Type.Jp# {-# UNPACK #-}integer-gmp-1.0.0.1:GHC.Integer.Type.BigNat
  | integer-gmp-1.0.0.1:GHC.Integer.Type.Jn# {-# UNPACK #-}integer-gmp-1.0.0.1:GHC.Integer.Type.BigNat
data Float = GHC.Types.F# GHC.Prim.Float#
data Double = GHC.Types.D# GHC.Prim.Double#
```

#### Num

``` haskell
class Num a where
    (+) :: a -> a -> a
    (-) :: a -> a -> a
    (*) :: a -> a -> a
    negate :: a -> a
    abs :: a -> a
    signum :: a -> a
    fromInteger :: Integer -> a
```

`Word, Int, Integer, Float, Double`都是`Num`的`instance`

### List

`[]`**的定义:**

``` haskell
-- GHC.Types
data [] a = [] | a : [a]
```

### Tuple

``` haskell
-- GHC.Tuple
data () = ()
```

### 定义新的数据类型

#### 使用关键字`date`定义新的数据类型

`Bool`类在标准库中的定义:  

``` haskell
data Bool = False | True
```

`=`左端定义了类型的名称, 右端则是给出了可能的值(`False`, `True`称为构造子(type constructor))

再来看一个例子:  

``` haskell
data Person = Man Float Float Int | Woman Float Float Int

agePerson  :: Person -> Int
agePerson (Man _ _ age) = age
agePerson (Woman _ _ age) = age
```

`Person`有`Man`和`Woman`两种, `Man`和`Woman`都有两个`Float`值分别代表`Height`, `Weight`. `Int`表示`Age`  
`Person`有两个构造子`Man`, `Woman`

**注意:**

+ **构造子可以和类型同名**
+ **构造子(type constructor)的值类型可以包括函数类型**

#### Record syntex

`Person`例子:  

``` haskell
data Person = 
    Man { 
    height :: Float
    , weight :: Float
    , age    :: Int
    }
    | Woman { 
    height :: Float
    , weight :: Float
    , age    :: Int
    }
```

将自动生成一下函数:  

+ `height    :: Person -> Float`
+ `weight    :: Person -> Float`
+ `age       :: Person -> Int`

对值的赋值可以采用以下形式:  

+ `me = Man 180 70 20`
+ `me = Man { height = 180, weight = 70, age = 20 }`

### Type parameters

**Maybe**, **Just**:  

``` haskell
data Maybe a = Nothing | Just a
```

`Maybe`接受一个类型作为参数, 结果是一个类型  
`Maybe`称为类型构造子(**Data constructor**)

### 类型类

### Type关键字

### TypeClass

## 函数

+ 函数也是有类型的
+ 函数的名称以小写字母开头
+ 函数的类型声明:`funcName :: Type1 -> Type2 -> Type3`

### 函数的定义

### CASE

## 使用GHCI

**Available Commands:**

|Commands|Description|
|:------:|-----------|
|`:`|重复上一个命令|
|`:{\n .. lines .. \n:}\n`|多行命令|
|`:add [*]<module> ...`|添加模块|
|`:browse[!] [[*]<mod>]`|查看模块信息, `!`详细显示|
|`:cd <dir>`|改变当前目录|
|`:ctags[!] [<file>]`|新建`ctags`文件, for vi[m]|
|`:def <cmd> <expr>`|新建`cmd`, `:<cmd>`|
|`:edit <file>`|编辑文件|
|`:edit`|编辑最后一个模块|
|`:etags [<file>]`|tags file for emacs|
|`:help, :?`|打印帮助信息|
|`:info[!] [<name> ...]`|显示关于`<name>`的有关信息|
|`:issafe [<mod>]`|显示关于该模块的安全信息|
|`:kind[!] <type>`|关于类型`<type>`的信息|
|`:load[!] [*]<module> ...`|load module|
|`:main [<arguments> ...]`|运行`main`函数|
|`:module [+/-] [*]<mod> ...`|expression evaluation|
|`:quit`|退出GHCI|
|`:reload[!]`|重新加载当前模块集|
|`:run function [<arguments> ...]`|运行`function`|
|`:script <file>`|运行脚本|
|`:undef <cmd>`|删除用户定义命令`<cmd>`|
|`:!<sh-cmd>`|运行`shell cmd`|

## 模块

## IO

## 一些基础的模块

### Data

#### Data.List

#### Data.Map

#### Data.Set

#### Data.Char
