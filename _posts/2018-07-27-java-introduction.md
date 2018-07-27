---
layout: post
title: "Java简介与快速入门（一）"
date: 2018-07-26 22:00:00
tags: Java code
description: 介绍Java特点与三类语句
---

- [Java简介](#simpleIntroduction)
    - [何为”纯面向对象“？](#pureOOP)
    - [GC](#gc)
- [数组](#arr)
- [字符串](#string)
- [几种常用的语句结构](#severalStruct)
    - [判断结构](#judge)
    - [循环结构](#recurrent)
- [面向对象语言中的潜规则](#subrule)
- [命令行下的Java（选读）](#commandline)

# <span id="simpleIntroduction">Java简介</span> 
Java是一种纯面向对象（注意这个”纯“）编程语言。相较于C++有不少优点，比如没有繁琐的指针，拥有GC（Garbage Collector）模块用于管理内存（从而舍去了C++中的析构函数，以下会讲到）

## <span id="pureOOP">何为”纯面向对象“？</span>
- Java所有的代码都必须包括在类之中，甚至连main函数都不放过
- Java的原则中有一条是：一切皆对象。即所有的能使用的都是以类的形式出现，并且几个最基本的变量类型也是如此，例如Integer，Double, Boolean（注意是首字母大写），而首字母小写的都是类似于C++中的int, double ,float等基本变量类型）
> 等会，你不是说一切皆对象么？那int，double, boolean这些变量怎么办？
- 其实在函数传参的过程中Java底层对其进行了“拆箱装箱”的操作, (C#，以及之后的很多语言都使用了这个方法来解决这个问题），即在函数传参的过程中将其包装为Integer对象，然后在函数体内部进行拆箱操作，将其转化为int类型进行使用。

## <span id="gc">GC模块</span>
- GC模块的核心是垃圾（Garbage）收集（collection）算法
- C++被人诟病的原因之一是因为需要人为地管理内存（申请与释放）这会导致内存的泄露
> 这一部分比较难理解，需要对内存和指针有一定的认识，于是就有了下面的一种解释
- C++就像一个很皮的孩子，每次玩完玩具都不会自己把东西放回原处（释放内存），作为家长（程序设计者）需要帮他把东西归位（手动释放内存）。而Java面对这样的情况，就请了一个保姆（GC模块）来收拾东西，而我们就可以将精力放在如何设计程序上了。

# <span id="arr">数组</span>
- 由于一切皆对象的思想，数组也被Java包装成了对象，但是与Integer类型不同的是，数组对象中除了数组本身还有一些别的变量来辅助我们更方便的设计程序

>下面是一个C++函数实现了数组的输出
{:.filename}
{% highlight C++ %}
// 省略一些代码
void printArr(int[] arr, int num)
{
    for(int i = 0;i < num;++i){
        cout << arr[i];
    }
}
{% endhighlight C++ %}
{:.end}

> 可以看出如果没有`num`变量，我们就不知道数组的长度，进而无法进行数组遍历。

>下面是一个Java函数实现数组的输出
{:.filename}
{% highlight Java %}
// 省略一些代码
void printArr(int[] arr)
{
    for(int i = 0;i < arr.length;++i){
        System.out.println(arr[i]);
    }
}
{% endhighlight %}
{:.end}

> 显然arr对象中的`length`属性被访问用于代替上述C++代码中的num，突然就少了一个参数呢

# <span id="string">字符串</span>
- C++中的字符串多用char数组来进行字符的处理，每次拼接字符串还需要使用大量的指针（看得我头都大了）。Java的标准库中提供了String类来进行字符串的处理。
- 拼接
{% highlight Java %}
public static void main(String[] args)
{
    String s1 = "hello";
    String s2 = "world";
    System.out.println(s1 + s2); //helloworld
}
{% endhighlight %}
> 是的，就是这么简单只需要用”+“号连接即可

{: .note}
- 当需要拼接大量字符串时<span style="color: red">千万不要使用</span>上述方法进行操作，会极大的消耗内存，正确的姿势是使用[StringBuilder](https://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html)
{: end}

# <span id="severalStruct">几种常用的语句结构</span>
## <span id="judge">判断结构</span>

{% highlight Java %}
public static void main(String[] args)
{
    if(1 == 1)
    {
        Sytem.out.println("always printed");
    }
    else
    {
        System.out.println("never printed");
    }
}
{% endhighlight %}

## <span id="recurrent">循环结构</span>
- for循环前面已经有用过，这里不再敖述。
- for循环高级使用
{% highlight Java %}
void printArr(String[] arr)
{
    for(String s : arr) // 此处s就是每一个arr中的元素
    { 
        System.out.println(s);
    }
}

// 以上代码等价于    

void printArrWithIndex(String[] arr)
{
    for(int i = 0;i < arr.length;++i)
    {
        String s = arr[i];
        System.out.println(s);
    }
}
{% endhighlight %}

- while循环

{% highlight Java %}
public static void main(String[] args)
{
    while(1)
    {
        System.out.println("dead loop!");
    }
}
{% endhighlight %}

# <span id="subrule">面向对象语言中的潜规则</span>
- 写到这里发现所有的大括号都没有直接换行，对于必须换行的强迫症这真的是一种灾难，于是我用了五分钟时间将所有的大括号都换到了下一行，但是在大多数的Java的IDE中，比如Eclipse，都会是以大括号不换行的形式呈现代码。要解决这样的问题可以在IDE的设置中定义生成模板代码的格式等。

# <span id="commandline">命令行下的Java（选读）</span>
- 如果细心观察，会发现在IDE运行代码的时候，在输出窗口会有类似与这样的一句话

{% highlight bash %}
$ /path/to/java /path/to/certain/classname
{% endhighlight %}

- 其实不止Java，C++也有类似的操作——编译（compile）
> Max plus II 软件中就有这个`compile`选项。
- 我们发现`.java`文件的本质是一个文本文件，也就是说我们可以用记事本之类的工具打开并进行编辑，那我们需要使其变成能被计算机所理解的指令才可以运行我们的程序。

{% highlight bash %}
$ javac classname.java # 编译程序
{% endhighlight %}

> 此时在该文件夹下会生成一个文件`classname.class`

{% highlight bash %}
$ java classname # 运行程序
{% endhighlight %}

> 注意`classname`后面没有任何后缀

- 其实在这时删除classname.java，程序依然可以运行，所以`.java`文件本身不参与程序的运行，而如果删除了`classname.class`则不能运行程序。 



