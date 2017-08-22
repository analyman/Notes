## Haskell

## Table of contents

## 关键字

## 类型

+ 类型的名称以大写字母开头

### Bool

### Int, Integer, Float, Double

### List

### Tuple

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

+ 函数的名称以小写字母开头

### 函数的定义

### CASE

## 模块

## IO

## 一些基础的模块

### Data

#### Data.List

#### Data.Map

#### Data.Set

#### Data.Char
