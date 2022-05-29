# Fundamentals of Object-Oriented Programming

## Lecture 12Hailong Yao

## hailongyao@tsinghua.edu.cn

孔子曰：“君子有三戒：少之时，血气未定，戒之在色；及其壮也，血气方刚，戒之在斗；及其老也，血气既衰，戒之在得。”


### Overview

###### Design Pattern

**Strategy (**

策略模式

**)**

**Template Method (**

模板方法

**)**

**Proxy (**

代理

**)**

**Example**

**Simplified Painter with Command (**

命令

**)**

**and State (**

状态

**)**

###### Summary


**Design patterns**

**Factory MethodParameterized Factory MethodAbstract FactoryObserver**

### Last Week


### Factory Method


### Abstract Factory


### Observer


### Strategy

### (

### 策略模式

### )

**—— Behavioral**

**Pattern**

**(**

行为型模式

**)**


### Load Monitor (

### 负载监视器

### )

**Monitor loads of computational grids (**

计算节点

**)**

**Different interfaces on different operating systems (** 操作系统

**)**

```
Win32Win64Linux32Linux64...
```
**How**

**to**

**solve**

**this**

**problem?**


### switch-case ......

```
enum
```
```
MonitorType {Win32,
```
```
Win64,
```
```
Ganglia};
```
```
float
```
```
getLoad
```
```
(MonitorType type)
```
```
{
```
```
switch
```
```
(type)
```
```
{
```
```
case
```
```
Win32:
//get
```
```
system
```
```
load
```
```
via
```
```
Win
```
```
APIs
```
```
return
```
```
load;
```
```
case
```
```
Win64:
//get
```
```
system
```
```
load
```
```
via
```
```
Win
```
```
APIs
```
```
return
```
```
load;
```
```
case
```
```
Ganglia:
//get
```
```
system
```
```
load
```
```
via
```
```
ganglia
```
```
interface
```
```
return
```
```
load;
```
```
}
}
```
**How**

**about**

**this?**


**“**

Open-closed principle violated!

**”**

**Is**

**there**

**a**

**better**

**solution?**

**“**

Dependency Inversion Principle

**”**


### Program to an

### Interface


class

Monitor

{

```
public
```
```
:
```
```
virtual
```
```
float
```
```
getLoad
```
```
()
```
```
=
```
```
0 ;
```
```
}; class
```
```
Win32Monitor
```
```
:^
```
```
public
```
```
Monitor
```
```
{
```
```
public
```
```
:
```
```
float
```
```
getLoad
```
```
()
```
```
{
```
```
//...return
```
```
load;
```
```
}
}; class
```
```
Win64Monitor
```
```
:^
```
```
public
```
```
Monitor
```
```
{
```
```
public
```
```
:
```
```
float
```
```
getLoad
```
```
()
```
```
{
```
```
//...return
```
```
load;
```
```
}
};
```
```
void
```
```
Test
```
```
()
```
```
{
```
```
Monitor
```
```
*
```
```
monitor
```
```
{
```
```
new
```
```
Win32Monitor
```
```
{}
```
```
};
```
```
float
```
```
load
```
```
=
```
```
monitor
```
```
‐
>
getLoad
```
```
();
```
```
cout <<
```
```
load
```
```
<<
```
```
endl;
```
} **Good**

**if**

**we**

**only**

**monitor**

**the**

**load.**

**How**

**to**

**monitor**

**other**

**performance**

**parameters?**


### Monitor Latency (

### 网络时延

### )

**Monitor latency of a given node through network**

**long getLatency(const char *node)**

**Many latency measurement methods**

**Direct latencyProxy latency...**

**Challenging problem**

**For**

**_m_**

**methods of getLoad() and**

**_n_**

**methods of**

**getLatency(), we need**

**_m_**

×

**_n_**

**implementation classes**

```
Win32LoadDirectLatency, Win32LoadProxyLatency, Win64LoadDirectLatency, Win64LoadProxyLatency, ......
```
**Things get worse if we need to getMemory(), getDiskUsage(), etc.**


### Solution

**Separate/decouple**

**getLoad from getLatency**

**In the Context (**

上下文

**) of load/performance**

**monitoringgetLoad is a Strategy (**

策略

**) (interface class)**

**Win32Load and Win64Load are implementation classes**

**getLatency is a Strategy (**

策略

**) (interface class)**

**DirectLatency and ProxyLatency are implementation classes**

## Strategy (

## 策略模式

## )


### Strategy

### （策略模式）

**Strategy Pattern:**

**define a family of algorithms, encapsulate**

**each one, and make them interchangeable (**

可互换

**)**

```
Composition
```
```
Inheritance
```

#ifndef LOADSTRATEGY_H#define

```
LOADSTRATEGY_H
```
```
class
```
```
LoadStrategy
```
```
{
```
```
public
```
```
:
LoadStrategy
```
```
()
```
```
{}
```
```
virtual
```
```
~
LoadStrategy
```
```
()
```
```
{}
```
```
virtual
```
```
float
```
```
getLoad
```
```
()
```
```
=
```
```
0
;
```
```
}; #endif
```
```
// LOADSTRATEGY_H
```
```
LoadStrategy.h
```
Demo


#ifndef WIN32LOADSTRATEGY_H#define

```
WIN32LOADSTRATEGY_H
```
```
#include
```
```
"LoadStrategy.h"
```
```
class
```
```
Win32LoadStrategy
```
```
:
```
```
public
```
```
LoadStrategy {
```
```
public
```
```
:
Win32LoadStrategy
```
```
()
```
```
{}
```
```
virtual
```
```
~
Win32LoadStrategy
```
```
()
```
```
{}
```
```
float
```
```
getLoad
```
```
()
```
```
{
```
```
return
```
```
32
```
```
;
```
```
}
```
```
}; #endif
```
```
//
```
```
WIN32LOADSTRATEGY_H
```
```
Win32LoadStrategy.h
```
```
#ifndef WIN64LOADSTRATEGY_H#define
```
```
WIN64LOADSTRATEGY_H
```
```
#include
```
```
"LoadStrategy.h"
```
```
class
```
```
Win64LoadStrategy
```
```
:
```
```
public
```
```
LoadStrategy
```
```
{
```
```
public
```
```
:
Win64LoadStrategy
```
```
()
```
```
{}
```
```
virtual
```
```
~
Win64LoadStrategy
```
```
()
```
```
{}
```
```
float
```
```
getLoad
```
```
()
```
```
{
```
```
return
```
```
64
```
```
;
```
```
}
```
```
}; #endif
```
```
// WIN64LOADSTRATEGY_H
```
```
Win64LoadStrategy.h
```

#ifndef LATENCYSTRATEGY_H#define

```
LATENCYSTRATEGY_H
```
```
class
```
```
LatencyStrategy
```
```
{
```
```
public
```
```
:
LatencyStrategy
```
```
()
```
```
{}
```
```
virtual
```
```
~
LatencyStrategy
```
```
()
```
```
{}
```
```
virtual
```
```
long
```
```
getLatency
```
```
(
const
```
```
char
```
```
*node)
```
```
=
```
```
0
;
```
```
}; #endif
```
```
//
```
```
LATENCYSTRATEGY_H
```
**LatencyStrategy.h**


#ifndef DIRECTLATENCYSTRATEGY_H#define

```
DIRECTLATENCYSTRATEGY_H
```
```
#include
```
```
"LatencyStrategy.h"
```
```
class
```
```
DirectLatencyStrategy :
```
```
public
```
```
LatencyStrategy
```
```
{
```
```
public
```
```
:
DirectLatencyStrategy
```
```
()
```
```
{}
```
```
~
DirectLatencyStrategy
```
```
()
```
```
{}
```
```
long
```
```
getLatency
```
```
(
const
```
```
char
```
```
*node)
```
```
{
```
```
return
```
```
100
```
```
;
```
```
}
```
```
};#endif
```
```
//
```
```
DIRECTLATENCYSTRATEGY_H
```
```
DirectLatencyStrategy.h
```
```
#ifndef PROXYLATENCYSTRATEGY_H#define
```
```
PROXYLATENCYSTRATEGY_H
```
```
#include
```
```
"LatencyStrategy.h"
```
```
class
```
```
ProxyLatencyStrategy :
```
```
public
```
```
LatencyStrategy
```
```
{
```
```
public
```
```
:
ProxyLatencyStrategy
```
```
()
```
```
{}
```
```
~
ProxyLatencyStrategy
```
```
()
```
```
{}
```
```
long
```
```
getLatency
```
```
(
const
```
```
char
```
```
*node)
```
```
{
```
```
return
```
```
200
```
```
;
```
```
}
```
```
};#endif
```
```
// PROXYLATENCYSTRATEGY_H
```
```
ProxyLatencyStrategy.h
```

**#ifndef MONITOR_H#define**

```
MONITOR_H
```
```
#include
```
```
"LoadStrategy.h"
```
```
#include
```
```
"LatencyStrategy.h"
```
```
class
```
```
Monitor
```
```
{
```
```
public
```
```
:
Monitor(LoadStrategy *load,
```
```
LatencyStrategy*
```
```
latency)
```
```
:m_load{load},
```
```
m_latency{latency}
```
```
{}
```
```
~Monitor()
```
```
{
```
```
if
```
```
(m_load)
```
```
delete
```
```
m_load;
```
```
if
```
```
(m_latency)
```
```
delete
```
```
m_latency;
```
```
} float
```
```
getLoad()
```
```
{
```
```
return
```
```
m_load
```
```
‐>getLoad();
```
```
} long
```
```
getLatency(
```
```
const
```
```
char
```
```
*node)
```
```
{
```
```
return
```
```
m_latency
```
```
‐>getLatency(node);
```
```
} void
```
```
setLoadStrategy(Load
```
```
Strategy *load)
```
```
{
```
```
if
```
```
(m_load)
```
```
delete
```
```
m_load;
```
```
m_load =
```
```
load;
```
```
} void
```
```
setLatencyStrategy(Lat
```
```
encyStrategy *latency)
```
```
{
```
```
if
```
```
(m_latency)
```
```
delete
```
```
m_latency;
```
```
m_latency =
```
```
latency;
```
```
}
```
```
private
```
```
:
LoadStrategy*
```
```
m_load;
```
```
LatencyStrategy*
```
```
m_latency;
```
```
};#endif
```
```
// MONITOR
```
```
_H
```
```
Monitor.h
```

#include

<iostream>

```
#include
```
```
"Monitor.h"
```
```
#include
```
```
"Win32LoadStrategy.h"
```
```
#include
```
```
"Win64LoadStrategy.h"
```
```
#include
```
```
"DirectLatencyStrategy.h"
```
```
#include
```
```
"ProxyLatencyStrategy.h"
```
```
using
```
```
namespace
```
```
std;
```
```
static
```
```
void
```
```
Test
```
```
()
```
```
{
```
```
LoadStrategy*
```
```
load
```
```
{
```
```
new
```
```
Win32LoadStrategy
```
```
{}
```
```
};
```
```
LatencyStrategy*
```
```
latency
```
```
{
```
```
new
```
```
DirectLatencyStrategy
```
```
{}
```
```
};
```
```
Monitor
```
```
*
```
```
monitor
```
```
{
```
```
new
```
```
Monitor
```
```
{load,
```
```
latency}
```
```
};
```
```
float
```
```
loadVal {
```
```
monitor
```
```
 ‐
```
```
>^
```
```
getLoad
```
```
()
```
```
};
```
```
long
```
```
latencyVal {
```
```
monitor
```
```
 ‐
```
```
>^
```
```
getLatency
```
```
("n324"
```
```
)^
```
```
};
```
```
cout <<
```
```
"Load:
```
```
"
```
```
<<
```
```
loadVal <<
```
```
endl;
```
```
cout <<
```
```
"Latency:
```
```
"
```
```
<<
```
```
latencyVal <<
```
```
endl;
```
```
monitor
```
```
‐>
```
```
setLatencyStrategy
```
```
(new
```
```
ProxyLatencyStrategy
```
```
());
```
```
latencyVal =
```
```
monitor
```
```
 ‐
```
```
>^
```
```
getLatency
```
```
("n324"
```
```
);
```
```
cout <<
```
```
"Latency:
```
```
"
```
```
<<
```
```
latencyVal <<
```
```
endl;
```
```
monitor
```
```
‐>
```
```
setLoadStrategy
```
```
(new
```
```
Win64LoadStrategy
```
```
());
```
```
loadVal =
```
```
monitor
```
```
 ‐
```
```
>^
```
```
getLoad
```
```
();
```
```
cout <<
```
```
"Load:
```
```
"
```
```
<<
```
```
loadVal <<
```
```
endl;
```
```
delete
```
```
monitor;
```
```
} int
```
```
main
```
```
()
```
```
{
```
```
Test
```
```
();
```
```
return
```
```
0 ;
```
```
}
```
```
main.cpp
```
**Userchanges strategy**


###### Example of Strategy Pattern

###### Define animals by two strategies: Fly and Swim

**Can fly**



**Bird**

**Can swim**



**Fish**

**Neither fly nor swim**


class

FlyBehavior {

```
public
```
```
:
```
```
virtual
```
```
void
```
```
fly
```
```
()
```
```
=^
```
```
0
;
```
```
}; class
```
```
BirdFly :
```
```
public
```
```
FlyBehavior {
```
```
public
```
```
:
```
```
void
```
```
fly
```
```
()
```
```
{
```
```
cout <<
```
```
"bird
```
```
fly"
```
```
<<
```
```
endl;
```
```
}
}; class
```
```
CannotFly:
```
```
public
```
```
FlyBehavior {
```
```
public
```
```
:
```
```
void
```
```
fly
```
```
()
```
```
{
```
```
cout <<
```
```
"can
```
```
not
```
```
fly"
```
```
<<
```
```
endl;
```
```
}
};
```

class

SwimBehavior {

```
public
```
```
:
```
```
virtual
```
```
void
```
```
swim
```
```
()
```
```
=
```
```
0
;
```
```
}; class
```
```
FishSwim :
```
```
public
```
```
SwimBehavior {
```
```
public
```
```
:
```
```
void
```
```
swim
```
```
()
```
```
{
```
```
cout <<
```
```
"fish
```
```
swim"
```
```
<<
```
```
endl;
```
```
}
}; class
```
```
CannotSwim:
```
```
public
```
```
SwimBehavior {
```
```
public
```
```
:
```
```
void
```
```
swim
```
```
()
```
```
{
```
```
cout <<
```
```
"can
```
```
not
```
```
swim"
```
```
<<
```
```
endl;
```
```
}
};
```

class

Animal

{

```
protected
```
```
:
```
```
FlyBehavior*
```
```
m_fly;
```
```
SwimBehavior*
```
```
m_swim;
```
```
public
```
```
:
```
```
void
```
```
fly
```
```
()
```
```
{
m_fly
```
```
‐
>
fly
```
```
();
```
```
}
```
```
void
```
```
swim
```
```
()
```
```
{^
```
```
m_swim
```
```
‐>
```
```
swim
```
```
();
```
```
}
```
```
}; class
```
```
Fish
```
```
:
```
```
public
```
```
Animal
```
```
{
```
```
public
```
```
:
```
```
Fish
```
```
()
```
```
{
```
```
m_swim=
```
```
new
```
```
FishSwim
```
```
();
```
```
m_fly=
```
```
new
```
```
CannotFly
```
```
();
```
```
}
```
```
}; class
```
```
Bird:
```
```
public
```
```
Animal
```
```
{
```
```
public
```
```
:
```
```
Bird
```
```
()
```
```
{
```
```
m_swim =
```
```
new
```
```
CannotSwim
```
```
();
```
```
m_fly=
```
```
new
```
```
BirdFly
```
```
();
```
```
}
```
```
};
```

int

**main**

()

```
{
```
```
Fish
```
```
fish;
```
```
Bird
```
```
bird;
```
```
fish.
```
```
fly
```
```
();
```
```
fish.
```
```
swim
```
```
();
```
```
bird.
```
```
fly
```
```
();
```
```
bird.
```
```
swim
```
```
();
```
```
return
```
```
0
;
```
```
}
```
**User program**


### Template

### Method

### (

### 模板方法

### )

**—— Behavioral**

**Pattern**

**(**

行为型模式

**)**


**New Requirements in Pizza Store**

**Then, there are drinks in pizza store**

**Hot drinks: coffee, tea, ......**

```
Ok, ok ......
```
**We want drinks!!!**


### How to Make Hot Drinks?

```
class
```
```
Coffee
```
```
{
```
```
public
```
```
:
```
```
void
```
```
sellDrink
```
```
()
```
```
{
```
```
boilWater
```
```
();
```
```
dripCoffee
```
```
();
```
```
pourIntoCup
```
```
();
```
```
addSugerAndMilk
```
```
();
```
```
} void
```
```
boilWater
```
```
()
```
```
{
```
```
cout <<
```
```
"Boiling
```
```
water"
```
```
;
```
```
} void
```
```
dripCoffee
```
```
()
```
```
{
```
```
cout <<
```
```
"Dripping Coffee"
```
```
;
```
```
} void
```
```
pourIntoCup
```
```
()
```
```
{
```
```
cout <<
```
```
"Pouring into cup"
```
```
;
```
```
} void
```
```
addSugerAndMilk
```
```
()
```
```
{
```
```
cout <<
```
```
"Adding Sugar and Milk"
```
```
;
```
```
}
};
```
```
class
```
```
Tea
```
```
{
```
```
public
```
```
:
```
```
void
```
```
sellDrink
```
```
()
```
```
{
```
```
boilWater
```
```
();
```
```
steepTea
```
```
();
```
```
pourIntoCup
```
```
();
```
```
addLemon
```
```
();
```
```
} void
```
```
boilWater
```
```
()
```
```
{
```
```
cout <<
```
```
"Boiling
```
```
water"
```
```
;
```
```
} void
```
```
steepTea
```
```
()
```
```
{
```
```
cout <<
```
```
"Steeping the tea"
```
```
;
```
```
} void
```
```
pourIntoCup
```
```
()
```
```
{
```
```
cout <<
```
```
"Pouring into cup"
```
```
;
```
```
} void
```
```
addLemon
```
```
()
```
```
{
```
```
cout <<
```
```
"Adding Lemon"
```
```
;
```
```
}
};
```

```
class
```
```
HotDrink {
```
```
public
```
```
:
```
```
void
```
```
sellDrink
```
```
()
```
```
{
```
```
boilWater
```
```
();
```
```
brew
```
```
();
```
```
pourIntoCup
```
```
();
```
```
addCondiments
```
```
();
```
```
} void
```
```
boilWater
```
```
()
```
```
{
```
```
cout <<
```
```
"Boiling
```
```
water"
```
```
;
```
```
} virtual
```
```
void
```
```
brew
```
```
()
```
```
=
```
```
0
;
```
```
void
```
```
pourIntoCup
```
```
()
```
```
{
```
```
cout <<
```
```
"Pouring into cup"
```
```
;
```
```
} virtual
```
```
void
```
```
addCondiments
```
```
()
```
```
=
```
```
0
;
```
```
};
```
###### Hot Drinks in Similar Steps

**We have similar ways to make hot drinks**


### Differences between Coffee

### and Tea

```
class
```
```
Coffee
```
```
:
```
```
public
```
```
HotDrink{
```
```
public
```
```
:
```
```
void
```
```
brew
```
```
()
```
```
{
```
```
cout <<
```
```
"Dripping Coffee"
```
```
;
```
```
} void
```
```
addCondiments
```
```
()
```
```
{
```
```
cout <<
```
```
"Adding Sugar and Milk"
```
```
;
```
```
}
};
```
```
class
```
```
Tea
```
```
:
```
```
public
```
```
HotDrink{
```
```
public
```
```
:
```
```
void
```
```
brew
```
```
()
```
```
{
```
```
cout <<
```
```
"Steeping the tea"
```
```
;
```
```
} void
```
```
addCondiments
```
```
()
```
```
{
```
```
cout <<
```
```
"Adding Lemon"
```
```
;
```
```
}
};
```
## Template Method

## （模板方法）


### Template Method (

### 模板方法

### )

**Define skeleton (**

骨架

**) of an algorithm**

**Deferring (**

延迟

**) some steps to subclasses**

**Subclasses redefine certain steps without changing the algorithm’s structure**


### Template Method vs.

### Strategy

**Algorithm skeleton does not changeChange implementation of certain algorithm stepObjective: implement a new algorithm with similar steps**

**Algorithm usage and interface do not changeChange implementation of the algorithmObjective: avoid dramaticincrease in class number via user configuration**

##### Template Method

#### Strategy

**Sometimes, these patterns can be combined together**


###### More Flexible Template Method

**Drink in different cups**

**Typical cup for most drinksSpecial cup for special drinkModify pourIntoCup() in implementation classes**

```
class
```
```
HotDrink {
```
```
public
```
```
:
```
```
void
```
```
sellDrink
```
```
()
```
```
{
```
```
boilWater
```
```
();
```
```
brew
```
```
();
```
```
pourIntoCup
```
```
();
```
```
addCondiments
```
```
();
```
```
} void
```
```
boilWater
```
```
()
```
```
{
```
```
cout <<
```
```
"Boiling
```
```
water"
```
```
;
```
```
} virtual
```
```
void
```
```
brew
```
```
()
```
```
=
 0
```
```
;
```
```
virtual
```
```
void
```
```
pourIntoCup
```
```
()
```
```
=
```
```
0
;
```
```
virtual
```
```
void
```
```
addCondiments
```
```
()
```
```
=
 0
```
```
;
```
```
};
```
Demo


**Default Implementation in Base Class**

```
class
```
```
HotDrink {
```
```
public
```
```
:
```
```
void
```
```
sellDrink
```
```
()
```
```
{
```
```
boilWater
```
```
();
```
```
brew
```
```
();
```
```
pourIntoCup
```
```
();
```
```
addCondiments
```
```
();
```
```
} void
```
```
boilWater
```
```
()
```
```
{
```
```
cout <<
```
```
"Boiling
```
```
water"
```
```
;
```
```
} virtual
```
```
void
```
```
brew
```
```
()
```
```
=
```
```
0
;
```
```
virtual
```
```
void
```
```
pourIntoCup
```
```
()
```
```
{
```
```
cout <<
```
```
"Pouring into typical
```
```
cup"
```
```
;
} virtual
```
```
void
```
```
addCondiments
```
```
()
```
```
=
```
```
0
;
```
```
};
```
```
class
```
```
Tea
```
```
:
```
```
public
```
```
HotDrink{
```
```
public
```
```
:
```
```
void
```
```
brew
```
```
()
```
```
{
```
```
cout <<
```
```
"^
```
```
Steeping the tea"
```
```
<<
```
```
endl;
} void
```
```
addCondiments
```
```
()
```
```
{
```
```
cout <<
```
```
"Adding Lemon"
```
```
<<
```
```
endl;
```
```
} void
```
```
pourIntoCup
```
```
()
```
```
{
```
```
cout <<
```
```
"Pouring into a
```
```
special
```
```
tea
```
```
cup"
```
```
<<
```
```
endl;
```
```
}
};
```
###### Avoid code redundancy


```
Implementation class
```
```
Step i
```
```
Step j
```
```
Step k
```
```
Abstract class
```
```
Algorithm skeleton (virtual interface)
```
### Review of Template Method

**Abstract class defines the algorithm skeletonDetails are given in implementation classesUser program calls the skeleton method**

**The implementation details are called correspondingly**

**When adding a new implementation class, changes are introduced in the algorithm**

```
Step i
```
```
Step j
```
```
Step k
```
```
Algorithm changes
```

**Another Example — Task Scheduler**

**Task (**

作业

**): a program along with data input**

**Task scheduling (**

作业调度

**): based on predefined**

**algorithm, choose one task from the task queue, assign resources (e.g., memory, I/O, etc.), and run it on CPUAlgorithm steps**

**Get current system statusFind a task from the task queue based on a given algorithmAllocate resources for the taskStart to run the task**


### Task Scheduler using Template Method (1)

```
class
```
```
TaskScheduler
```
```
{ public
```
```
:
void
```
```
schedule
```
```
()
```
```
//
```
```
Algorithm
```
```
skeleton
```
```
{
```
```
systemStatus =
```
```
getSystemStatus
```
```
();
```
```
taskToRun =
```
```
findTaskToRun
```
```
(systemStatus);
```
```
if
```
```
(
allocateResources
```
```
(taskToRun))
```
```
startTask
```
```
(taskToRun);
```
```
} virtual
```
```
SystemStatus*
```
```
getSystemStatus
```
```
()
```
```
=^
```
```
0
;
```
```
virtual
```
```
Task*
```
```
findTaskToRun
```
```
(SystemStatus*
```
```
systemStatus)
```
```
=
 0
```
```
;
```
```
virtual
```
```
BOOL
```
```
allocateResources
```
```
(Task*
```
```
taskToRun)
```
```
=^
```
```
0
;
```
```
virtual
```
```
void
```
```
startTask
```
```
(Task*
```
```
taskToRun)
```
```
=^
```
```
0
;
```
```
};
```

### Task Scheduler using Template Method (2)

```
class
```
```
MyTaskScheduler :
```
```
public
```
```
TaskScheduler {
```
```
public
```
```
:
SystemStatus*
```
```
getSystemStatus
```
```
()
```
```
{
```
```
SystemStatus *status
```
```
{
new
```
```
SystemStatus
```
```
{}
```
```
};
```
```
//get
```
```
current
```
```
status
```
```
of
```
```
system
```
```
return
```
```
status;
```
```
} Task*
```
```
findTaskToRun
```
```
(SystemStatus*
```
```
systemStatus)
```
```
{
```
```
//find
```
```
a
task
```
```
by
```
```
a^
```
```
schedule
```
```
algorithm
```
```
return
```
```
task;
```
```
} BOOL
```
```
allocateResources
```
```
(Task*
```
```
taskToRun)
```
```
{
```
```
//allocate
```
```
resources
```
```
such
```
```
as
```
```
memory,
```
```
process...
```
```
return
```
```
TRUE;
```
```
} void
```
```
startTask
```
```
(Task*
```
```
taskToRun)
```
```
{
```
```
//start
```
```
the
```
```
task
```
```
}
```
```
};
```

### Task Scheduler using Template Method (3)

```
void
```
```
schedule
```
```
()
```
```
{
```
```
TaskScheduler*
```
```
scheduler
```
```
{
```
```
new
```
```
MyTaskScheduler
```
```
{}
```
```
};
```
```
scheduler
```
```
 ‐
```
```
>
```
```
schedule
```
```
();
```
```
}
```
**What if there are many different implementations for each step?**


### Combine Template

### Method and Strategy (1)

**Use**

**Template Method**

**to define algorithm skeleton**

**Use**

**Strategy**

**to choose implementation of each algorithm step**

```
class
```
```
SystemStatusStrategy {
```
```
public
```
```
:
virtual
```
```
SystemStatus*
```
```
getSystemStatus
```
```
()
```
```
=^
```
```
0
;
```
```
};class
```
```
TaskFinderStrategy {
```
```
public
```
```
:
virtual
```
```
Task*
```
```
findTaskToRun
```
```
(SystemStatus*
```
```
systemStatus)
```
```
=
 0
```
```
;
```
```
};class
```
```
ResourceAllocator {
```
```
public
```
```
:
virtual
```
```
BOOL
```
```
allocateResources
```
```
(Task*
```
```
taskToRun)
```
```
=^
```
```
0
;
```
```
};class
```
```
TaskRunner {
```
```
public
```
```
:
virtual
```
```
void
```
```
startTask
```
```
(Task*
```
```
taskToRun)
```
```
=^
```
```
0
;
```
```
};
```
**Abstract class for algorithm steps**


### Combine Template

### Method and Strategy (2)

```
class
```
```
MySystemStatusStrategy :
```
```
public
```
```
SystemStatusStrategy {
```
```
public
```
```
:
SystemStatus*
```
```
getSystemStatus
```
```
()
```
```
{
```
```
//
```
```
...
}
```
```
};class
```
```
FIFOTaskFinderStrategy :
```
```
public
```
```
TaskFinderStrategy {
```
```
public
```
```
:
Task*
```
```
findTaskToRun
```
```
(SystemStatus*
```
```
systemStatus)
```
```
{
```
```
//
```
```
...
```
```
}
```
```
};class
```
```
SimpleResourceAllocator :
```
```
public
```
```
ResourceAllocator {
```
```
public
```
```
:
BOOL
```
```
allocateResources
```
```
(Task*
```
```
taskToRun)
```
```
{
```
```
//
```
```
...
}
```
```
};class
```
```
MyTaskRunner :
```
```
public
```
```
TaskRunner {
```
```
public
```
```
:
void
```
```
startTask
```
```
(Task*
```
```
taskToRun)
```
```
{
```
```
//
```
```
...
}
```
```
};
```
**Implemetation**

**classes**


### Combine Template

### Method and Strategy (3)

```
class
```
```
TaskScheduler {
```
```
public
```
```
:
TaskScheduler
```
```
(SystemStatusStrategy *s
```
```
ystemStatusStrategy,
```
```
TaskFinderStrategy*
```
```
taskFinder,
```
```
ResourceAllocator*
```
```
resourceAllocator,
```
```
TaskRunner*
```
```
taskRunner)
```
```
:
```
```
systemStatusStrategy
```
```
{systemStatusStrategy},
```
```
taskFinder
```
```
{
```
```
taskFinder},
```
```
resourceAllocator
```
```
{resourceAllocator},
```
```
taskRunner
```
```
{taskRunner}
```
```
{}
```
```
void
```
```
schedule
```
```
()
```
```
{
```
```
systemStatus =
```
```
systemStatusStrategy
```
```
‐>
```
```
getSystemStatus
```
```
();
```
```
taskToRun =
```
```
taskFinder
```
```
‐>
```
```
findTaskToRun
```
```
(systemStatus);
```
```
if
```
```
(resourceAllocator
```
```
‐>
```
```
allocateResources
```
```
(taskToRun))
```
```
taskRunner
```
```
‐>
```
```
startTask
```
```
(taskToRun);
```
```
}
```
```
private
```
```
:
SystemStatusStrategy *sy
```
```
stemStatusStrategy;
```
```
TaskFinderStrategy*
```
```
taskFinder;
```
```
ResourceAllocator*
```
```
resourceAllocator;
```
```
TaskRunner*
```
```
taskRunner
```
```
};
```
**Template method**

**Strategy**

```
Set strategy
```

### Class Diagram

```
Inheritance
```
```
Inheritance
```
```
Aggregation/composition
```
```
Aggregation/composition
```

### Template Method and OOP

### Principle

-

```
Always refer to the skeleton
```
```
method in abstract class
```
```
Dependency Inversion Principle •
```
```
Open: change algorithm details by adding new implementation classes
```
-

```
Closed: no need to modify existing classes/codes
The open-closed principle •
```
```
Algorithm skeleton (no chan
```
```
ge) remains the same in
```
```
abstract class; each algorithm step (change) is deferred to implementation classes
Partition different tasks and assign them to different objects
```

### Proxy

### （代理

### /

### 委托）

**—— Structural**

**Pattern**

**(**

结构型模式

**)**


### Show-Image Program

### Through Internet

```
class
```
```
Image{
```
```
public
```
```
:
void
```
```
show
```
```
()
```
```
{
```
```
download
```
```
();
```
```
//......
```
```
}
```
```
private
```
```
:
void
```
```
download
```
```
()
```
```
{
```
```
//......
```
```
}
```
```
};
```
```
int
```
```
main
```
```
()
```
```
{
```
```
Image
```
```
*
```
```
image
```
```
{
```
```
new
```
```
Image
```
```
{}
```
```
};
```
```
image
```
```
 ‐
```
```
>
```
```
show
```
```
();
```
```
return
```
```
0
;
```
```
}
```
**Internet is very slow sometimes. How to improve user experience (**

用户体验

**)?**


### One Solution

```
class
```
```
Image{
```
```
public
```
```
:
void
```
```
show
```
```
()
```
```
{
```
```
download
```
```
();
```
```
//......
```
```
}
```
```
private
```
```
:
void
```
```
download
```
```
()
```
```
{
```
```
//......
```
```
}
```
```
};
```
```
int
```
```
main
```
```
()
```
```
{
```
```
Image
```
```
*
```
```
image
```
```
{
```
```
new
```
```
Image
```
```
{}
```
```
};
```
```
cout <<
```
```
"please
```
```
wait..."
```
```
;
```
```
image
```
```
 ‐
```
```
>
```
```
show
```
```
();
```
```
return
```
```
0
;
```
```
}
```
**What if “image->show()” is called atdifferent places?**


### Another Solution

```
class
```
```
Image
```
```
{
```
```
public
```
```
:
void
```
```
show
```
```
()
```
```
{
```
```
cout <<
```
```
"please
```
```
wait..."
```
```
;
```
```
download
```
```
();
```
```
//......
```
```
}
```
```
private
```
```
:
void
```
```
download
```
```
()
```
```
{
```
```
//......
```
```
}
```
```
};
```
```
int
```
```
main
```
```
()
```
```
{
```
```
Image
```
```
*
```
```
image
```
```
{
```
```
new
```
```
Image
```
```
{}
```
```
};
```
```
image
```
```
 ‐
```
```
>
show
```
```
();
```
```
return
```
```
0
;
```
```
}
```
**How about this?**

**How to perform different tasks instead ofthe prompt for different calls to “show()”?**


### Using Proxy

```
class
```
```
Image
```
```
:
```
```
public
```
```
Graph
```
```
{
```
```
public
```
```
:
void
```
```
show
```
```
()
```
```
{
```
```
download
```
```
();
```
```
//......
```
```
}
```
```
private
```
```
:
void
```
```
download
```
```
()
```
```
{
```
```
//......
```
```
}
```
```
};
```
```
int
```
```
main
```
```
()
```
```
{
```
```
Graph
```
```
*
```
```
graph
```
```
{
```
```
new
```
```
ImageProxy
```
```
{
new
```
```
Image
```
```
{}}};
```
```
graph
```
```
 ‐
```
```
>
```
```
show
```
```
();
```
```
return
```
```
0
;
```
```
class }
```
```
ImageProxy :
```
```
public
```
```
Graph
```
```
{
```
```
public
```
```
:
void
```
```
show
```
```
()
```
```
{
```
```
cout <<
```
```
"please
```
```
wait..."
```
```
;
```
```
image
```
```
 ‐
```
```
>
```
```
show
```
```
();}
```
```
private
```
```
:
Image
```
```
*
```
```
image;
```
```
};
```
```
class
```
```
Graph
```
```
{
```
```
public
```
```
:
virtual
```
```
void
```
```
show
```
```
()
```
```
=
```
```
0 ;
```
```
};
```
## Proxy

## （代理）


### Proxy

**Provide a surrogate (**

代理

**) or placeholder for**

**another object to**

**control access**

**to it (**

控制器访问

**)**

**Before and after accessing the object, different tasks can be added for different purposes**



**very**

**flexible pattern**

```
RealSubject
+ request(): void
```
```
Subject
```
```
+ request(): void
```
```
Inheritance
```
```
Proxy
```
```
+ request(): void
```
```
Client
```
```
Reference/pointer
```
```
Composition
```
```
realSubject.request();
```

**Remote Proxy (**

远程代理

**): provides a local**

**representative for an object in a different address spaceControl access to a remote objectDifferent address space**

**Between different processes (**

进程

**) on the same machine**

**Between different machines through internet**

**Remote proxy are used when**

###### Application 1 — Remote ProxyEncoding a request and its argumentsSending the encoded request to the real subject in a different address space


**Control access to an expensive object (in terms of memory or runtime)Only creates expensive objects (consumes large memory and/or processing time)**

**on demand**

**Objective: delay creation of expensive objects to save memory and runtime**

###### Application 2 — Virtual Proxy


**Protect (or Access) Proxy**

**Control access to an object based on access rightsProtection proxy is useful when objects should have different access rights**

**Application 3 — Protection Proxy**

```
void
```
```
Proxy
```
```
::
```
```
request
```
```
(
```
```
)
```
```
{
```
```
if
```
```
(
userAuthorize
```
```
(^
```
```
))
```
```
{
```
```
realSubject
```
```
‐
>
```
```
request
```
```
(
```
```
);
```
```
}
}
```

**A**

**smart reference**

**is a replacement for a bare**

**pointer (**

替换普通指针

**) that performs additional**

**actions when an object is accessedTypical usage**

**Reference counting (**

引用计数

**): count the number of**

**references to an object, so that it can be freed automatically when there are no more references**

**BTW, you are suggested to learn by yourselves unique_ptr, shared_ptr, and weak_ptr.**

**Application 4 — Smart Reference**


### Proxy vs. Adapter

**Similarity**

**Provide access between two objects**

**Difference**

**Proxy wraps one object to control it’s access; Adapter wraps one or more objects to adapt their interface to the user programProxy does not change interface; Adapter may change interfaceProxy often changes functionality; Adapterdoes not change functionality**


### Example: Simple Painter

### (

### 简单绘图工具

### )

### Command

### (

### 命令

### )

### State

### (

### 状态

### )

**—— Behavioral**

**Pattern**

**(**

行为型模式

**)**


### Simplified Painter

**Design a simple Painter tool: according to given commands, draw pictures with line segmentsThe commands are as follows**

**Move forward/backward by**

**_M_**

**pixels (**

像素

**)**

**Rotate left/right by**

**_N_**

**degrees**

**Pen up / pen down (**

抬笔

**/**

落笔

**)**


### Objective

**Example: draw a square of 100x100 by the following commands**

**Initial position: [200,200], heading direction: UPForward 100Right 90Forward 100Right 90Forward 100Right 90Forward 100**


### Design

###### We need the following classes

**Class**

**Canvas**

**: to store and display the**

**drawn picture, and provide drawing interface Line(x1, y1, x2, y2)Class**

**Command**

**for drawing commands**

**Class**

**Context (**

上下文

**)**

**: to store current**

**drawing status**


### Canvas

```
class
```
```
Canvas
```
```
{
```
```
public
```
```
:
Canvas
```
```
(
```
```
);
```
```
//create
```
```
a^
```
```
blank
```
```
canvas
```
```
void
```
```
show
```
```
(
```
```
);
```
```
//show
```
```
the
```
```
drawn
```
```
picture
```
```
void
```
```
Line
```
```
(x1,
```
```
y1,
```
```
x2,
```
```
y2);
```
```
//draw
```
```
a
```
```
line
```
```
on
```
```
the
```
```
canvas
```
```
};
```

### Command

**Class CommandCommand is an**

**interface class**

**(**

接口类

**):**

**different concrete commands correspond to different implementation classes (**

实现类

**)**

```
class
```
```
Command
```
```
{
```
```
public
```
```
:
virtual
```
```
void
```
```
execute
```
```
(
)
```
```
=
```
```
0
;
```
```
}; class
```
```
MoveCommand :
```
```
Command
```
```
{
```
```
public
```
```
:
MoveCommand
```
```
(
int
```
```
step,
```
```
Canvas&
```
```
canvas,
```
```
Context&
```
```
context);
```
```
void
```
```
execute
```
```
(^
```
```
);
```
```
};
```

###### Implementation Classes of

###### Command

**Total 6 commands combined into 3 classes:**

**MoveCommand: forward/backward**

```
Parameter
```
```
step
```
```
: denote different directions
```
```
Negative for backward and positive for forward
```
**RotateCommand: left/right**

```
Parameter
```
```
angle
```
```
: denote different directions
```
```
Negative for left and positive for right
```
**PenCommand: up/down**

```
Parameter
```
```
isDown
```
```
: denote different cases
```
```
0/1: 0 for pen up, 1 for pen down
```
**Parameters are introduced to reduce the number of classes**

**Similar to**

**Parameterized Factory Method**


### Context

```
Context class: store current status (current position, current direction, pen up or down)
class
```
```
Context
```
```
{
```
```
public
```
```
:
Context
```
```
(
)
```
```
:
```
```
x
{
200
```
```
},
```
```
y
{
200
```
```
},
```
```
heading
```
```
{
0
},
```
```
penDown
```
```
{
1
}
{
```
```
}
```
```
bool
```
```
isPenDown
```
```
(
```
```
)
{
```
```
return
```
```
penDown;}
```
```
void
```
```
setPenDown
```
```
(
bool
```
```
down)
```
```
{
```
```
penDown =
```
```
down;}
```
```
int
```
```
getX
```
```
(^
```
```
)
```
```
{
```
```
return
```
```
x;
```
```
}
```
```
int
```
```
getY
```
```
(^
```
```
)
```
```
{
```
```
return
```
```
y;
```
```
}
```
```
void
```
```
setPos
```
```
(
int
```
```
xx,
```
```
int
```
```
yy)
```
```
{
```
```
x
```
```
=
xx;
```
```
y
```
```
=
```
```
yy;
```
```
}
```
```
int
```
```
getHeading
```
```
(
```
```
)
{
```
```
return
```
```
heading;
```
```
}
```
```
void
```
```
setHeading
```
```
(
int
```
```
head)
```
```
{
```
```
heading
```
```
=
```
```
head;
```
```
}
```
```
//use
```
```
int
```
```
for
```
```
the
```
```
four
```
```
directions:
```
```
U‐
```
```
0/D
```
```
‐
1/L
```
```
‐
2/R
```
```
‐
3
```
```
private
```
```
:
int
```
```
x,
```
```
y,
```
```
heading;
```
```
bool
```
```
penDown;
```
```
};
```

### Command Creation (1)

**Interface class UI for creating Commands**

**Read user input and interpret (**

解释

**) it into a**

```
Command object
class
```
```
UI
```
```
{
```
```
public
```
```
:
virtual
```
```
Command*
```
```
getCommand
```
```
(
```
```
)
```
```
=
```
```
0
;
```
```
};
```

### Command Creation (2)

###### Read in commands from configuration file or command line

```
class
```
```
StreamUI :
```
```
public
```
```
UI
```
```
{
```
```
public
```
```
:
StreamUI
```
```
(istream *in,
```
```
Canvas&
```
```
ca,
```
```
Context&
```
```
co)
```
```
:^
```
```
input
```
```
{in},
```
```
canvas
```
```
{ca},
```
```
context
```
```
{co}
```
```
{
```
```
}
```
```
Command*
```
```
getCommand
```
```
();
```
```
private
```
```
:
istream*
```
```
input;
```
```
Canvas&
```
```
canvas;
```
```
Context&
```
```
context;
```
```
};
```

### Interpret Commands

**Using string comparison for determining different commands**

```
Command*
```
```
StreamUI
```
```
::
```
```
getCommand
```
```
(
```
```
)
```
```
{
```
```
string
```
```
cmd;
```
```
*input
```
```
>>
```
```
cmd;
```
```
if
```
```
(cmd ==
```
```
"forward"
```
```
)
```
```
{
```
```
int
```
```
step;
```
```
*input
```
```
>>
```
```
step;
```
```
Command
```
```
*
forward
```
```
=
new
```
```
MoveCommand{step,c
```
```
anvas,context};
```
```
return
```
```
forward;
```
```
}
```
```
else
```
```
if
```
```
(cmd ==
```
```
"penup"
```
```
)
```
```
{
```
```
Command
```
```
*
penup =
```
```
new
```
```
PenCommand{
```
```
0
,canvas,context};
```
```
return
```
```
penup;
```

}

else

if

(cmd ==

"pendown"

)

{

```
Command
```
```
*
pendown =
```
```
new
```
```
PenCommand{
```
```
1
,canvas,context};
```
```
return
```
```
pendown;
```
```
}
```
```
else
```
```
if
```
```
(cmd ==
```
```
"back"
```
```
)
```
```
{
```
```
int
```
```
step;
```
```
input
```
```
>>
```
```
step;
```
```
Command
```
```
*
back
```
```
=
```
```
new
```
```
MoveCommand{
```
```
‐
step,canvas,context};
```
```
return
```
```
back;
```
```
}
```
```
else
```
```
......
```
```
}
```

### Implementation Classes

### of Command

```
class
```
```
MoveCommand :
```
```
public
```
```
Command
```
```
{
```
```
public
```
```
:
MoveCommand
```
```
(
int
```
```
st,
```
```
Canvas&
```
```
ca,
```
```
Context&
```
```
co)
```
```
:
```
```
step
```
```
{st},
```
```
canvas
```
```
{ca},
```
```
context
```
```
{co}
```
```
{
```
```
}
```
```
void
```
```
execute
```
```
(
```
```
);
```
```
//implement
```
```
it
```
```
here...
```
```
private
```
```
:
int
```
```
step;
```
```
Canvas&
```
```
canvas;
```
```
Context&
```
```
context;
```
```
};class
```
```
PenCommand :
```
```
public
```
```
Command
```
```
{
```
```
public
```
```
:
PenCommand
```
```
(
bool
```
```
down,
```
```
Context&
```
```
co):
```
```
isDown
```
```
{down},
```
```
context
```
```
{co}
```
```
{}
```
```
void
```
```
execute
```
```
(
```
```
);
```
```
//implement
```
```
it
```
```
here...
```
```
private
```
```
:
bool
```
```
isDown;
```
```
Context&
```
```
context;
```
```
};
```
Demo


### Executing a Command

```
void
```
```
MoveCommand
```
```
::
```
```
execute
```
```
(
```
```
)
```
```
{
```
```
int
```
```
x1
```
```
=^
```
```
context.
```
```
getX
```
```
();
```
```
int
```
```
y1
```
```
=^
```
```
context.
```
```
getY
```
```
();
```
```
int
```
```
heading
```
```
=
```
```
context.
```
```
getHeading
```
```
();
```
```
int
```
```
x2,
```
```
y2;
```
```
//Compute
```
```
end
```
```
point
```
```
(x2,
```
```
y2)
```
```
by
```
```
start
```
```
point
```
```
(x1,
```
```
y1),
```
```
heading
```
```
and
```
```
step
```
```
here
```
```
......
```
```
if
```
```
(context.
```
```
isPenDown
```
```
())
```
```
{
```
```
canvas.
```
```
Line
```
```
(x1,
```
```
y1,
```
```
x2,
```
```
y2);
```
```
} context.
```
```
setPos
```
```
(x2,
```
```
y2);
```
```
} void
```
```
PenCommand
```
```
::
```
```
execute
```
```
(
```
```
)
```
```
{
```
```
context.
```
```
setPenDown
```
```
(isDown);
```
```
}
```

### User Program

```
int
```
```
main
```
```
(int
```
```
argc,
```
```
char
```
```
*
```
```
argv[])
```
```
{
```
```
istream *in;if
```
```
(argc >
```
```
1
)
{
```
```
ifstream *
```
```
fs
```
```
=
```
```
new
```
```
ifstream{argv[
```
```
1
]};
```
```
in
```
```
=
```
```
fs;
```
```
}
```
```
else
```
```
in
```
```
=
```
```
&cin;
```
```
//
```
```
Determine
```
```
inputs
```
```
by
```
```
command
```
```
‐
line
```
```
arguments
```
```
Canvas
```
```
canvas;
```
```
Context
```
```
context;
```
```
UI*
```
```
ui =
```
```
new
```
```
StreamUI
```
```
{in,
```
```
canvas,
```
```
context};
```
```
while
```
```
(!in.
```
```
eof
```
```
())
```
```
{
```
```
Command*
```
```
command
```
```
=
ui
```
```
‐
>
```
```
getCommand
```
```
();
```
```
if
```
```
(!command)
```
```
break;
```
```
command.
```
```
execute
```
```
();
```
```
canvas.
```
```
show
```
```
();
```
```
}
```
```
//Loop:
```
```
Read
```
```
a
```
```
command
```
```

```
```
execute
```
```
the
```
```
command
```
```

```
```
show
```
```
delete
```
```
ui;
```
```
return
```
```
0
;
```
```
}
```

### Command Pattern

**Also called Action (**

行动

**) Pattern or Transaction (**

交易

**) Pattern**

**Command Pattern**

**Encapsulates a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations (**

支持撤消操作

**)**

**Using Command Pattern, we encapsulate**

**method**

**invocation (**

方法调用

**), so that the invoker (**

调用者

**) does not**

**need to know implementation details**

**Single Responsibility Principle**

**The tasks of making request and executing command are separated/**

**decoupled (**

解耦

**)**

**to different objects**

**The object for making request does not need to know details of how command is executed**


### Class Diagram of Command

### Pattern

```
Command (
```
```
命令
```
```
): declares an interface for executing an operation
```
```
ConcreteCommand (
```
```
具体命令
```
```
)
```
```
Defines a binding between a
```
```
Receiver and an action
```
```
Implements Execute() by invoking (
```
```
调用
```
```
) the corresponding operation on Receiver
```
```
Receiver (
```
```
接收者
```
```
): responsible for performing operation associated with request
```
```
—Canvas & ContextClient (
```
```
客户
```
```
): creates a ConcreteCommand object and sets its receiver (
```
```
接收者
```
```
)
```
```
—UIInvoker (
```
```
请求者
```
```
): asks command to carry out (
```
```
执行
```
```
) the request by execute()
```
```
Receiver+ Action() —main
```
```
Command+ Execute()
```
```
Inheritance
```
```
ConcreteCommand
```
```
+ Execute()
```
```
Invoker
```
```
Reference/pointer
```
```
Composition
```
```
receiver.Action();
```
```
Client
```
```
Creates
```
```
Composition
```

### Command Pattern

**Decouples (**

解耦

**) between the object making**

**request (**

**Invoker**

**) and the object that knows how**

**to perform it (**

**Receiver**

**)**

**A**

**concrete command object**

**is responsible for a**

**decoupled task, which**

**encapsulates a receiver**

**with an action or set of actionsInvokers are parameterized with Commands**


### Undo & Redo in Painter

**Command Pattern is suitable for realizing Undo**

**and**

**Redo**

**Method**

**Store the Commands sequentially (**

顺序地

**) in a**

**list. When showing the picture, execute all the Commands once againUndo:**

**_skip the last command_**

**in the list, and**

**execute the remaining commands.Redo:**

**_execute the latest command once again_**

**,**

**and add it to the end of command list.**


###### Re-construct (

###### 重构

###### ) Painter

**Store the Commands in Context and introduce a show() function**

```
class
```
```
Context
```
```
{
```
```
public
```
```
:
Context
```
```
()
```
```
:
```
```
lastCommand
```
```
{^0
```
```
},
```
```
maxCommand
```
```
{
0
},
```
```
/*......*/
```
```
{
```
```
commandList =
```
```
new
```
```
Command[
```
```
256
```
```
];
```
```
//to
```
```
store
```
```
commands...
```
```
} //......void
```
```
addCommand
```
```
(Command
```
```
&command);
```
```
void
```
```
undo
```
```
();
```
```
void
```
```
redo
```
```
();
```
```
void
```
```
show
```
```
();
```
```
private
```
```
:
int
```
```
x,
```
```
y,
```
```
heading,
```
```
penDown;
```
```
Command*
```
```
commandList;
```
```
int
```
```
lastCommand,
```
```
maxCommand;
```
```
};
```

### Execution of the CommandsNOTE: buffer overflow and “=” operator overloading are omitted here

```
void
```
```
Context
```
```
::
```
```
addCommand
```
```
(Command
```
```
&command)
```
```
{
```
```
commandList[lastCommand ++]
```
```
=
```
```
command;
```
```
maxCommand =
```
```
lastCommand;
```
```
} void
```
```
Context
```
```
::
```
```
undo
```
```
()
```
```
{
```
```
if
```
```
(lastCommand >
```
```
 0
```
```
)
```
```
lastCommand
```
```
‐‐
```
```
;
```
```
} void
```
```
Context
```
```
::
```
```
redo
```
```
()
```
```
{^
```
```
//Need
```
```
further
```
```
improvement
```
```
for
```
```
multiple
```
```
times
```
```
of
```
```
undo
```
```
and
```
```
redo
```
```
if
```
```
(lastCommand <
```
```
maxCommand)
```
```
lastCommand ++;
```
```
}
```

### Modify Command

```
Remove Canvas and Context members, and pass them as function arguments
class
```
```
Command
```
```
{
```
```
public
```
```
:
virtual
```
```
void
```
```
execute
```
```
(Canvas&
```
```
canvas)
```
```
=
```
```
0
;
```
```
}; class
```
```
MoveCommand :
```
```
Command
```
```
{
```
```
public
```
```
:
MoveCommand
```
```
(
int
```
```
step,
```
```
Context&
```
```
context);
```
```
void
```
```
execute
```
```
(Canvas&
```
```
canvas);
```
```
//the
```
```
same
```
```
implementation...
```
```
};
```

### show()

**Show(): execute all the commandsUsing lastCommand, we can Undo commandsThis method for “Undo” takes more runtime**

**In real applications, there could be better ways depending on the interface of the canvas**

void

Context

::

**show**

()

{

Canvas

canvas;

//start

by

a

new

blank

canvas

for

(

int

i=

0

;

i<

lastCommand;

i++)

{

commandList[i]

 ‐

>

**execute**

(canvas);

} canvas.

**show**

();

}


### User Program

**Correspondingly, StreamUI needs to identify Undo and Redo Commands**

**Implementation is omitted**

```
int
```
```
main
```
```
(int
```
```
argc,
```
```
char
```
```
*
```
```
argv[])
```
```
{
```
```
//the
```
```
same
```
```
as
```
```
before
```
```
......
```
```
UI*
```
```
ui {
```
```
new
```
```
StreamUI
```
```
{in,
```
```
canvas,
```
```
context}};
```
```
while
```
```
(!in.
```
```
eof
```
```
())
```
```
{
```
```
Command&
```
```
command
```
```
{^
```
```
ui
```
```
‐
>
```
```
getCommand
```
```
()};
```
```
context.
```
```
addCommand
```
```
(command);
```
```
context.
```
```
show
```
```
();
```
```
} delete
```
```
ui;
```
```
return
```
```
0
;
```
```
}
```

### Alternative Solution: State

### Pattern

**In our system, a pen has two states:**

**pen**

**up / pen down**

**Under different states, commands have different results“if ... else ...” is used to check the states**

**Alternative solution: State (**

状态

**) Pattern**

```
Have different inter-changeable internal states
```
```
Class
Strategy!
```
```
Class
diagram is
```
```
same as
Strategy!
```
```
Inheritance
```
```
Composition
```

### An Example Using State

### Pattern

**Traffic lights: red**



**green**



**yellow**



**red**



**...**

**Implementation without State Pattern**

```
class
```
```
Light
```
```
{
```
```
public
```
```
:
Light
```
```
(
```
```
)^
```
```
:
```
```
color
```
```
{
"red"
```
```
}
```
```
{^
```
```
}
```
```
void
```
```
next
```
```
(
```
```
)
```
```
{
```
```
if
```
```
(color
```
```
==
```
```
"red"
```
```
)
```
```
color
```
```
=
"green"
```
```
;
```
```
else
```
```
if
```
```
(color
```
```
==
```
```
"green"
```
```
)
```
```
color
```
```
=
"yellow"
```
```
;
```
```
elsecolor
```
```
=
```
```
"red"
```
```
;
```
```
} string
```
```
getColor
```
```
(^
```
```
)
```
```
{
```
```
return
```
```
color;
```
```
}
```
```
private
```
```
:
string
```
```
color;
```
```
};
```

### Traffic Lights Using State

### Pattern (1)

###### State classes

```
class
```
```
State
```
```
{
```
```
public
```
```
:
State
```
```
(Light*
```
```
l)
```
```
:
```
```
light
```
```
{l};
```
```
virtual
```
```
void
```
```
next
```
```
(
```
```
)
```
```
=^
```
```
0
;
```
```
virtual
```
```
string
```
```
getColor
```
```
(
```
```
);
```
```
protected
```
```
:
```
```
Light
```
```
*light;
```
```
};class
```
```
RedState
```
```
:
```
```
public
```
```
State
```
```
{
```
```
void
```
```
next
```
```
(
```
```
)
{
```
```
light
```
```
 ‐
```
```
>
```
```
setState
```
```
(
new
```
```
GreenState
```
```
{});
```
```
}
```
```
string
```
```
getColor
```
```
(
```
```
)
```
```
{
```
```
return
```
```
"red"
```
```
;
```
```
}
```
```
};class
```
```
GreenState :
```
```
public
```
```
State
```
```
{
```
```
void
```
```
next
```
```
(
```
```
)
{
```
```
light
```
```
 ‐
```
```
>
```
```
setState
```
```
(
new
```
```
YellowState
```
```
{});
```
```
}
```
```
string
```
```
getColor
```
```
(
```
```
)
```
```
{
```
```
return
```
```
"green"
```
```
;
```
```
}
```
```
};
```

### Traffic Lights Using State

### Pattern (2)

###### Light class

```
class
```
```
Light
```
```
{
```
```
public
```
```
:
Light
```
```
(
)
```
```
{
```
```
state
```
```
=
```
```
new
```
```
RedState
```
```
{
this
```
```
};
```
```
}
```
```
~
Light
```
```
(^
```
```
)
```
```
{
```
```
delete
```
```
state;
```
```
}
```
```
void
```
```
next
```
```
(
```
```
)
```
```
{
```
```
State*
```
```
old
```
```
{state};
```
```
old
```
```
 ‐
```
```
>
```
```
next
```
```
();
```
```
delete
```
```
old;
```
```
} void
```
```
setState
```
```
(State
```
```
*s)
```
```
{
```
```
state
```
```
=^
```
```
s;
```
```
}
```
```
string
```
```
getColor
```
```
(^
```
```
)
```
```
{
```
```
return
```
```
state
```
```
 ‐
```
```
>
```
```
getColor
```
```
();
```
```
}
```
```
private
```
```
:
State*
```
```
state;
```
```
};
```

### State Pattern

**State Pattern: allow an object to alter its behavior when its internal state changes. The object will appear to change its class.**

**By referencing different State objects, it seems each object is instantiated from a different class**

**State transitions (**

状态改变

**) can be controlled**

**either by State or ContextAlthough State and Strategy have the same class diagram, their intents (**

设计意图

**) are different**

**State: context’s behavior changes due to changes of its internal states. The client knows little about the state objectsStrategy: the client sets the strategy object of the context**


###### Scenario for Using State Pattern

**State Pattern is suitable when there are complicated transformation between different states**

**Classical TcpConnection**

```
Tcp states include Established, Listening and Closed. The three states transform between each other frequently.
```
**Switch between different tools in the toolbox**

```
For example, in drawing programs, the user may switch between different drawing tools for drawing rectangle, line, curve, etc.
```
**For implementation of finite automata (**

有限自动机

**),**

**where there are different states and transfer functions**


## DESIGN PATTERNS


### Summary of Design

### Patterns

**SOLID OOP principles**

**Single Responsibility Principle (SRP)Open-Closed Principle (OCP)Liskov Substitution Principle (LSP)Interface Segregation Principle (ISP)Dependency Inversion Principle (DIP)**

**Law of Demeter (**

迪米特法则

**) or the Least Knowledge**

**Principle (**

最少知识原则

**)**

**Talk only to your immediate friends (**

不与陌生人讲话）

**Decouple between different classes**

**Composite Reuse Principle (**

合成复用原则

**)**

**Composition over inheritance: achieve**

**_code reuse_**

**by**

**composition rather than inheritance**


### Summary of Design

### Patterns

**The 23 Design Patterns**

```
Creational (
```
```
创建型
```
```
)
```
```
Singleton (
```
```
单件
```
```
); Factory Method (
```
```
工厂方法
```
```
); Abstract Factor (
```
```
抽象工厂
```
```
)
```
```
Builder (
```
```
生成器
```
```
): Separate the construction of a complex object
```
```
Prototype (
```
```
原型
```
```
): Create new objects by copying a prototypical instance
```
```
Structural (
```
```
结构型
```
```
)
```
```
Adapter (
```
```
适配器
```
```
); Proxy (
```
```
代理
```
```
)
```
```
Bridge (
```
```
桥连
```
```
): Decouple between interface and implementation
```
```
Composite (
```
```
组成
```
```
): Represent part-whole hierarchies of objects by a tree
```
```
structureDecorator (
```
```
装饰
```
```
) (or Wrapper): Attach additional responsibilities to an
```
```
object dynamicallyFacade (
```
```
外观
```
```
): Provide higher-level interface to decouple between clients
```
```
and the subsystem’s interfacesFlyweight (
```
```
享元
```
```
): Sharing large number of fine-grained objects to different
```
```
clients
```

```
Behavioral (
```
```
行为型
```
```
)
```
```
Template Method (
```
```
模板方法
```
```
)
```
```
Strategy (
```
```
策略
```
```
)
```
```
Observer (
```
```
观察者
```
```
)
```
```
Command (
```
```
命令
```
```
)
```
```
State (
```
```
状态
```
```
)
```
```
Iterator (
```
```
迭代器
```
```
): Access elements of an aggregate object sequentially
```
```
Chain of Responsibility (
```
```
职责链
```
```
): Pass request along the chain of objects
```
```
until an object handles itInterpreter (
```
```
解释器
```
```
): Interpret sentences of a language with its grammar
```
```
Mediator (
```
```
中介者
```
```
): Define an object encapsulating how objects interact
```
```
Memento (
```
```
备忘录
```
```
): Make a snapshot for an obje
```
```
ct to be restored to this
```
```
state later Visitor (
```
```
访问者
```
```
): Perform an operation on elements of an object structure
```
### Summary of Design

### Patterns


**More design patterns**

```
Functional, concurrency, architectural, distributed, etc. https://en.wikipedia.org/wiki/Design_Patterns
```
### Summary of Design

### Patterns


### Exercise

```
Exercise
```
```
Download from Tsinghua Web Learning
```
```
Optional exercise
```
```
Compile and run the Traffic Light example
```
```
Read the book “Head First Design
```
```
Patterns” or “Design Patterns:
```
```
Elements of Reusable Object-Oriented Software”
```
```
Review what we have learned
```
```
Read the book “Beginning C++17”
```
```
Preview Chapter 12: Operator OverloadingPreview Chapter 16: Introduction to Templates (
```
```
模板
```
```
)
```


