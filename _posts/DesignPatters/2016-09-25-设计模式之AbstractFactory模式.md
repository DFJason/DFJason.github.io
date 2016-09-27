---
layou: post
title: 设计模式之AbstractFactory模式
categories:[blog]
tags:[DesignPatterns]
description:学习笔记

---

### AbstractFactory模式解决的问题
需要创建**一组**相关或者相互依赖的对象

### 典型模式结构图
[AbstractFactory](https://cnlg.github.io/images/DesignPatters/AbstractFactory/AFactory.png)


### 演示代码

#### Product.h


```
#pragma once
#ifndef _PRODUCT_H_
#define _PRODUCT_H_

class AbstractProductA   //创建第一个接口类
{
public:
	virtual ~AbstractProductA();   //这里用的是纯虚析构函数
protected:
	AbstractProductA();
private:
};
 
class AbstractProductB   //创建第二个接口类
{
public:
	virtual ~AbstractProductB();
protected:
	AbstractProductB();
private:
};

class ProductA1 :public AbstractProductA   //继承关系
{
public:
	ProductA1();
	~ProductA1();
protected:
private:
};

class ProductA2 :public AbstractProductA  //继承关系
{
public:
	ProductA2();
	~ProductA2();
protected:
private:
};

class ProductB1 :public AbstractProductB  //继承关系
{
public:
	ProductB1();
	~ProductB1();
protected:
private:
};

class ProductB2 :public AbstractProductB  //继承关系
{
public:
	ProductB2();
	~ProductB2();
protected:
private:
};
#endif
```

#### Product.cpp

```
#include "Product.h"
#include "iostream"
using namespace std;

AbstractProductA::~AbstractProductA()
{
}

AbstractProductA::AbstractProductA()
{
}

AbstractProductB::~AbstractProductB()
{
}

AbstractProductB::AbstractProductB()
{
}

ProductA1::ProductA1()  //构造函数
{
	cout << "ProductA1..." << endl;
}

ProductA1::~ProductA1()
{
}

ProductA2::ProductA2()  //构造函数
{
	cout << "ProductA2..." << endl;
}

ProductA2::~ProductA2()
{

}

ProductB1::ProductB1()  //构造函数
{
	cout << "ProductB1..." << endl;
}

ProductB1::~ProductB1()
{
}

ProductB2::ProductB2()  //构造函数
{
	cout << "ProductB2..." << endl;
}

ProductB2::~ProductB2()
{
}

```

#### AbstractFactory.h

```
#ifndef _ABSTRACTFACTORY_H_
#define _ABSTRACTFACTORY_H_

class AbstractProductA;
class AbstractProductB;

class AbstractFactory  //接口类
{
public:	
	virtual ~AbstractFactory();
	virtual AbstractProductA *CreateProductA() = 0;  //接口，注意返回类型是上面的基类
	virtual AbstractProductB *CreateProductB() = 0;  //接口
protected:
	AbstractFactory();
};

class ConcreteFactory1 :public AbstractFactory   //继承自接口
{
public:
	ConcreteFactory1();
	~ConcreteFactory1(); 
	AbstractProductA * CreateProductA();     //对接口的实现
	AbstractProductB * CreateProductB();
protected:
private:
};

class ConcreteFactory2 :public AbstractFactory  //继承自接口
{
public:
	ConcreteFactory2();
	~ConcreteFactory2();

	AbstractProductA* CreateProductA();    //对接口的实现
	AbstractProductB* CreateProductB();

protected:
private:
};


#endif

```
#### AbstractFactory.cpp

```
#include "AbstractFactory.h"
#include "Product.h"
#include <iostream>
using namespace std;

#include "AbstractFactory.h"


AbstractFactory::AbstractFactory()
{
}


AbstractFactory::~AbstractFactory()
{
}

ConcreteFactory1::ConcreteFactory1()
{
}

ConcreteFactory1::~ConcreteFactory1()
{
}

AbstractProductA * ConcreteFactory1::CreateProductA()  //接口的实现
{
	return new ProductA1();
}

AbstractProductB * ConcreteFactory1::CreateProductB()  //接口的实现
{ 
	return new ProductB1();
}

ConcreteFactory2::ConcreteFactory2()
{
}

ConcreteFactory2::~ConcreteFactory2()
{
}

AbstractProductA * ConcreteFactory2::CreateProductA()  //接口的实现
{
	return new ProductA2();
}

AbstractProductB * ConcreteFactory2::CreateProductB()   //接口的实现
{
	return new ProductB2();
}

```

#### 测试代码

```
#include "AbstractFactory.h"
#include <iostream>
using namespace std;

int main()
{
	AbstractFactory* cf1 = new ConcreteFactory1();   //创建一个“工厂”
	cf1->CreateProductA();                           //实例化需要创建的类
	cf1->CreateProductB();

	AbstractFactory* cf2 = new ConcreteFactory2();  //创建另一个“工厂”
	cf2->CreateProductA();                          //实例化需要创建的类
	cf2->CreateProductB(); 
	while (1);
	
	return 0;
}
```


#### 运行效果
[AbstractFactory](https://cnlg.github.io/images/DesignPatters/AbstractFactory/yunxing.png)


#### 代码说明
测试程序中，创建一组对象（ProductA1,ProductA2)的时候，只要维护一个创建对象（ConcreteFactory1),简化了维护成本和工作


#### 参考资料
设计模式精解－GoF 23种设计模式解析附C++实现源码




