> 本文内容由[模板 \(C++\)](https://zh.wikipedia.org/wiki/模板_\(C++\))转换而来。


**模板**（****）指[C++](../Page/C++.md "wikilink")[程序设计语言中的](https://zh.wikipedia.org/wiki/程序设计语言 "wikilink")[函数模板与](../Page/子程序.md "wikilink")[类模板](../Page/类_\(计算机科学\).md "wikilink")\[1\]，是一种[参数化类型机制](https://zh.wikipedia.org/wiki/参数化类型 "wikilink")，大体对应于[java和](https://zh.wikipedia.org/wiki/java "wikilink")[C＃中的](https://zh.wikipedia.org/wiki/C＃ "wikilink")[泛型](../Page/泛型.md "wikilink")，但也有一些功能上的显著差异（C++模板支持后两者没有明确对应的模板模板参数和模板非类型参数，但不支持Java的通配符以及C\#的泛型类型约束）。模板是C++的[泛型编程中不可缺少的一部分](https://zh.wikipedia.org/wiki/泛型编程 "wikilink")。

模板是C++程序员绝佳的武器，特別是結合了[多重继承](../Page/多重继承.md "wikilink")与[运算符重载](../Page/运算符重载.md "wikilink")之后。C++的标准函数库提供的许多有用的函数大多結合了模板的概念，如[STL以及](https://zh.wikipedia.org/wiki/STL "wikilink")[iostream](https://zh.wikipedia.org/wiki/iostream "wikilink")。

## 语法

### 模板的声明与定义

模板定义以关键字`template`开始，后接模板形参表（template parameter list），模板形参表是用尖括号括住的一个或者多个模板形参的列表，形参之间以逗号分隔。模板形参可以是表示类型的类型形参（type parameter），也可以是表示常量表达式的非类型形参（non-type parameter）。非类型形参跟在类型说明符之后声明。类型形参跟在关键字class或typename之后声明。模板形参可以给出默认值（default arguments for template parameters）。

#### 模板的非类型形参

模板的非类型形参（template non-type parameter）允许为下述形式：

  - 整型或枚举型
  - 到对象的指针或函数指针
  - 到对象的引用或函数引用
  - [成员指针](../Page/类成员函数指针.md "wikilink")

模板的非类型参数被声明为数组或函数的，将被转换为指针或函数指针。例如：

` template<int a[4]> struct A { };`
` template<int f(int)> struct B { };`
` int i;`
` int g(int) { return 0;}`
` A<&i> x;`
` B<&g> y;`

模板的非类型形参允许用const或volatile限定（而模板的类型形参是不允许cv限定的）。模板的非类型形参是不允许声明为浮点型、class类型、void型。

#### 模板的模板参数

类模板的模板参数允许是另外一个类模板，这称为**模板的模板参数**（template template parameter），也译作“模板参数模板”。函数模板不允许有模板的模板参数。例如：

`template<template `<class T>` class X> class A { }; //类模板A的第二个参数是另外一个类模板X`
`template`<class T>` class B { };`
`A<B> a; //模板A的实际使用。其中的B是模板的模板实参（template template argument）`

#### 模板参数的默认值

模板形参可以给出默认值（default arguments for template parameters）。如果一个模板参数给出了默认值，那么模板形参列表中在其后声明的模板参数都应该给出默认值。例如：

`template<class T = char, class U, class V = int> class X { }; //编译出错，或者给出U的默认值，或者不给出T的默认值`

一个模板的各次声明给出的模板参数的默认值可以累积其效果。例如：

`template<class T, class U = int> class A;`
`template`<class T = float, class U>` class A;`
`template<class T, class U> class A {`
`  public:`
`     T x;`
`     U y;`
`};`
`A<> a; //a.x is float, and the type of a.y is int`

但是如果交换本示例第一行与第二行的次序，将编译报错。因为如果第一个模板参数T有了默认值，此时编译器必须已经知道其后的第二个模板参数U的默认值。

在同一个作用域（scope）中，不能对同一个模板的同一个参数多次声明其默认值。例如：

`template`<class T = char>` class X;`
`template`<class T = char>` class X { };//编译报错。如果在本行中不给出模板参数T的默认值将编译通过`

模板参数的作用域为从其声明之处至该模板的定义结束之处。因此可以使用一个模板参数作为其后声明的其他模板参数的一部分或默认值。例如：

`template<class V, V obj> class C; `
`template<class T, class U = T> class D { };`

#### 变量模板

变量模板（variable template）是[C++14](../Page/C++14.md "wikilink")引入的新的一个种类的模板。可用于在命名空间作用域声明一个变量。例如：

`template`<class T>
`constexpr T pi = T(3.1415926535897932385);  // variable template`
`template`<class T>
`T circular_area(T r) // function template`
`{`
`   return pi`<T>` * r * r; // pi`<T>` is a variable template instantiation`
`}`

可以在类作用域声明一个静态数据成员：

`struct matrix_constants`
`{`
`   template`<class T>
`   using pauli = hermitian_matrix<T, 2>; // alias template`
`   template`<class T>` static constexpr pauli`<T>` sigma1 = { { 0, 1 }, { 1, 0 } }; // static data member template`
`   template`<class T>` static constexpr pauli`<T>` sigma2 = { { 0, -1i }, { 1i, 0 } };`
`   template`<class T>` static constexpr pauli`<T>` sigma3 = { { 1, 0 }, { 0, -1 } };`
`};`

类的静态数据成员模板，也可以用类模板的非模板数据成员来实现：

`struct limits {`
`   template`<typename T>
`   static const T min; // declaration of a static data member template`
`};`
`template`<typename T>` const T limits::min = { }; // definition of a static data member template`
`template`<class T>` class X {`
`    static T s; // declaration of a non-template static data member of a class template`
`};`
`template`<class T>` T X`<T>`::s = 0; // definition of a non-template data member of a class template`

变量模板不能用作[模板的模板参数](../Page/模板的模板参数.md "wikilink")（template template arguments）。

### 模板的使用

使用模板时，可以在模板名字后面显式给出用尖括号括住的模板实参列表（template argument list）。对模板函数或类的模板成员函数，也可不显式给出模板实参，而是由编译器根据函数调用的上下文推导出模板实参，这称为**[模板参数推导](../Page/模板参数推导.md "wikilink")**。

如果模板参数使用其默认值，则在模板实参列表中可以忽略它。如果所有的模板参数都使用了默认值，模板实参列表为空，但仍然必须写出成对的尖括号。例如：

`template`<class T = int>` class X { };`
`X<> a; //编译通过`
`X b;   //编译报错`

对于作为类型的模板实参，不允许是局部类型（local type）、无链接性的类型（type with no linkage）、无名类型（unnamed type）或包括了这三种情形的复合类型。\[2\]但C++11以及允许本地类型作为模板实参。

## 示例

### 函数模板

以下以取最大值的函数模板maximum为例。此函数在编译时会自动产生对应参数类型的代码，而不用显式声明。

``` cpp
#include <iostream>

template <typename T>
inline const T& maximum(const T& x,const T& y)
{
   if(y > x){
      return y;
   }
   else{
      return x;
   }
}

int main(void)
{
   using namespace std;
   int a=3,b=7;
   float x=3.0,y=7.0;
   //Calling template function
   std::cout << maximum<int>(a,b) << std::endl;         //输出 7
   std::cout << maximum(a, b) << std::endl;             //自动补充类型声明
   std::cout << maximum<double>(x,y) << std::endl;  //输出 7
   return 0;
}
```

### 类模板

  - 以下以將元件指標的操作，封裝成类別模板ComPtr為例。

<!-- end list -->

``` cpp
#pragma once

template <typename Ty>
class ComPtr
{
protected:
    Ty* m_ptr;

public:

    ComPtr()
    {
        m_ptr = NULL;
    }

    ComPtr(const ComPtr& rhs)
    {
        m_ptr = NULL;
        SetComPtr(rhs.m_ptr);
    }

    ComPtr(Ty* p)
    {
        m_ptr = NULL;
        SetComPtr(p);
    }

    ~ComPtr()
    {
        Release();
    }

    const ComPtr& operator=(const ComPtr& rhs)
    {
        SetComPtr(rhs.m_ptr);
        return *this;
    }

    Ty* operator=(Ty* p)
    {
        SetComPtr(p);
        return p;
    }

    operator Ty* ()
    {
        return m_ptr;
    }

    Ty* operator->()
    {
        return m_ptr;
    }

    operator Ty** ()
    {
        Release();
        return &m_ptr;
    }

    operator void** ()
    {
        Release();
        return (void**)&m_ptr;
    }

    bool IsEmpty()
    {
        return (m_ptr == NULL);
    }

    void SetComPtr(Ty* p)
    {
        Release();

        m_ptr = p;
        if (m_ptr)
        {
            m_ptr->AddRef();
        }
    }

    void Release()
    {
        if (m_ptr)
        {
            m_ptr->Release();
            m_ptr = NULL;
        }
    }
};
```

### 模板的嵌套：成员模板

对于类中的模板成员函数、嵌套的成员类模板，可以在封闭类的内部或外部定义它们。当模板成员函数、嵌套类模板在其封闭类的外部定义时，必须以封闭类模板的模板参数（如果它们也是模板类）和成员模板的模板参数开头。\[3\]如下例：

``` cpp
template <typename C> class myc{
  public:
    template <typename S> C foo(S s);
};

//下行需要给出外部类与内部嵌套类的模板形参列表：
template<typename C> template <typename S> C myc<C>::foo(S s){
C var;
return var;
}

int main()
{
float f;
myc<int> v1;
v1.foo(f);
}
```

C++标准规定：如果外围的类模板没有特例化，里面的成员模板就不能特例化\[4\]。例如：

``` cpp
template <class T1> class A {
  template<class T2> class B {
      template<class T3> void mf1(T3);
      void mf2();
  };
};

template <> template <class X>
   class A<int>::B {
      template <class T> void mf1(T);
   };

template <> template <> template<class T>
    void A<int>::B<double>::mf1(T t) { }

template <class Y> template <>
     void A<Y>::B<double>::mf2() { } // ill-formed; B<double> is specialized but its enclosing class template A is not
```

## 依赖名字与typename关键字

一个模板中的依赖于一个模板参数（template parameter）的名字被称为**依赖名字** （dependent name）。当一个依赖名字嵌套在一个类的内部时，称为嵌套依赖名字（nested dependent name）。一个不依赖于任何模板参数的名字，称为**非依赖名字**（non-dependent name）。\[5\]

编译器在处理模板定义时，可能并不确定依赖名字表示一个类型，还是嵌套类的成员，还是类的静态成员。C++标准规定：如果解析器在一个模板中遇到一个嵌套依赖名字，它假定那个名字不是一个类型，除非显式用`typename`关键字前置修饰该名字。\[6\]

`typename`关键字有两个用途：

1.  常见的在模板定义中的模板形参列表，表示一个模板参数是类型参数。等同于使用`class`。
2.  使用模板类内定义的嵌套依赖类型名字时，显式指明这个名字是一个类型名。否则，这个名字会被理解为模板类的静态成员名。[C++11](../Page/C++11.md "wikilink")起，这一用途也可以出现在模板以外，尽管此时`typename`关键字不是必要的。

在下述情形，对嵌套依赖类型名字不需要前置修饰`typename`关键字：\[7\]

  - 派生类声明的基类列表中的基类标识符；
  - 成员初始化列表中的基类标识符；
  - 用`class`、`struct`、`enum`等关键字开始的类型标识符

因为它们的上下文已经指出这些标识符就是作为类型的名字。例如：

``` cpp

template <class T> class A: public T::Nested { //基类列表中的T::Nested
  public:
    A(int x) : T::Nested(x) {}; //成员初始化列表中的T::Nested
    struct T::type1 m; //已经有了struct关键字的T::type1
};

class B{
  public:
    class Nested{
      public:
           Nested(int x){};
    };
    typedef struct {int x;} type1;
};

int main()
{
  A<B> a(101);
  return 0;
}
```

## template关键字

`template`关键字有两个用途：

1.  常见的在模板定义的开始。
2.  模板类内部定义了模板成员函数或者嵌套的成员模板类。在模板中，当引用这样的模板成员函数或嵌套的成员模板类时，可以在`::`（作用域解析）运算符、`.`（以对象方式访问成员）运算符、`->`（以指针方式访问成员）运算符之后使用`template`关键字，随后才是模板成员函数名字或嵌套的成员模板类名字，这使得随后的左尖括号`<`被解释为模板参数列表的开始，而不是小于号运算符。[C++11](../Page/C++11.md "wikilink")起，这一用途也可以出现在模板以外，尽管此时`template`关键字不是必要的。例如：

<!-- end list -->

``` cpp
class A { public:
    template <class U> class B{
         public: typedef int INT;
    };
    template <class V> void foo(){}
};

template <typename T>
int f()
{
  typename T::template B<double>::INT i;
  i=101;
  T a, *p=&a;
  a.template foo<char>();
  p->template foo<long>();
  return 0;
}

int main()
{
  f<A>();
  A::B<double>::INT i;  // 自C++11起，也可写作typename A::template B<double>::INT i;
}
```

## 别名模板

别名模板（aliase template）是C++11引入的技术。在C++03标准中，可以用typedef给全特化模板定义新的类型名。但是不允许用typedef施加于偏特化模板上。例如：

``` cpp
template <typename First, typename Second, int Third>
class SomeType;

template <typename Second>
typedef SomeType<OtherType, Second, 5> TypedefName; // Illegal in C++03
```

C++11增加了给偏特化模板增加别名的功能，例如：

``` cpp
template <typename First, typename Second, int Third>
class SomeType;

template <typename Second>
using TypedefName = SomeType<OtherType, Second, 5>;
```

`using`在C++11中也可用于其他的类型别名的声明:

``` cpp
typedef void (*FunctionType)(double);       // Old style
using FunctionType1 = void (*)(double); // New introduced syntax
```

## 模板實例化

**模板实例化**（）是指在编译或链接时生成函数模板或类模板的具体实例源代码。ISO C++定义了两种模板实例化方法：隐式实例化（当使用实例化的模板时自动地在当前代码单元之前插入模板的实例化代码）、显式实例化（直接声明模板实例化）。在[C++](../Page/C++.md "wikilink")语言的不同实现中，模板编译模式（模板初始化的方法）大致可分为三种：

  - [Borland](../Page/Borland.md "wikilink")模型（**包含**模板编译模式）：[编译器生成每个](https://zh.wikipedia.org/wiki/编译器 "wikilink")[编译单元中遇到的所有的模板实例](https://zh.wikipedia.org/wiki/编译单元 "wikilink")，并存放在相应的[目标文件中](https://zh.wikipedia.org/wiki/目标文件 "wikilink")；[链接器](../Page/链接器.md "wikilink")合并相同的模板实例，生成[可执行文件](https://zh.wikipedia.org/wiki/可执行文件 "wikilink")。为了在每次模板实例化时模板的定义都是可见的，模板的声明与定义放在同一个.h文件中。这种方法的优点是[链接器](../Page/链接器.md "wikilink")只需要处理[目标文件](https://zh.wikipedia.org/wiki/目标文件 "wikilink")；这种方法的缺点是由于模板实例被重复编译，编译时间被加长了，而且不能使用系统的[链接器](../Page/链接器.md "wikilink")，需重新设计[链接器](../Page/链接器.md "wikilink")。
  - [Cfront/查询模型](https://zh.wikipedia.org/wiki/Cfront/查询 "wikilink")（**分离**（）模板编译模式）：[AT\&T公司](../Page/AT&T公司.md "wikilink")的[C++](../Page/C++.md "wikilink")[编译器](https://zh.wikipedia.org/wiki/编译器 "wikilink")[Cfront为解决模板实例化问题](https://zh.wikipedia.org/wiki/Cfront "wikilink")，增加了一个**模板仓库**，用以存放模板实例的代码并可被自动维护。当生成一个[目标文件时](https://zh.wikipedia.org/wiki/目标文件 "wikilink")，[编译器把遇到的模板定义与当前可生成的模板实例存放到模板仓库中](https://zh.wikipedia.org/wiki/编译器 "wikilink")。[链接时](https://zh.wikipedia.org/wiki/链接 "wikilink")，[链接器](../Page/链接器.md "wikilink")的包装程序（wrapper）首先调用[编译器生成所有需要的且不在模板仓库中的模板实例](https://zh.wikipedia.org/wiki/编译器 "wikilink")。这种方法的优点是[编译速度得到了优化](https://zh.wikipedia.org/wiki/编译 "wikilink")，而且可以直接使用系统的[链接器](../Page/链接器.md "wikilink")；这种方法的缺点是复杂度大大增加，更容易出错。使用这种模型的源程序通常把模板声明与非内联的模板成员分别放在.h文件与模板定义文件中，后者单独[编译](https://zh.wikipedia.org/wiki/编译 "wikilink")。
  - 混合（迭代）模型：[g++目前是基于](https://zh.wikipedia.org/wiki/gcc "wikilink")[Borland](../Page/Borland.md "wikilink")模型完成模板实例化。[g++未来将实现混合模型的模板实例化](../Page/GCC.md "wikilink")，即[编译器把](https://zh.wikipedia.org/wiki/编译器 "wikilink")[编译单元中的模板定义与遇到的当前可实现的模板实例存放在相应的](https://zh.wikipedia.org/wiki/编译单元 "wikilink")[目标文件中](https://zh.wikipedia.org/wiki/目标文件 "wikilink")；[链接器](../Page/链接器.md "wikilink")的包装程序（）调用[编译器生成所需的目前还没有实例化的模板实例](https://zh.wikipedia.org/wiki/编译器 "wikilink")；[链接器](../Page/链接器.md "wikilink")合并所有相同的模板实例。使用这种模型的源程序通常把模板声明与非内联的模板成员分别放在.h文件与模板定义文件中，后者单独[编译](https://zh.wikipedia.org/wiki/编译 "wikilink")。

[ISO](https://zh.wikipedia.org/wiki/ISO "wikilink") [C++](../Page/C++.md "wikilink")标准规定，如果隐式实例化模板，则模板的成员函数一直到引用时才被实例化；如果显式实例化模板，则模板所有成员立即都被实例化，所以模板的声明与定义在此处都应该是可见的，而且在其它程序[文本文件](../Page/文本文件.md "wikilink")使用了这个模板实例时用编译器选项抑制模板隐式实例化，或者模板的定义部分是不可见的，或者使用*template\<\> type FUN_NAME(type list)*的语句声明模板的特化但不实例化。

[g++的模板实例化](https://zh.wikipedia.org/wiki/gcc "wikilink")，目前分为三种方式：\[8\]

  - 不指定任何特殊的[编译器参数](https://zh.wikipedia.org/wiki/编译器 "wikilink")：按[Borland](../Page/Borland.md "wikilink")模型写的源代码能正常完成模板实例化，但每个编译单元将包含所有它用到的模板实例，导致在大的程序中无法接受的代码冗余。需要用[GNU](../Page/GNU.md "wikilink")的[链接器](../Page/链接器.md "wikilink")删除各个[目标文件中冗余的模板实例](https://zh.wikipedia.org/wiki/目标文件 "wikilink")，不能使用操作系统提供的[链接器](../Page/链接器.md "wikilink")。
  - 使用**-fno-implicit-templates**编译选项：在生成[目标文件时完全禁止隐式的模板实例化](https://zh.wikipedia.org/wiki/目标文件 "wikilink")，所有模板实例都显式的写出来，可以存放在一个单独的源文件中；也可以存放在各个模板定义文件中。如果一个很大的源文件中使用了各个模板实例，这个源文件不用-fno-implicit-templates选项编译，就可以自动隐式的生成所需要的模板实例。在生成库文件时这个编译选项特别有用。
  - 使用**-frepo**编译选项：在生成每个[目标文件时](https://zh.wikipedia.org/wiki/目标文件 "wikilink")，把需要用到的当前可生成的模板实例存放在相应的**.rpo**文件中。[链接器](../Page/链接器.md "wikilink")包装程序(wrapper)—[collect2将删除](https://zh.wikipedia.org/wiki/collect2 "wikilink").rpo文件中冗余的模板实例并且修改相应的.rpo文件，使得[编译器可以利用](https://zh.wikipedia.org/wiki/编译器 "wikilink").rpo文件知道在那里正确放置、引用模板实例，并重新编译生成受影响的[目标文件](https://zh.wikipedia.org/wiki/目标文件 "wikilink")。由操作系统的通用的[链接器](../Page/链接器.md "wikilink")生成[可执行文件](https://zh.wikipedia.org/wiki/可执行文件 "wikilink")。这对[Borland](../Page/Borland.md "wikilink")模型是很好的模板实例化方法。对于使用[Cfront模型的软件](https://zh.wikipedia.org/wiki/Cfront "wikilink")，需要修改源代码，在模板头文件的末尾加上*\#include \<tmethods.cc\>*。不过[MinGW](../Page/MinGW.md "wikilink")中不包含[链接器](../Page/链接器.md "wikilink")包装程序[collect2](https://zh.wikipedia.org/wiki/collect2 "wikilink")，故不使用此方法。对于库(library)，建议使用显式实例化方法。
  - 另外，[g++扩展了ISO](https://zh.wikipedia.org/wiki/gcc "wikilink") [C++](../Page/C++.md "wikilink")标准，用**extern**[关键字指出模板实例在其它编译单元中显式声明](https://zh.wikipedia.org/wiki/关键字 "wikilink")（这已经被C++11标准接受）；用**inline**[关键字实例化](https://zh.wikipedia.org/wiki/关键字 "wikilink")[编译器支持的数据](https://zh.wikipedia.org/wiki/编译器 "wikilink")（如[类的](https://zh.wikipedia.org/wiki/类 "wikilink")[虚表](https://zh.wikipedia.org/wiki/虚表 "wikilink")）但不实例化模板成员；用**static**[关键字实例化模板的](https://zh.wikipedia.org/wiki/关键字 "wikilink")[静态数据成员但不实例化其它非静态的模板成员](https://zh.wikipedia.org/wiki/静态数据成员 "wikilink")。
  - [g++不支持模板实例化的](https://zh.wikipedia.org/wiki/gcc "wikilink")**export**[关键字](https://zh.wikipedia.org/wiki/关键字 "wikilink")（此关键字的这个用法已在C++11标准里被取消）。

[VC++](https://zh.wikipedia.org/wiki/VC++ "wikilink")7.0中必须类模板实例化只有[Borland](../Page/Borland.md "wikilink")模型；函数模板一般隐式实例化，自5.0版以后也可显式实例化。

## 参考文献

<references/>

[de:Vorlage (Datenverarbeitung)](https://zh.wikipedia.org/wiki/de:Vorlage_\(Datenverarbeitung\) "wikilink") [fr:Modèle (informatique)](https://zh.wikipedia.org/wiki/fr:Modèle_\(informatique\) "wikilink")

[Category:C++](https://zh.wikipedia.org/wiki/Category:C++ "wikilink")

1.  [MSDN：嵌套的类模板](http://msdn.microsoft.com/zh-cn/library/71dw8xzh.aspx)
2.  §14.3.1/2 from the 2003 C++ Standard: A local type, a type with no linkage, an unnamed type or a type compounded from any of these types shall not be used as a template-argument for a template type-parameter.
3.
4.  C++11标准：§14.7.3，¶16规定：the declaration shall not explicitly specialize a class member template if its enclosing class templates are not explicitly specialized as well
5.  C++11标准：§14.6，¶1
6.  C++11标准§14.6，¶2规定：A name used in a template declaration or definition and that is dependent on a template-parameter is assumed not to name a type unless the applicable name lookup finds a type name or the name is qualified by the keyword typename.
7.  C++11标准§14.6，¶5规定
8.