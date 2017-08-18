[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">C#</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [0. 介绍](#0-介绍)
    * [0.1 保留字](#01-保留字)
    * [0.2 历史](#02-历史)

* [1. 类](#1)
    * [1.1 类的简介](#11-类的简介)
    * [1.2 构造和析构](#12-构造和析构)
    * [1.3 属性和索引](#13-属性和索引)
    * [1.4 事件](#14-事件)
 
* [2. 数组](#2-数组)
    * [2.1 数组类型](#21-数组类型)
    * [2.2 数组创建](#22-数组的创建)

## 0. 介绍

### 0.1 关键字

> 保留字

|关键字|关键字|关键字|关键字|
|------|------|------|------|
|abstract|as|base|bool|
|break|byte|casecatch|
|char|checked|class|const|
|continuedecimal|default|delegate|
|do|double|else|enum|
|event|explicit|extern|false|
|finally|fixed|float|for|
|foreach|goto|if|implicit|
|in|in(泛型修饰符)|int|interface|
|internal|is|lock|long|
|namespace|new|null|object|
|operator|out|out(泛型修饰符)|override|
|params|private|protected|public|
|readonly|ref|return|sbyte|
|sealed|short|sizeof|stackalloc|
|static|string|struct|switch|
|this|throw|true|try|
|typeof|uint|ulong|unchecked|
|unsafe|ushort|using|using static|
|void|volatile|while||


> 上下文关键字

|关键字|关键字|关键字|关键字|
|----|----|----|----|
|add|alias|ascending|async|
|await|descending|dynamic||from|
|get|global|group|into|
|join|let|orderby|partial(类型)|
|partial(方法)|remove|select|set|
|value|var|when(筛选条件)|where(泛型类型约束|
|yield||||

> 上下文关键字用于在代码中提供特定的含义，但不是C#的保留字

> 类型符用于声明  
>> 值类型  

|类型符|范围|Description|
|------|----|-----------|
|sbyte|-128 到 127|有符号 8 位整数|
|byte|0 到 255|无符号 8 位整数|
|char|U+0000 到 U+ffff|16 位 Unicode 字符|
|short|-32,768 到 32,767|有符号 16 位整数|
|ushort|0 到 65,535|无符号 16 位整数|
|int|-2,147,483,648 到 2,147,483,647|有符号 32 位整数|
|uint|0 到 4,294,967,295|无符号 32 位整数|
|long|-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807|有符号 64 位整数|
|ulong|0 到 18,446,744,073,709,551,615|无符号 64 位整数|
|float|±1.5e45 到 ±3.4e38|7 位精度|
|double|±5.0e324 到 ±1.7e308|15 到 16 位精度|
|decimal|(-7.9 x 10e28 - 7.9 x 10e28)/(10e(0 - 28))|128bit,高精度|
|bool|true,false,null|boolean类型|
|enum|Ommit|枚举类型|

>> class,interface,delegate,dynamic,object,string  

|关键字|Description|
|------|-----------|
|class|声明类,Csharp中的类允许单继承|
|interface|声明接口,只包含方法，属性，事件，索引器的签名|
|delegate|声明一个委托,委托类似于函数指针|
|dynamic|编译时不检查dynamic类型|
|object|统一类型系统所有类型都直接或间接继承object类|
|string|声明字符串|

>> 指针类型

|运算符,语句|Description|
|-----------|-----------|
|&#42;|执行指针间接寻址|
|&#45;&#62;|通过指针访问结构的成员|
|[]|为指针建立索引|
|&#38;|获取变量的地址|
|++,--|递加和递减指针|
|+,-|执行指针算法|
|比较符号|比较指针大小|
|stackalloc|分配heap上的内存|
|fixed|临时固定变量|

>> 访问修饰符  

|关键字|Description|
|------|-----------|
|public|访问不受限制|
|protected|访问仅限于包含类或包含类派生的类型|
|Internal|访问仅限于当前程序集|
|protected internal|两者相加|
|private|访问仅限于包含类型|

>> 其他的关键字  

|关键字|Description|
|------|-----------|
|abstract|不可实例化,要由派生类来实现|
|async|将方法,lambda表达式,匿名方法指定为异步|
|const|声明为常量|
|event|事件|
|extern|声明在外部实现的方法|
|in(泛型修饰符)|对于泛型类型参数,in关键字可指定类型参数是逆变的|
|out(泛型修饰符)|对与泛型类型参数,out关键字可指定类型参数是协变得|
|override|拓展或修改继承的方法,属性,索引器或事件的抽象或虚拟实现需要override修饰符|
|readonly|该声明引入的赋值只能作为声明的一部分出现,或者出现在同一类的构造函数中|
|sealed|阻止类被继承|
|static|声明静态成员|
|unsafe|不安全上下文,使用指针必须|
|virtual|用于修改方法,属性,索引器或事件声明|
|volatile|通常用于由多个线程访问,但不使用lock语句对访问进行序列化的字段|

### 0.1 历史

**C#**是为**.NET**提供的编程语言.**C#**版本,**.NET**版本,**VS**版本  

|C#|.NET|Visual stdio|Description|
|:-:|:-:|:----------:|-----------|
|C# 1.0|.net framework 1.0/1.1|visual studio 2002/2003|c#的第一个版本|
|C# 2.0|.net framework 2.0|visual studio 2005|支持泛型|
|unchanged|.net framework 3.0|unchanged|新增api支持分布式通信|
|C# 3.0|.net framework 3.5|visual studio 2008|添加了LINQ的支持,对集合操作api大幅度修改|
|C# 4.0|.net framework 4.0|visual studio 2010|添加了动态类型的支持,对多线程编程api进行了大幅度的改进|
|C# 5.0|.net framework 5.0|visual studio 2012|添加了异步方法的调用|
|C# 6.0|unchanged|visual studio 2015|简化，阐明并压缩代码|

## 1. 类

### 1.1 类的简介

C#使用类规范来构造对象,对象是类的实例.因此,类在本质上是指定如何创建对象的一组计划.类是一种逻辑抽象.创建类的对象,内存才会有该类的物理表示.  

>一些关键字  

`base`关键字用于从派生类中访问基类成员:  

* 调用基类上已被其他方法重写的方法  
* 指定创建派生类实例时应调用的基类构造函数  
* 静态方法不可用`base`关键字  
* 基类访问仅允许在构造函数,实例方法,实例属性访问器中进行  

`this`关键字指代类的当前实例:  

* 在方法,构造函数中调用与传入参数同名的成员  
* 将对象作为参数传递给方法  
* 声明索引器  
* 静态成员函数,存在于类级别不属于对象不具有`this`指针,在静态方法中使用`this`是错误的

`ref`关键字指定通过引用传递参数,而非值  

* 定义和调用方法时都需要指定`ref`关键字  
* `ref`的实参需要经过初始化  
* 属性不能传递到`ref`参数  
* 不能用于异步方法,迭代器方法  
*`ref`可以用于重载,但是不可以与`out`重载  

`out`关键字与`ref`相似,区别在于`out`指定的参数可以不经过初始化  

> 一个简单的例子

``` csharp
/*
 * filename:TestClass.cs
 */
class TestClass         //首字母大写
{
    private int fir_ele;

    /*
     * c#自己有默认的构造方法,将所有数据置零.当有用户定义的构造方法时
     * 将不会再使用默认的构造方法
     */
    public TestClass(int fir){      //构造方法1
        fir_ele = fir;  //初始化fir_ele变量
    }
    public TestClass(){             //重载的构造方法2
        fir_ele = 0;
    }

    // info 方法
    public void info(){
        System.Console.WriteLine("the first element is " + fir_ele);
    }
}

/*
 * 另一个cs文件中
 * filename:main.cs
 */
class App_ent
{
    static void Main(string[] args){
        TestClass test1 = new TestClass(81);
        test1.info();       //输出"the first element  is 81"
        TestClass test2;
        test2 = new TestClass();
        test2.info();       //输出"the first element is 0"
        
        // Keep the console window open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();

    }
}
```

### 1.2 构造与析构

> 构造方法:在创建实例时调用构造方法初始化对象  
> 析构函数:在销毁对象之前调用此函数

``` csharp
class TestClass
{
    // 构造方法
    public TestClass(){
        System.Console.WriteLine("new object is creacting.");
    }

    // 析构函数,不能继承和重载
    public ~TestClass(){
        System.Console.WriteLine("this object is ruining");
    }
}
```

> private的构造方法,可以用与防止类被实例化(当类用户定义的构造函数,并且都是Private修饰的

``` csharp
/*
 * filename:TestClass.cs
 */
class TestClass
{
   private TestClass()
   {}

   public static hello(){
   System.Console.WriteLine("hello man!");
    }
}

/*
 * filename:MainApp.cs
 */
 class MainApp
 {
    static void Main(){
        // TestClass obj1 = new TestClass(); error!
        TestClass.hello();

        // Keep the console window open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}

// output:"hello man!"
```

> 静态类的构造方法  

``` csharp
/*
 * filename:TestClass.cs
 */
static class TestClass
{
    TestClass()                     //需要声明为static,并且不能有访问限定符
    {
        System.Console.WriteLine("引用静态类TestClass");
    }

    // say hello method
    public static void hello(){     //需要声明为static
        System.Console.WriteLine("hello man!");
    }
}

/*
 * filename:MainApp.cs
 */
 class MainApp
 {
    static void Main(string[] args)
    {
        TestClass.hello();          //引用构造类的hello()方法
        TestClass.hello();
        
        // Keep the console window open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}

// 最终输出:"引用静态类","hello man!","hello man!".
// 所以静态类的构造函数只在第一次引用时调用
```

### 1.3 属性与索引器

属性结合了字段和方法的多个方面。 对于对象的用户，属性显示为字段，访问该属性需要相同的语法。 对于类的实现者，属性是一个或两个代码块，表示一个`get`访问器和`V`或一个`set`访问器。 当读取属性时，执行`get`访问器的代码块；当向属性分配一个新值时，执行`set`访问器的代码块。 不具有`set`访问器的属性被视为只读属性。 不具有`get`访问器的属性被视为只写属性。同时具有这两个访问器的属性是读写属性。  
与字段不同，属性不作为变量来分类。 因此，不能将属性作为`ref`参数或`out`参数传递。  

``` csharp
/*
 * filename:TestClass.cs
 */
class TestClass
{
    public TestClass(){}

    //属性prop1
    private int Prop1 = 0;          //定义属性的字段
    public int prop1 {              //属性的访问器
        set
        {
            if(value >= 0){
                Prop1 = value;
            }
        }
        get
        {
            return Prop1;
        }
    }
    //自动属性prop2
    public int prop2 {get;set;} = 0;        //初始值为0,C#6.0及以上
}

/*
 * filename:MainApp.cs
 */
class MainApp
{
    static void Main(string[] args){
        TestClass test1 = new TestClass();

        int initia_value = test1.prop1;
        test1.prop1 = 4;
        test1.prop2 = 8;
        System.Console.WriteLine("prop1 initialization value is "
        + initia_value + "\nnow prop1 is " + test1.prop1
        + "\nnow prop2 is " + test1.prop2);

        // Keep the console window open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}
 
/*
 * prop1 initialization value is 0
 * now prop1 is 4
 * now prop2 is 8
 * Press any key to exit.
 */
```

索引器和属性的区别  
* 属性由它的名称标识，而索引器由它的签名标识。  
* 属性可以是 static 成员，而索引器始终是实例成员。  
* 属性的 get 访问器对应于不带形参的方法，而索引器的 get 访问器对应于与索引器具有相同的形参表的方法。  
* 属性的 set 访问器对应于具有名为 value 的单个形参的方法，而索引器的 set 访问器对应于与索引器具有相同的形参表加上一个名为 value 的附加形参的方法。  
* 若在索引器访问器内使用与该索引器的形参相同的名称来声明局部变量，就会导致一个编译时错误。  
* 在重写属性声明中，被继承的属性是使用语法 base.P 访问的，其中 P 为属性名称。在重写索引器声明中，被继承的索引器是使用语法 base[E] 访问的，其中 E 是一个用逗号分隔的表达式列表。

``` csharp
/*
 * filename:BitArray.cs
 */
using System;
class BitArray
{
    private int[] bits;
    private int length;

    //构造方法
    public BitArray(int length){
        if(length < 0){
            throw new ArgumentException();
        }
        this.length = length;
        /* (length - 1)/32 + 1 > length/32
         * 分配的内存足够用；
         */
        bits[] = new int[((length - 1) >> 5) + 1];
    }

    //属性Length
    public int Length {
        get{
            return length;
        }
    }

    //索引器
    public bool this[int index] {
        get {
            if(index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            //注意返回值类型
            return (bits[index >> 5] & 1 << (index%32)) != 0;
        }
        set {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            if(value) {
                bits[index >> 5] |= (1 << (index%32));
            } else {
                bits[index >> 5] &= ~(1 << (index%32));
            }
        }
    }
}

/*
 * filename:MainApp.cs
 */
class MainApp
{
    static void Main(string[] args){
        BitArray integer32 = new BitArray(32);
        integer32[11] = true;
        
        int i;
        for(i=0;i<32;i++) {
            System.Console.WriteLine("the " + i + "bit is " + integer32[i]);
        }

        // Keep the console window open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}

// output:太长了,只有11显示true;结果符合预期
```

### 1.4 事件


## 2. 数组

### 2.1 数组类型


