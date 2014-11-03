---
layout: post
title: Default Constructor
category: 学习
tags: 深度探索c++对象模型
keywords: 缺省构造函数
description: 
---


学习缺省构造函数时候，首先要明白什么时候需要构建，c++ Annotated Reference Manual（ARM）中提出：“default constructor ...在需要的时候被编译器产生”，这个需要的时候是在编译器需要的时候，而不是程序需要的时候。程序需要的时候比如变量的零初始化是程序员需要完成的事情。当然，这边说的是“nontrivial default constructor”。


存在两种误解：
1. 任何class如果没有定义default constructor，就会被合成出来
2. 编译器合成出来的default constructor会明确设定class 中的每一个data member的默认值


编译器合成出“nontrivial default constructor”的四种情况如下：

### （一）“带有Default Constructor”的Member Class Object

这种情况主要指类的内含时：

```
	class Foo{ public: Foo();Foo(int)...};
	class Bar{ public: Foo foo;char *str};

	void foo_bar()
	{
		Bar bar;//Bar的构造函数中Bar：：foo必须在此处初始化，这时如果Bar中没有构造函数，编译器会生成，如果有，则把foo.Foo:Foo()；插入到其构造函数中

		if(str)
	}
```

### （二）“带有Default Constructor”的Base Class

这种情况跟上面的情况相似

### （三）“带有一个 Virtual Function”的Class

两种情况如下：
1. class声明（或继承）一个virtual function。
2. class派生自一个继承串链，其中有一个或更多的virtual base classes。

```
	class Widget{
	public:
		virtual void flip()=0;
	};

	void flip( const widget& widget){ widget.flip();}

	void foo()
	{
		Bell b;
		Whistle w;
		flip(b);
		flip(w);
	}
```

1. 编译器会生成一个virtual function table（vtbl） 内放virtual function 的地址
2. 编译器会生成一个pointer指向vtbl的地址
3. 改写 widget。flip--->（*widget.vptr[1]）  1 为virtual table中的索引

### （四）“带有一个virtual Base Class”的Class

例如C继承A

```
	void foo(const A* pa) {pa->i=1024;}

	main()
	{
		foo(new A);
		foo(new C);
	}
```

由于多态的存在，具体执行什么样的代码可能延迟到执行期才决定下来

```
	void foo(const A* pa) {pa->_vbcx->=1024;}//编译器可能的转变操作
```

其中，_vbcx表示编译器产生的指针，指向virtual base class X


