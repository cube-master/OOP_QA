# Fundamentals of Object-Oriented Programming

## Lecture 11Hailong Yao

## hailongyao@tsinghua.edu.cn

子曰：“视其所以，观其所由，察其所安。人焉廋

```
哉？人焉
```
```
廋
哉？”
```

## Overview

#### Design PatternFactory Method (

##### 工厂方法

##### )

##### Abstract Factory (

##### 抽象工厂

##### )

##### Observer (

##### 观察者

##### )

#### Summary

```
2022/5/
```

## Last Class

### Design Pattern: Singleton

```
2022/5/
```

## Last Class

### Design Pattern: Adapter

```
2022/5/
```
```
Inheritance
```
```
Composition
```
### Object Adapter (

### 对象适配器

### )

```
Reference/pointer
```

## Last Class

### Design Pattern: Simple Factory

```
2022/5/
```
```
SimpleFactory
+ create(type: string): Product
```
```
Client Reference/pointer
```
```
ConcreteProductA+ operation1(): void+ operation2(): void
```
```
Inheritance
```
```
ConcreteProductB+ operation1(): void+ operation2(): void
<<interface>> Product+ operation1(): void+ operation2(): void
Creates
```

## Question in Last Week ...Does^

##### Simple

##### Factory

##### comply

##### with

##### the^ Open

##### ‐

##### Closed

##### Principle?

**We**^ **will**

**discuss**

**on**^ **this**

**next**^

**week.**

##### NO! When

**a**^ **new**

**product**

**is**^ **added,**

**we**^ **have**

**to**^ **modify**

**class**^

**_SimpleFactory_**

```
.
 Violates
```
```
the^ Closed
Principle
```
```
2022/5/
```

## The Simple Factory

##### Class diagram

```
2022/5/
```
```
VeggiePizzasellPizza()
```
```
PizzasellPizza()
Inheritance
```
```
CheesePizzasellPizza()
```
```
SimplePizzaFactorycreatePizza(PizzaType) : PizzaCompositionPizzaStoreorderPizza() : Pizzam_factory
```
```
Creates
```

### Problem with the Simple Factory

##### What if we want to add the PepperoniPizza?Need to modify both enum

```
and
createPizza()
```
```
2022/5/
```
```
enumPizzaType {CHEESE,
```
```
VEGGIE,
```
```
PEPPERONI};
```
```
class
```
```
SimplePizzaFactory {
public
```
```
: Pizza*^ createPizza
```
```
(PizzaType type)
```
```
{
```
```
Pizza^
```
```
*pizza
```
```
{^0 };
switch
```
```
(type)
```
```
{
casePEPPERONI:pizza
```
```
=^ new
```
```
PepperoniPizza
```
```
{};
```
```
break; caseCHEESE:pizza^
```
```
=^ new
```
```
CheesePizza
```
```
{};
```
```
break; caseVEGGIE:pizza^
```
```
=^ new
```
```
VeggiePizza
```
```
{};
```
```
break; default: cerr <<
```
```
"Unknown
```
```
Pizza
```
```
Type"
```
```
<<^
```
```
endl;
```
```
exit (‐
```
```
1 );
} return
```
```
pizza;
}};
```
**This**^ **does**

**not**^ **satisfy**

**the**^ **Open**

**‐**

**Closed**

**Principle**

**!**


```
2022/5/
```
## Factory

## method

## （工厂方法）

##### —— Creational

##### Pattern

##### ( 创建型模式

##### )


## What is the Problem?

##### SimplePizzaFactory does not comply with the Open-Closed Principle there is only one factory for all types of pizza Need one-to-one correspondence between pizza and factory (

##### 披萨与工厂一一对应

##### )

## For a new type of pizza, just add a new pizza factory, and no need to modify existing factories  Comply with the Open-Closed PrincipleThis is a new design pattern Factory Method

## （工厂方法）

```
2022/5/
```

### Class Diagram: Factory Method

```
2022/5/
```
```
VeggiePizzasellPizza()
```
```
PizzasellPizza()
Inheritance
```
```
CheesePizzasellPizza()
PepperoniPizzasellPizza()
```
```
VeggiePizzaFactorycreatePizza() : Pizza
```
```
PizzaFactorycreatePizza() : Pizza
Inheritance
```
```
CheesePizzaFactorycreatePizza() : Pizza
PepperoniPizzaFactorycreatePizza() : Pizza
```
```
PizzaStore
```
```
Reference/pointer
```
```
Creates
```

## Pizza by Factory Method (1)Pizza store using Factory MethodCheesePizza and VeggiePizze are defined similarly as in Simple Factory example

```
#ifndef __PIZZA__#define
```
```
__PIZZA__
class
```
```
Pizza
```
```
{
//cut,
```
```
box^
```
```
and^ sell
```
```
pizza
```
```
virtual
```
```
void
```
```
sellPizza
```
```
()^ =^
```
```
0 ;
```
```
}; #endif
```
```
Pizza.h
```
```
2022/5/
```

##### First define an interface class (

##### 接口类

##### ) for “factory”

##### Then provide implementation classes (

##### 实现类

##### ) for

##### different factories corresponding to different types of pizza

```
#ifndef __PIZZA_FACTORY__#define
```
```
__PIZZA_FACTORY__
#include
```
```
"Pizza.h"
class
```
```
PizzaFactory {
public
```
```
: virtualPizza*
```
```
createPizza
```
```
()^ =^
```
```
0 ;
```
```
}; #endif
```
```
PizzaFactory.h
```
```
2022/5/
```
## Pizza by Factory Method (2)


```
#ifndef __CHEESE
```
```
_PIZZA_FACTORY__
```
```
#define
```
```
__CHEESE_PIZZA_FACTORY__
#include
```
```
"Pizza.h"
#include
```
```
"CheesePizza.h"
class
```
```
CheesePizzaFactory :
```
```
public
```
```
PizzaFactory {public
```
```
: Pizza*^ createPizza
```
```
()^ {
```
```
Pizza
```
```
*pizza
```
```
{^ new
```
```
CheesePizza
```
```
{}^ };
return
```
```
pizza;
} };#endif
```
```
CheesePizzaFactory.h
```
```
#ifndef __VEGGIE
```
```
_PIZZA_FACTORY__
```
```
#define
```
```
__VEGGIE_PIZZA_FACTORY__
#include
```
```
"Pizza.h"
#include
```
```
"VeggiePizza.h"
class
```
```
VeggiePizzaFactory :
```
```
public
```
```
PizzaFactory {public
```
```
: Pizza*^ createPizza
```
```
()^ {
```
```
Pizza
```
```
*pizza
```
```
{^ new
```
```
VeggiePizza
```
```
{}^ };
return
```
```
pizza;
} };#endif
```
```
VeggiePizzaFactory.h
```
```
2022/5/
```
## Pizza by Factory Method (3)


```
#ifndef __PIZZA_STORE__#define
```
```
__PIZZA_STORE__
#include
```
```
"Pizza.h"
#include
```
```
"PizzaFactory.h"
//class
```
```
PizzaStore is
```
```
decoupled
```
```
from
```
```
instantiation
```
```
and^
```
```
concrete
```
```
classes
class
```
```
PizzaStore {
public
```
```
: Pizza^ * orderPizza
```
```
(PizzaFactory*
```
```
factory)
```
```
{
```
```
Pizza
```
```
*pizza
```
```
{^ factory
```
```
‐> createPizza
```
```
()^ };
```
```
pizza
```
```
‐> sellPizza
```
```
();
```
```
return
```
```
pizza;
} }; #endif
```
```
PizzaStore.h
```
```
2022/5/
```
## Pizza by Factory Method (4)


```
#include
```
```
"PizzaStore.h"
#include
```
```
"PizzaFactory.h"
#include
```
```
"CheesePizzaFactory.h"
#include
```
```
"VeggiePizzaFactory.h"
int main
```
```
()^ {
PizzaStore *store
```
```
{^ new
```
```
PizzaStore
```
```
{}^ };
```
```
PizzaFactory *factory
```
```
{^ new
```
```
CheesePizzaFactory
```
```
{}^ };
```
```
Pizza
```
```
*pizza
```
```
{^ store
```
```
‐> orderPizza
```
```
(factory)
```
```
};
```
```
delete
```
```
pizza;
delete
```
```
factory;
factory
```
```
=^ new
```
```
VeggiePizzaFactory
```
```
{};
```
```
pizza
```
```
=^ store
```
```
‐> orderPizza
```
```
(factory);
```
```
delete
```
```
pizza;
delete
```
```
factory;
delete
```
```
store;
return
```
```
0 ;
}
```
```
main.cpp
```
**Sell a CheesePizzaSell a VeggiePizza**

**Output**

```
2022/5/
```
##### Demo

## Pizza by Factory Method (5)


## New Type of Pizza

```
#ifndef __HAWAIIAN_PIZZA__#define
```
```
__HAWAIIAN_PIZZA__
#include
```
```
<iostream>
#include
```
```
"Pizza.h"
using
```
```
namespace
```
```
std;
```
```
class
```
```
HawaiianPizza :
```
```
public
```
```
Pizza
```
```
{
public
```
```
: void sellPizza
```
```
()^ {
cout <<
```
```
"Hawaiian
```
```
Pizza"
```
```
<<^
```
```
endl;} };#endif
```
```
HawaiianPizza.h
```
```
#ifndef __HAWAII
```
```
AN_PIZZA_FACTORY__
```
```
#define
```
```
__HAWAIIAN_PIZZA_FACTORY__
#include
```
```
"Pizza.h"
#include
```
```
"HawaiianPizza.h"
class
```
```
HawaiianPizzaFactory :
```
```
public
```
```
PizzaFactory {public
```
```
: Pizza*^ createPizza
```
```
()^ {
```
```
Pizza
```
```
*pizza
```
```
{^ new
```
```
HawaiianPizza
```
```
{}^ };
return
```
```
pizza;
} };#endif
```
```
HawaiianPizzaFactory.h
```
#### A new type of pizza needs two new classes

```
2022/5/
```

## User Program

```
#include
```
```
"PizzaStore.h"
#include
```
```
"PizzaFactory.h"
#include
```
```
"CheesePizzaFactory.h"
#include
```
```
"VeggiePizzaFactory.h"
int main
```
```
()^ {
PizzaStore *store
```
```
{^ new
```
```
PizzaStore
```
```
{}^ };
```
```
PizzaFactory *factory
```
```
{^ new
```
```
HawaiianPizzaFactory
```
```
{}^ };
```
```
Pizza
```
```
*pizza
```
```
{^ store
```
```
‐> orderPizza
```
```
(factory)
```
```
};
```
```
delete
```
```
pizza;
delete
```
```
factory;
delete
```
```
store;
return
```
```
0 ;
}
```
```
2022/5/
```

## Factory Method 2022/5/

##### Creational design pattern

```
Inheritance
```
```
Creates
```

### Factory Method and OOP

### Principle

**Dependency Inversion Principle (** • **Interface class: Pizza, PizzaFactory** • **Implementation classes: CheesePizza, CheesePizzaFactory...** • **PizzaStore does not reference any implementation class**

依赖倒置原则

**)**

**The open-closed principle** • **Open: for a new type of pizza, add two implementation classes for Pizza and PizzaFactory** • **Closed: no need to modify existing class/code (except user program in main.cpp)Partition different tasks and assign them to different objects — Single Responsibility Principle** • **Separate different Pizza creation tasks** • **Assign different types of pizza to different pizza factories**

（单一责任原则）

```
2022/5/
```

### Parameterized Factory Method

### ( 参数化工厂方法

### )

##### Problems with Factory MethodFor a new type of pizza, two new implementation classes are needed: one for pizza, one for factoryThe number of classes increases dramaticallyParameterized Factory Method = Simple Factory + Factory MethodOne factory class can manufacture different types of products 

**avoid dramatic increase in the number of classesStill easy for extension by adding new factories**

 **comply**

**with the Open-Closed Principle**

```
class
```
```
PizzaFactory
```
```
{
```
```
public:virtual
```
```
Pizza*
```
```
createPizza()
```
```
=^ 0;
```
```
class };
```
```
PizzaFactory {
public
```
```
: virtualPizza*
```
```
createPizza(string
```
```
type)
```
```
=^0 ;
```
```
class };
```
```
PizzaFactory {
public
```
```
: virtualPizza*
```
```
createPizza(string
```
```
type)
```
```
=^0 ;
```
```
};
```
```
2022/5/7
```

```
2022/5/7
```
## Abstract

## Factory

## （抽象工厂）

##### —— Creational

##### Pattern

##### ( 创建型模式

##### )


## New Problem

##### What if the pizza store wants to sell

##### hamburger

##### ?

**Cheeseburger, veggieburger, etc.So we have several**

**series**

**of food (**

一系列口味的食品

**)**

```
Cheese series: cheesepizza, cheeseburgerVeggie series: veggiepizza, veggieburgerHawaiian series: hawaiianpizza, hawaiianburger
```
##### Another example: for creating database users/administrators (

##### 数据库用户及管理员

##### )

###### SQL Server family, Oracle family, mongodb family

###### ,

##### etc.Different database series need to create families of different users and administratorsAbstract factory (

##### 抽象工厂

##### ) can be used for creating

##### series of related objects

```
2022/5/7
```

### Class Diagram of the Example

```
2022/5/7
```
```
VeggiePizzasellPizza()
```
```
PizzasellPizza()
Inheritance
```
```
CheesePizzasellPizza()
```
```
VeggiePBFactorycreatePizza() : PizzacreateBurger : Burger
```
```
PBFactorycreatePizza() : Pizza
createBurger() : Burger Inheritance
```
```
CheesePBFactorycreatePizza() : PizzacreateBurger : Burger
```
```
VeggieBurgersellBurger()
```
```
BurgersellBurger()
Inheritance
```
```
CheeseBurgersellBurger()
```
```
PBStore
```
```
Reference/pointer
```
```
Creates
```

#### Class Diagram of Abstract Factory

```
2022/5/7
```
```
ProductA1
```
```
AbstractProductA
Inheritance
```
```
ProductA2
```
```
ConcreteFactory1createProductA()createProductB()
```
```
AbstractFactorycreateProductA()createProductB()
Inheritance
```
```
ConcreteFactory2createProductA()createProductB()
```
```
AbstractProductB InheritanceProductB1
```
```
ProductB2
```
```
Client
```
##### Creational design pattern

```
Reference/pointer
```
```
Creates
```

```
2022/5/7
```
```
#ifndef __PB_FACTORY__#define
```
```
__PB_FACTORY__
#include
```
```
"Pizza.h"
#include
```
```
"Burger.h"
class
```
```
PBFactory {
public
```
```
: virtualPizza*
```
```
createPizza
```
```
()^ =^
```
```
0 ;
```
```
virtual
```
```
Burger*
```
```
createBurger
```
```
()^ =^
```
```
0 ;
```
```
}; #endif
```
**PBFactory.h**

##### Demo


```
2022/5/7
```
#ifndef __CHEESE_PB_FACTORY__#define

```
__CHEESE_PB_FACTORY__
#include
```
```
"Pizza.h"
#include
```
```
"CheesePizza.h"
#include
```
```
"Burger.h"
#include
```
```
"CheeseBurger.h"
#include
```
```
"PBFactory.h"
class
```
```
CheesePBFactory :
```
```
public
```
```
PBFactory {
```
```
public
```
```
: Pizza*^ createPizza
```
```
()^ {
```
```
Pizza
```
```
*pizza
```
```
{^ new
```
```
CheesePizza
```
```
{}^ };
```
```
return
```
```
pizza;
} Burger*
```
```
createBurger
```
```
()^ {
```
```
Burger
```
```
*burger
```
```
{^ new
```
```
CheeseBurger
```
```
{}^ };
```
```
return
```
```
burger;
} };#endif
```
**CheesePBFactory.h**


```
2022/5/7
```
#ifndef __VEGGIE_PB_FACTORY__#define

```
__VEGGIE_PB_FACTORY__
#include
```
```
"Pizza.h"
#include
```
```
"VeggiePizza.h"
#include
```
```
"Burger.h"
#include
```
```
"VeggieBurger.h"
class
```
```
VeggiePBFactory :
```
```
public
```
```
PBFactory {
```
```
public
```
```
: Pizza*^ createPizza
```
```
()^ {
```
```
Pizza
```
```
*pizza
```
```
{^ new
```
```
VeggiePizza
```
```
{}^ };
```
```
return
```
```
pizza;
} Burger*
```
```
createBurger
```
```
()^ {
```
```
Burger
```
```
*burger
```
```
{^ new
```
```
VeggieBurger
```
```
{}^ };
```
```
return
```
```
burger;
} };#endif
```
**VeggiePBFactory.h**


```
2022/5/7
```
#ifndef __PB_STORE__#define

```
__PB_STORE__
#include
```
```
"Pizza.h"
#include
```
```
"Burger.h"
#include
```
```
"PBFactory.h"
//client
```
```
class
```
```
PBStore is
```
```
decoupled
```
```
from
```
```
instantiation
```
```
and^
```
```
concrete
```
```
classes
class
```
```
PBStore {
public
```
```
: Pizza^ * orderPizza
```
```
(PBFactory*
```
```
factory)
```
```
{
```
```
Pizza
```
```
*pizza
```
```
{^ factory
```
```
‐> createPizza
```
```
()^ };
```
```
pizza
```
```
‐> sellPizza
```
```
();
```
```
return
```
```
pizza;
} Burger
```
```
* orderBurger
```
```
(PBFactory*
```
```
factory)
```
```
{
```
```
Burger
```
```
*burger
```
```
{^ factory
```
```
‐> createBurger
```
```
()^ };
```
```
burger
```
```
‐> sellBurger
```
```
();
```
```
return
```
```
burger;
} };#endif
```
**PBStore.h**


```
2022/5/7
```
#ifndef __BURGER__#define

```
__BURGER__
class
```
```
Burger
```
```
{
public
```
```
: virtualvoid
```
```
sellBurger
```
```
()^ =^0
```
```
;^ //^ box,
```
```
sell,
```
```
etc.
```
```
};#endif
```
**Burger.h**

```
#ifndef __CHEESE_BURGER__#define
```
```
__CHEESE_BURGER__
#include
```
```
<iostream>
#include
```
```
"Burger.h"
using^
```
```
namespace
```
```
std;
class
```
```
CheeseBurger :
```
```
public
```
```
Burger
```
```
{
```
```
public
```
```
: void sellBurger
```
```
()^ {^ cout <<
```
```
"Sell
```
```
a^ CheeseBurger"
```
```
<<^ endl;
```
```
} };#endif
```
**CheeseBurger.h**

```
#ifndef __VEGGIE_BURGER__#define
```
```
__VEGGIE_BURGER__
#include
```
```
<iostream>
#include
```
```
"Burger.h"
using^
```
```
namespace
```
```
std;
class
```
```
VeggieBurger :
```
```
public
```
```
Burger
```
```
{
```
```
public
```
```
: void sellBurger
```
```
()^ {^ cout <<
```
```
"Sell
```
```
a^ VeggieBurger"
```
```
<<^ endl;
```
```
} };#endif//
```
```
Pizza.h,
```
```
CheesePizza.h and
```
```
VeggiePizza.h are
```
```
the^
```
```
same as the previous version
```
**VeggieBurger.h**


```
2022/5/7
```
#include

"PBStore.h"
#include

```
"PBFactory.h"
#include
```
```
"CheesePBFactory.h"
#include
```
```
"VeggiePBFactory.h"
int main
```
```
()^ {
PBStore *store
```
```
{^ new
```
```
PBStore
```
```
{}^ };
```
```
PBFactory *factory
```
```
{^ new
```
```
CheesePBFactory
```
```
{}^ };^
```
```
Pizza
*pizza
```
```
{^ store
```
```
‐> orderPizza
```
```
(factory)
```
```
};
```
```
Burger
```
```
*burger
```
```
{^ store
```
```
‐> orderBurger
```
```
(factory)
```
```
};
```
```
delete
```
```
pizza;
delete
```
```
burger;
delete
```
```
factory;
factory
```
```
=^ new
```
```
VeggiePBFactory
```
```
{};
```
```
pizza
=^ store
```
```
‐> orderPizza
```
```
(factory);
```
```
burger
```
```
=^ store
```
```
‐> orderBurger
```
```
(factory);
```
```
delete
```
```
pizza;
delete
```
```
burger;
delete
```
```
factory;
delete
```
```
store;
return
```
```
0 ;
}
```
```
main.cpp
Series 1: cheese Series 2: veggie
Sell a CheesePizzaSell a CheeseBurgerSell a VeggiePizzaSell a VeggieBurger
```
**Output**


## Abstract Factory (

## 抽象工厂

## )

#### Abstract factoryProvide an interface for creating families of related or dependent (

##### 彼此相关或依赖的

##### ) objects

#### without specifying the objects’ concrete classesOOP design principleDependency inversion principleAbstractFactory, AbstractProductA, AbstractProductBOpen-closed principleOpen for adding new families of productsClosed for modifying existing codesSingle responsibility principleEach factory is responsible for creating one family (

系列 **)**

**of products**

```
2022/5/7
```

### Example of Abstract Factory

##### ProblemDesign a user interface toolkit that supports multiple look-and-feel (

##### 观感

##### ) standards

##### Different look-and-feels define different appearances and behaviors for user interface “widgets” (

##### 部件

##### ) like scroll bars (

##### 滚动条

##### ),

##### windows (

##### 窗口

##### ), and buttons (

##### 按钮

##### )

##### How to make it easy to add new look-and-feels?

```
2022/5/7
```

## “Original” Design

```
class
```
```
WidgetFactory {
private
```
```
: intstyle;......
public
```
```
: Window*
```
```
createWindow
```
```
();
```
```
Scroll*
```
```
createScroll
```
```
();
```
```
......
}; Window*
```
```
WidgetFactory
```
```
:: createWindow
```
```
()^ {
```
```
if(style
```
```
==^0
```
```
)^ {
return
```
```
new
```
```
Style1Window;
```
```
}^ else
```
```
if(style
```
```
==^1
```
```
)^ {
```
```
return
```
```
new
```
```
Style2Window;
```
```
}^ else
```
```
{ return^
```
```
newDefaultStyleWindow;
}
} //switch
```
```
‐case based createScroll()...
```
**This**^ **does**

**not**^ **satisfy**

**the**^ **Open**

**‐**

**Closed**

**Principle**

```
2022/5/7
```

## Use Abstract Factory

```
class
```
```
WidgetFactory {
public
```
```
: virtual
```
```
Window*
```
```
createWindow
```
```
();
```
```
virtual
```
```
Scroll*
```
```
createScroll
```
```
();
```
```
......
};class
```
```
LinuxFactory :
```
```
public
```
```
WidgetFactory {
```
```
public
```
```
: Window*
```
```
createWindow
```
```
();
```
```
Scroll*
```
```
createScroll
```
```
();
```
```
......
};class
```
```
WindowsFactory :
```
```
public
```
```
WidgetFactory {
```
```
public
```
```
: Window*
```
```
createWindow
```
```
();
```
```
Scroll*
```
```
createScroll
```
```
();
```
```
......
};
```
```
2022/5/7
```

Window*

LinuxFactory

:: **createWindow**

()^ {

```
return
```
```
new
```
```
LinuxWindow;
```
```
} Scroll*
```
```
LinuxFactory
```
```
:: createScroll
```
```
()^ {
```
```
return
```
```
new
```
```
LinuxScroll;
```
```
} ...... Window*
```
```
WindowsFactory
```
```
:: createWindow
```
```
()^ {
```
```
return
```
```
new
```
```
WindowsWindow;
```
```
} Scroll*
```
```
WindowsFactory
```
```
:: createScroll
```
```
()^ {
```
```
return
```
```
new
```
```
WindowsScroll;
```
```
} ......
```
```
2022/5/7
```

```
2022/5/7
```
## Observer

## （观察者）

##### —— Behavioral

##### Pattern

##### ( 行为型模式

##### )


## Observer Pattern

#### Also called Publish-Subscribe (

#### 发布

**-** 订阅

#### )

#### Pattern or Source-Listener (

#### 源 - 监听器

#### )

#### PatternMany-to-many correspondenceOne subject can be observed by several observers simultaneouslyOne observer can observe many subjects simultaneouslyWhen the subject changes status, all observers will be notified

```
2022/5/7
```

### Example: Newspaper

### Subscription

```
#ifndef PUBLISHER_H_#define
```
```
PUBLISHER_H_
#include
```
```
<list>
#include
```
```
<string>
class
```
```
Subscriber;
class
```
```
Publisher
{ public
```
```
: void Attach
```
```
(Subscriber
```
```
*s)^
```
```
{^ subscribers_.
```
```
push_back
```
```
(s);^
```
```
}
```
```
void
```
```
Detach
```
```
(Subscriber
```
```
*s);
```
```
void
```
```
Notify
```
```
();
virtual
```
```
~ Publisher
```
```
()^ {}
```
```
private
```
```
: std::list<Subscriber
```
```
*>^ subscribers_;
```
```
}; #endif
```
```
2022/5/7
```
##### Publisher.h Demo


```
2022/5/7
```
#include

"Publisher.h"
#include

```
"Subscriber.h"
using
```
```
namespace
```
```
std;
```
```
void
```
```
Publisher
```
```
:: Detach
```
```
(Subscriber
```
```
*s)
```
```
{
```
```
for(list<Subscriber
```
```
*>::iterator
```
```
itr =
```
```
subscribers_.
```
```
begin
```
```
();
```
```
itr !=
```
```
subscribers_.
```
```
end ();
```
```
++^ itr)
```
```
{
```
```
if(*itr ==
```
```
s)
{ subscribers_.
```
```
erase
```
```
(itr);
```
```
break
```
```
;
}
}
} void
```
```
Publisher
```
```
:: Notify
```
```
()^ {
```
```
for(list<Subscriber
```
```
*>::iterator
```
```
itr =
```
```
subscribers_.
```
```
begin
```
```
();
```
```
itr !=
```
```
subscribers_.
```
```
end ();
```
```
++^ itr)
```
```
{
```
```
(*itr)
```
```
‐> Update
```
```
(this
```
```
);
```
```
}
}
```
**Publisher.cpp**


#### Subscriber: when the newspaper is published, the subscriber gets notified

```
2022/5/7
```
```
#ifndef SUBSCRIBER_H_#define
```
```
SUBSCRIBER_H_
#include
```
```
<string>
class
```
```
Publisher;
class
```
```
Subscriber
{ public
```
```
: virtual
```
```
void
```
```
Update
```
```
(Publisher
```
```
*pub)
```
```
=^0 ;
```
```
virtual
```
```
~ Subscriber
```
```
()^ {}
```
```
}; #endif
```
**Subscriber.h**


```
2022/5/7
```
#ifndef NEWSPAPER_H_#define

```
NEWSPAPER_H_
#include
```
```
<string>
#include
```
```
"Publisher.h"
class
```
```
Newspaper:
```
```
public
```
```
Publisher
```
```
{
```
```
public
```
```
: Newspaper
```
```
(std::string
```
```
news):
```
```
Publisher
```
```
{}, news_
```
```
{news}
```
```
{}
```
```
std::string
```
```
getNews
```
```
()^ {^
```
```
return
```
```
news_;
```
```
}
```
```
private
```
```
: std::string
```
```
news_;
```
```
}; #endif
```
**Newspaper.h**


```
2022/5/7
```
#ifndef MAGAZINE_H_#define

```
MAGAZINE_H_
#include
```
```
<string>
#include
```
```
"Publisher.h"
class
```
```
Magazine:
```
```
public
```
```
Publisher
```
```
{
```
```
public
```
```
: Magazine
```
```
(std::string
```
```
art):
```
```
Publisher
```
```
{}, article_
```
```
{art}
```
```
{}
```
```
std::string
```
```
getArticle
```
```
()^ {^
```
```
return
```
```
article_;
```
```
}
```
```
private
```
```
: std::string
```
```
article_;
```
```
}; #endif
```
**Magzine.h**


```
2022/5/7
```
#ifndef READER_H_#define

```
READER_H_
#include
```
```
<string>
#include
```
```
<iostream>
#include
```
```
"Subscriber.h"
#include
```
```
"Newspaper.h"
#include
```
```
"Magazine.h"
class
```
```
Reader:
```
```
public
```
```
Subscriber
```
```
{
```
```
public
```
```
: Reader (
```
```
std::string
```
```
name,
```
```
Newspaper
```
```
*news
```
```
=^ NULL,
```
```
Magazine
```
```
*mag
```
```
=^
```
```
NULL):
```
```
Subscriber
```
```
{},^ name_{
```
```
name},
```
```
news_
```
```
{news},
```
```
mag_
```
```
{mag}
```
```
{}
```
```
void
```
```
Update
```
```
(Publisher
```
```
*pub)
```
```
{
```
```
std::cout <<
```
```
name_
```
```
<<^ "
```
```
is^ notified
```
```
with
```
```
";
```
```
if(pub
```
```
==^ news_)std::cout <<
```
```
news_
```
```
‐> getNews
```
```
()^ <<
```
```
std::endl;
```
```
else^
```
```
if(pub
```
```
==^ mag_)
std::cout <<
```
```
mag_
```
```
‐> getArticle
```
```
()^ <<
```
```
std::endl;
```
```
} private: std::string
```
```
name_;
Newspaper
```
```
*news_;
Magazine
```
```
*mag_;
};#endif
```
**Reader.h**


```
2022/5/7
```
#include

"Newspaper.h"
#include

```
"Reader.h"
int main
```
```
()
{
```
```
Newspaper
```
```
news {
```
```
"Good
news!"
```
```
};
```
```
Magazine
```
```
mag {"Good
```
```
article!“
```
```
};
```
```
Reader
```
```
r1 {"Zhang
```
```
San",
```
```
&news,
```
```
&mag};
```
```
Reader
```
```
r2 {"Li
```
```
Si",^
```
```
&news,
```
```
&mag};
```
```
news. Attach
```
```
(&r1);
```
```
news.
```
```
Attach
```
```
(&r2);
```
```
news. Notify
```
```
();
std::cout <<
```
```
"Detach
```
```
Li^ Si
```
```
from
newspaper"
<<^ std
```
```
::endl;
```
```
news. Detach
```
```
(&r2);
news. Notify
```
```
();
news. Attach
```
```
(&r2);
std::cout <<
```
```
"Attach
```
```
Li^ Si
```
```
again
```
```
to^ newspaper"
```
```
<<^ std
```
```
::endl;
```
```
news. Notify
```
```
();
mag. Attach
```
```
(&r1);
```
```
mag. Attach
```
```
(&r2);
```
```
mag. Notify
```
```
();
std::cout <<
```
```
"Detach
```
```
Zhang
```
```
San^
from^ magazine"
```
```
<<^ std
```
```
::endl;
```
```
mag. Detach
```
```
(&r1);
mag. Notify
```
```
();
return
```
```
0 ;
}
```
```
main.cpp
Zhang San is notified with Good news!Li Si is notified with Good news!Detach Li Si from newspaperZhang San is notified with Good news!Attach Li Si again to newspaperZhang San is notified with Good news!Li Si is notified with Good news!Zhang San is notified with Good article!Li Si is notified with Good article!Detach Zhang San from newspaperLi Si is notified with Good article!
```

### Class Diagram

```
2022/5/7
```
```
Newspaper
```
```
Publisher
Inheritance
```
```
Magazine
```
```
Subscriber Reader
Inheritance
one-to-manyComposition
Aggregation Composition
```

## Class Diagram: Observer

```
2022/5/7
```
##### Behavioral design pattern

```
Aggregation
Composition
```
```
Inheritance
```
```
Inheritance
```

### Using Observer Pattern

##### When subject changes, all observers will be updatedThe number of observers can be dynamically modified (by interfaces Attach and Detach)Subject only needs to notify observers and does not need to know details of observers

```
2022/5/7
```

## Summary

#### What have we learned?Factory MethodAbstract FactoryObserver

```
2022/5/7
```

## Exercise

```
2022/5/7
```
#### Read the book “Design Patterns: Elements of Reusable Objected-Oriented Software”Review what we have learned todayPreview Strategy, Template Method, Proxy, Command, and StatePractice by yourselfCompile and run the “look-and-feel” example using abstract factory design pattern


2022/5/7


