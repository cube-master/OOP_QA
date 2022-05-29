# Fundamentals of Object-Oriented Programming

## Lecture 13Hailong Yao

## hailongyao@tsinghua.edu.cn

子张问仁于孔子，孔子曰：“能行五者于天下，为仁矣。”“请问之。”曰：“恭，宽，信，敏，惠。恭则不侮，宽则得众，信则人任焉，敏则有功，惠则足以使人。”


## Overview

#### Operator Overloading (

#### 运算符重载

#### )

#### As Member FunctionsAs (Friend) General FunctionsSpecial OperatorsStream Operator (

##### 流运算符

##### )

##### Assignment Operator (

##### 赋值运算符

##### )

##### Operator new and deleteFunction Call Operator (

##### 函数运算符

##### ) (also

#### called Function Objects)Lambda ExpressionsSummary

```
2022/5/
```

## Operator Overloading

##### Operators (

##### 运算符

##### ): Originally defined for numeric

##### computations of built-in types (

##### 内置类型

##### )

**“+”, “-”, “*”, “/”: for**

**int, float**

**, and**

**double**

**numbers**

##### Operator overloading (

##### 运算符重载

##### ): use operators for

##### user-defined data types (classes)Syntactic sugar (

语法糖

**): another way of function call**

```
Function name is “
```
```
operator @
```
```
” (@
```
```
represents an operator)
```
**Use operator overloading when there is a good reasonE.g., for better readability or wr**

```
itability, for using STL, etc.
```
##### Two ways of operator overloading: (1) as

##### member

##### function (

##### 类成员函数

##### ), and

##### (2) as (

##### friend,

##### 友元

##### )

##### general function

```
2022/5/
```

```
2022/5/
```
#include

<cstdio>
class

```
complex
```
```
{
double
```
```
re,^ im;
```
```
int
```
```
id;^
```
```
static
```
```
int
```
```
count;
```
```
public
```
```
: complex()
```
```
{^ //
```
```
Default
```
```
constructor
```
```
count++;
```
```
id^
```
```
=^ count;
```
```
re^
```
```
=^ im =
```
```
0.0;
```
```
printf
```
```
("%d^
```
```
constructed
```
```
in^ complex()\n"
```
```
,^ id);
```
```
} complex
```
```
(double
```
```
re,^ double
```
```
im)^ {
```
```
//^ Constructor
```
```
count++;
```
```
id^
```
```
=^ count;
```
```
this
```
```
‐>re^
```
```
=^ re;
```
```
this
```
```
‐>im =
```
```
im;
```
```
printf
```
```
("%d^
```
```
constructed
```
```
in^ complex(%g,
```
```
%g)\n"
```
```
,^ id,
```
```
re,^
```
```
im)
```
```
; } complex
```
```
(const
```
```
complex
```
```
&^ c)^
```
```
{^ //^
```
```
Copy^
```
```
constructor
```
```
count++;
```
```
id^
```
```
=^ count;
```
```
re^
```
```
=^ c.re;
```
```
im =
```
```
c.im;
```
```
printf
```
```
("%d^
```
```
copied
```
```
in^ complex(const
```
```
complex&)
```
```
from
```
```
%d\n"
```
```
,^
```
```
id,^ c.id);
} ~complex
```
```
()^ {^
```
```
//^ Destructor
count
```
```
‐‐;^ printf
```
```
("%d^
```
```
destructed
```
```
in^ ~complex()\n"
```
```
,^ id);
```
```
}
```
##### Demo


```
2022/5/
```
void

**show** ()

{^
**printf**

```
("id^
```
```
=^ %d:
```
```
re^ =
```
```
%^ 5.2f,
```
```
im =
```
```
%^ 5.2f\n"
```
```
,^ id,
```
```
re,^
```
```
im);^
```
```
} //overloaded
```
```
as^ friend
```
```
function
```
```
friend
```
```
complex
```
```
operator
```
```
+^ (const
```
```
complex
```
```
&^ left,
const
```
```
complex
```
```
&^ right);
```
```
friend
```
```
complex
```
```
operator
```
```
‐(const
```
```
complex
```
```
&^ left,
const
```
```
complex
```
```
&^ right);
```
```
//overloaded
```
```
as^ member
```
```
function
```
```
complex
```
```
&^ operator
```
```
=^ (const
```
```
complex
```
```
&^ c)^
```
```
{^
```
```
if(this
```
```
!=^ &c)
```
```
{^ //
```
```
Avoid
```
```
self
```
```
‐assignment
```
```
re^ =^
```
```
c.re;
im =^
```
```
c.im;
} printf
```
```
("assignment\n"
```
```
);
```
```
return
```
```
*this
```
```
;^
```
```
} }; // objA = objB = objC ...
```

```
2022/5/
```
int^ complex

::count

{^0 };

```
complex
```
```
operator
```
```
+^ (const
```
```
complex
```
```
&^ left,
```
```
const
```
```
complex
```
```
&^ right)
```
```
{ return
```
```
complex
```
```
(left.re
```
```
+^ right.re,
```
```
left.im
```
```
+^ right.im);
```
```
} complex
```
```
operator
```
```
‐(const
```
```
complex
```
```
&^ left,
```
```
const
```
```
complex
```
```
&^ right)
```
```
{ return
```
```
complex
```
```
(left.re
```
```
 ‐right.re,
```
```
left.im
```
```
 ‐right.im);
```
```
} complex
```
```
&^ func
```
```
(complex
```
```
&^ c)^
```
```
{^ return
```
```
c;^
}
```

```
2022/5/
```
int **main**

()^
{

```
complex
```
```
c;
printf
```
```
("begin....\n"
```
```
);
```
```
func (c); printf
```
```
("end.\n"
```
```
);
```
```
complex
```
```
c1 {1.
```
```
,^ 2.
```
```
};
```
```
complex
```
```
c2 {2.
```
```
,^ 4.
```
```
};
```
```
c^ =^ c
```
```
+^ c2;
c. show
```
```
();
complex
```
```
cc^ =^
```
```
c^ =^ c
```
```
 ‐c2;
```
```
c. show
```
```
();
cc. show
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
2022/5/
1 constructed in complex()begin....end.2 constructed in complex(1, 2)3 constructed in complex(2, 4)4 constructed in complex(3, 6)assignment4 destructed in ~complex()id = 1: re = 3.00, im = 6.004 constructed in complex(-1, -2)assignment5 copied in complex(const complex&) from 14 destructed in ~complex()id = 1: re = -1.00, im = -2.00id = 5: re = -1.00, im = -2.005 destructed in ~complex()3 destructed in ~complex()2 destructed in ~complex()1 destructed in ~complex()
```
##### Results

```
void
```
```
main ()
```
```
{
complex
```
```
c;
printf
```
```
("begin....\n"
```
```
);
```
```
func (c); printf
```
```
("end.\n"
```
```
);
```
```
complex
```
```
c1 {1.
```
```
,^ 2.
```
```
};
```
```
complex
```
```
c2 {2.
```
```
,^ 4.
```
```
};
```
```
c^ =^
```
```
c1^ +^
```
```
c2;
c. show
```
```
();
complex
```
```
cc^ =^
```
```
c^ =^ c
```
```
 ‐c2;
```
```
c. show
```
```
();
cc. show
```
```
();
return
```
```
0 ;
}
```
##### Source code


## Restrictions on Operator

## Overloading

#### RestrictionsCannot change operator’s usage (

##### 用法不能变

##### )

**cout << a << endl;**

 **a << cout;**



##### Cannot define new operatorsIllegal (

非法的

**): use “**” for exponentiation**

##### Cannot change

##### precedence rules (

##### 运算符优先级

##### )

##### “*” > “+”“+” > “||”Cannot change the number of operandsUnary (

一元运算符

**): “++”, “--"**

**Binary (**

二元运算符

**): “+”, “-”, “*”, “/”**

##### Operators that cannot be overloaded“.”, “.*”, “::”, “?:”

```
2022/5/
```

### Overloaded as

### Member Function

##### Assume objects x and y of class

##### TYPE

##### Binary operator “@”x @ y;



```
x.operator @ (y);
Example:
```
**bool operator >= (const TYPE& right) const;**

##### Prefix (

##### 前缀

##### ) unary operator “@”

**@ x;**



```
x.operator @();
Member function:
```
**const TYPE& operator ++() {...}**

##### Postfix (

##### 后缀

##### ) unary operator “@”

**x @;**



```
x.operator @(0); // 0 is a dummy variable
Member function:
```
**const TYPE& operator ++(int) {...}**

```
The dummy
```
```
intargument differentiates postfix from prefix
```
```
2022/5/
```

```
2022/5/
```
class

Byte^

{
unsigned

```
char
```
```
b;
```
```
public
```
```
: Byte (unsigned
```
```
char
```
```
bb^ =^
```
```
0 )^ :^
```
```
b {bb}
```
```
{}
```
```
//^ No
```
```
side
```
```
effects:
```
```
const
```
```
member
```
```
function:
```
```
const
```
```
Byte&
```
```
operator
```
```
+()^ const
```
```
{^ //^
```
```
No^ effect
```
```
cout <<
```
```
"+Byte\n"
```
```
;
```
```
return
```
```
*this
```
```
;
```
```
} //^ Side
```
```
effects:
```
```
non‐
```
```
const
```
```
member
```
```
function:
```
```
const
```
```
Byte&
```
```
operator
```
```
++()^
```
```
{^ //^
```
```
Prefix
```
```
cout <<
```
```
"++Byte\n"
```
```
;
```
```
b++;return
```
```
*this
```
```
;^ //
```
```
Return
```
```
the^
```
```
object
```
```
itself
```
```
as^
```
```
reference} const
```
```
Byte^
```
```
operator
```
```
++(int
```
```
)^ {^ //
```
```
Postfix
```
```
cout <<
```
```
"Byte++\n"
```
```
;
```
```
Byte^
```
```
before
```
```
{b};
b++;return
```
```
before;
```
```
//^ Return
```
```
by^ value,
```
```
not^
```
```
reference
```
```
} };
```
##### Demo


#### Overloaded as

#### (Friend) Function

```
2022/5/
```
##### Assume objects x and y of class

##### TYPE

##### Binary operator “@”x @ y;



```
operator @(x, y);
friend
```
**bool operator >= (const TYPE& left, const**

##### TYPE& right);Prefix unary operator “@”@ x;



```
operator @(x);
friend
```
**const TYPE& operator++(TYPE& a);**

##### Postfix unary operator “@”x @;



```
operator @(x, 0);
friend const TYPE operator++(TYPE& a, int);The dummy
```
```
intargument differentiates postfix from prefix
```
##### Note: keyword

##### friend

##### may be omitted


//^ Overloaded

as^ non

‐member

friend

functions

```
class
```
```
Integer
```
```
{
long
```
```
i;
Integer*
```
```
This
```
```
()^ {^
```
```
return
```
```
this
```
```
;^ }
```
```
public
```
```
: Integer (long
```
```
ll =^
```
```
0 )^ :^
```
```
i {ll}
```
```
{}
```
```
friend
```
```
const
```
```
Integer&
```
```
operator
```
```
+(const
```
```
Integer&
```
```
a);
```
```
friend
```
```
Integer*
```
```
operator
```
```
&(Integer&
```
```
a);
```
```
friend
```
```
intoperator
```
```
!(const
```
```
Integer&
```
```
a);
```
```
//^ Prefix:friend
```
```
const
```
```
Integer&
```
```
operator
```
```
++(Integer&
```
```
a);
```
```
//^ Postfix:friend
```
```
const
```
```
Integer
```
```
operator
```
```
++(Integer&
```
```
a,^ int
```
```
);
```
```
}; const
```
```
Integer&
```
```
operator
```
```
+(const
```
```
Integer&
```
```
a)^ {
```
```
cout <<
```
```
"+Integer\n"
```
```
;
```
```
return
```
```
a;^ //
```
```
Unary
```
```
+^ has
```
```
no^ effect
```
```
} ......
```
```
2022/5/
```
##### Demo


#### Member vs. General (Friend)

#### Functions

#### Which one is better?Prefer overloaded member functions

##### to

##### emphasize (

##### 强调

##### ) association between operator

##### and classBut not all operators can be overloaded as memberswhen left-hand operand (

左操作数

**) is not an object of**

**the class,**

```
the operator can only be overloaded as
general (
```
**friend)**

**functions**

**Example:**

**overloaded stream operator “<<”**

```
2022/5/
```

### Stream Operator (

### 流运算符

### )


##### int

##### a^ {^10

##### };

##### cout <<

##### a;^

##### //OK

##### Why can’t I do this? ClassA

##### b;

##### cout << b;

```
2022/5/
```
##### OK! But you need to define overloaded stream operator (

##### 重载流运算符

##### )!


### Overloaded Stream Operators

##### cin/cout

##### is object of fundamental C++ class

##### istream/ostreamExample:

##### stream operator

##### for built-in types

**int i; cout**

```
<<i;
const char *s = “HelloWorld”; cout
```
**<< s <<**

**“”<< (void *)s <<**

**endl;**

```
cout << s; //prints the stringcout << (void *)s; //prints the address of the stringStream operator is overloaded for built-in types
```
##### NOTE: Stream operators (“<<” and “>>”) can only be overloaded as general

##### functions (

##### 普通函数

##### )(

##### not necessarily

##### friend

##### )

**cout << obj;**



**operator << (cout, obj);**

```
2022/5/
```

#### Why Not Member Function?

**For a binary operator overloaded as**

**member function**

**, the**

**operator is called by left-hand objectx @ y;**

```
 x.operator @ (y);
So we have: TYPE obj; cout << obj;
```
```
 cout.operator << (obj);
```
```
Therefore, if stream operator
```
```
s are overloaded as member
```
```
functions, we need to modify
```
```
istream
```
```
and ostream
```
```
! 
```
**For a binary operator overloaded as general (**

**friend) functions**

**,**

**there is no such constraint on left-hand objectx @ y;**

```
 operator @(x, y);
cout << obj;
```
```
 operator << (cout, obj);
```
**Therefore, stream operators (“<<” and “>>”) can ONLY be overloaded as general functions, either**

**_friend_**

**or not**

```
2022/5/
```

### (Review) Example 2022/5/

```
#ifndef POINT_H_#define
```
```
POINT_H_
#include
```
```
<iostream>
using
```
```
std::ostream;
class
```
```
Point
{ public
```
```
: Point (
```
```
intx,
```
```
int
```
```
y)^ :^
```
```
x_ {x},
```
```
y_ {y}
```
```
{}
```
```
friend
```
```
ostream &
```
```
operator
```
```
<<^ (ostream &myOutput,
```
```
const
```
```
Point
```
```
&^ point);
private
```
```
: intx_;inty_;
};#endif
```
##### point.h Demo


```
2022/5/
```
#include

<iostream>
#include

```
"point.h"
using
```
```
std::endl;
ostream &
```
```
operator
```
```
<<^ (ostream &myOutput,
```
```
const
```
```
Point
```
```
&^
```
```
point){
```
```
myOutput <<
```
```
"MYOUTPUT:
```
```
Point
```
```
("<<
```
```
point.x_
```
```
<<^ ","
```
```
<<^ point.
```
```
y_^ <<
```
```
")"
```
```
<<^ endl;
return
```
```
myOutput;
}
```
**point.cpp**


```
2022/5/24
```
```
#include
```
```
<iostream>
#include
```
```
<fstream>
#include
```
```
"point.h"
using
```
```
std::cout;
```
```
using
```
```
std::cerr;
```
```
using
```
```
std::endl;
```
```
using
```
```
std::ofstream;
int main
```
```
(void
```
```
)
{
```
```
Point
```
```
point
```
```
{^2 ,^5 };
ofstream
```
```
file_out
```
```
{"result.txt"
```
```
};
```
```
if(!file_out){
```
```
cerr <<
```
```
"Error
```
```
in^ opening
```
```
file
```
```
result.txt"
```
```
<<^ endl;
```
```
exit (
```
```
‐^1 );
} file_out <<
```
```
point
```
```
<<^ endl;
```
```
cout <<
```
```
point
```
```
<<^ endl;
return
```
```
0 ;
}
```
**main.cpp**

```
Write to fileWrite to standard output
```

### Assignment Operator (

### 赋值运算符

### )


ClassA

a;
ClassA

```
b;
```
##### a=b; //Does this work? Why?

```
2022/5/24
```
##### Yes! The compiler helped us in assignment using bitcopy!Shall we depend on the compiler?NO! What if there are pointer members???


```
2022/5/24
```
##### Never trust the compiler!Always define your own

##### copy/move constructors

##### and

##### copy/move assignment operators

##### when needed,

##### especially when the class has pointer members.


## Assignment Operator

```
2022/5/24
```
##### TYPE&

##### operator

##### =^ (const

##### TYPE&

##### src)

##### {

##### if(&src !=

##### this

##### )

##### {^

##### //assignment

##### ...

##### } return

##### *this

##### ;

##### }

**x = y = z: first assigns z to y, then returned value y is assigned to x;Besides, allows (x=y)=z, same as built-in types.**

**Avoid copy constructor**

**Accept temporary objects generated by automatic type conversion**

**Avoid self-assignment (** 自赋值

**)**


### Notes on Assignment OperatorReturn reference of

##### *this

##### TYPE& TYPE::operator=(const TYPE&);x=y=z;(i1=i2)=i3;Need to assign values to all data membersBe careful for

**inheritance**

##### Avoid self-assignment (

##### 自赋值

##### )

**For correctness**

**: what will happen if there are pointer**

**members?First delete the pointer member to free the memoryThen assign the**

```
dangling pointer(
```
```
悬挂指针
```
```
) to itself
```
**For efficiency**

**: self-assignment is meaningless but**

**consumes runtime**

```
2022/5/24
```

```
2022/5/24
```
##### //^ ......//as

##### member

##### function

##### complex

##### &^ operator

##### =^ (const

##### complex

##### &^ c)

##### {^

##### if(

##### this

##### !=^ &c)

##### {^ //

##### Avoid

##### self

##### ‐assignment

##### re^ =

##### c.re;

##### im =

##### c.im;

##### } printf

##### ("assignment\n"

##### );

##### return

##### *this

##### ;^

##### } // objA = objB = objC


#### Assignment Operator vs. ConstructorAssignment operator is called when the object has already been defined, i.e., memory has already been allocatedTYPE OldObj;

###### TYPE NewObj;

###### NewObj = OldObj

###### ;

##### Constructor (including

##### copy constructor

##### ) is called

##### when the object is being defined, i.e., when the memory needs to be allocatedTYPE OldObj;

###### TYPE NewObj = OldObj

###### ;

```
2022/5/24
```

### Move

### Assignment

```
2022/5/24
```
#include

<iostream>
#include

```
<cstring>
using^ namespace
```
```
std;
classA
```
```
{ int*m_arr;
```
```
intm_size;
public: A (int
```
```
i): m_size
```
```
{i}^ {
m_arr =
```
```
newint
```
```
[m_size];
memset (m_arr,
```
```
 0 ,^ m_size*
```
```
sizeof(
```
```
int));
```
```
} //copy^
```
```
constructor
A (const
```
```
A&^ a): m_size
```
```
{a.m_size}
```
```
{
```
```
this‐>m_arr =
```
```
newint
```
```
[this‐>m_size];
```
```
for(int
```
```
i=^0 ;^
```
```
i<^ this
```
```
‐>m_size;
```
```
++^ i)^
```
```
{
```
```
this‐>m_arr[i]
```
```
=^ a.m_arr[i];
}}//move^ constructor A (A&&^ a): m_size
```
```
{a.m_size}
```
```
{
```
```
this‐>m_arr =
```
```
a.m_arr;
a.m_arr =
```
```
nullptr
```
```
;
```
```
} //move^
```
```
assignment
A&^ operator
```
```
=(A&&^ a)
```
```
{
if(&a^
```
```
==^ this
```
```
)
return
```
```
*this;
this‐>m_size =
```
```
a.m_size;
if (this
```
```
‐>m_arr)
```
```
delete
```
```
this‐>m_arr;
```
```
this‐>m_arr =
```
```
a.m_arr;
a.m_arr =
```
```
nullptr
```
```
;
return
```
```
*this;
} ~ A ()^ {^
```
```
delete
```
```
[]m_arr;
```
```
}
```
```
void set
```
```
(intindex,
```
```
intvalue)
```
```
{
```
```
m_arr[index]
```
```
=^ value;
} void print
```
```
();
};
```
```
voidA
```
```
:: print
```
```
()
{ cout <<
```
```
"m_arr:
```
```
";
for(int
```
```
i=^0 ;
```
```
i<^ m_size;
```
```
++^ i)
```
```
{ cout <<
```
```
"^ "<<
```
```
m_arr[i];
```
```
} cout <<
```
```
endl;
} int main
```
```
()^ { A a { 5 };A b { 7 };b = move (a);
```
```
//call
```
```
the^ move
```
```
assignment
```
```
a. print
```
```
();^ //what
```
```
happens
```
```
here?
```
```
b. print
```
```
();
b. set (
```
```
2 ,^10 );
b. print
```
```
();
a. print
```
```
();
} Be careful with move constructorand move assignment!
```
##### Demo


#### Move Constructor, Move Assignment Operator, and Assignment OperatorWhen a constructor (ordinary/copy/move constructor) is defined, the compiler will not synthesize a default one. When a move constructor or move assignment operator is declared, the copy constructor is implicitly declared as deleted When a move constructor is not defined, “A d = move(b);” will call copy constructor “A(

**const**

**A& a)” (const is**

**required)Assignment operator is implicitly declared as**

**_deleted_**

**when a**

**move constructor or move assignment operator is declaredWhen a move assignment operator is not defined, “b = move(a);” will call assignment operator “A& operator=(**

**const**

**A& a)” (const is required)**


### Operator

### new

### and

### delete


## Overloaded Operator

## new/delete

##### When calling “A *pA = new A;” or “A *pA = new A[10];”, the following steps are executed1. “operator new” or “operator new []” is called to allocate the raw memory2. Constructor is called to construct the object(s) and initialize the members3. Return pointer to the object or array of objectsWhen calling “delete pA;” or “delete [] pA;”, the following steps are executed Destructor is called for the object or array of objects“operator delete” or “operator delete []” is called to free the memory


## Overloaded operator

## new/delete

**Operator**

**_new_** **/**

**_delete_**

**can be overloaded**

```
As functions in global scope (
```
```
全局作用域）
```
```
As member functions of a class (as
```
```
static
```
```
, no class members are
```
**accessible when allocating/deleting memories)When calling**

**_operator new_**

**/** **_delete_**

**for an object, the compiler**

```
searches for the new/delete operator in the following order:1. Members of the corresponding class and the base class2. Global scope for user-defined operators3. Standard library
class^
```
```
Test^ {
public:static
```
```
void*
```
```
operator
```
```
new(size_t size);
```
```
static
```
```
void*
```
```
operator
```
```
new(size_t size,
```
```
void^
```
```
*ptr);
```
```
//placement
```
```
new
```
```
static
```
```
void*
```
```
operator
```
```
new[](size_t size);
```
```
static
```
```
void*
```
```
operator
```
```
new[](size_t size,
```
```
void^
```
```
*ptr);
```
```
//placement
```
```
new
```
```
static
```
```
void^
```
```
operator
```
```
delete(void*
```
```
ptr,^
```
```
size_t size);
```
```
static
```
```
void^
```
```
operator
```
```
delete[](void*
```
```
ptr,^
```
```
size_t size);
```
```
};
```
##### Demo


## Allocator Class

##### Note: Modern C++ programs typically use the allocator

##### class to allocate memory, which is safe and

##### flexibleTypically for developing libraries such as STL, where the user of the container can control where memory gets allocatedhttps://en.cppreference.com/w/cpp/memory/allocator

```
template<class
```
```
T,
class
```
```
Allocator
```
```
=^ std::allocator<T>
```
```
>^ class
```
```
vector;
```

### Function Pointer

### ( 函数指针

### )


## Problem

```
2022/5/24
```
```
#include
```
```
<iostream>
using
```
```
namespace
```
```
std;
```
```
int main
```
```
()^ {
inta[
```
```
10 ]^ =
```
```
{^12 ,
```
```
 1 ,^454
```
```
,^45 ,
```
```
 67 ,^
```
```
162 ,^
```
```
2 ,^90
```
```
,^15 ,
```
```
 49 };
```
```
cout <<
```
```
"^ >^
```
```
30:^ "
```
```
<<^ endl;
```
```
for(
```
```
inti=
```
```
0 ;^ i<
```
```
10 ;^ i++)
```
```
if(a[i]
```
```
>^30
```
```
)^ cout <<
```
```
a[i]
```
```
<<^ endl;
```
```
cout <<
```
```
"^ %2
```
```
==^ 1:
```
```
"<<
```
```
endl;
```
```
for(
```
```
inti=
```
```
0 ;^ i<
```
```
10 ;^ i++)
```
```
if(a[i]
```
```
%^2 )
```
```
cout <<
```
```
a[i]
```
```
<<^ endl;
```
```
return
```
```
0 ;
}
```
**avoid**

```
code
repetition?
```

### Improvement

```
2022/5/24
```
```
#include
```
```
<iostream>
using
```
```
namespace
```
```
std;
```
```
bool
```
```
Greater_30
```
```
(int
```
```
x)^ {^
```
```
return
```
```
(x^ >^
```
```
30 );^
```
```
}
```
```
bool
```
```
Mod_2
```
```
(int
```
```
x)^ {^
```
```
return
```
```
(x%^2 );
```
```
}
```
```
void
```
```
Disp (
```
```
inta[],
```
```
int
```
```
len,^
```
```
bool
```
```
(*op)(
```
```
int))
```
```
{
```
```
for(
```
```
inti=
```
```
0 ;^ i<len;
```
```
i++)
```
```
if( op
```
```
(a[i]))
```
```
cout <<
```
```
a[i]
```
```
<<^ endl;
```
```
} int main
```
```
()^ {
inta[
```
```
10 ]^ =
```
```
{^12 ,
```
```
 1 ,^454
```
```
,^45 ,
```
```
 67 ,^
```
```
162 ,^
```
```
2 ,^90
```
```
,^15 ,
```
```
 49 };
```
```
cout <<
```
```
"^ >^
```
```
30:^ "
```
```
<<^ endl;
```
```
Disp (a,
```
```
 10 ,^
```
```
Greater_30);
cout <<
```
```
"^ %2
```
```
==^ 1:
```
```
"<<
```
```
endl;
```
```
Disp (a,
```
```
 10 ,^
```
```
Mod_2);
return
```
```
0 ;
}
```
### void Disp(...)?


### Defining Pointers to Functions

##### Function:long find_maximum(const long* array, size_t size);Pointer definition: long

(*pfun)(

const

long

*,^ size_t

)^ {^ find_maximum };

auto

pfun =

find_maximum;

or^ auto

*^ pfun =

find_maximum;

```
int product
```
```
(int
```
```
a,^ int
```
```
b){
```
```
std::cout <<
```
```
a^ *^
```
```
b^ <<^
```
```
std::endl;
```
```
return
```
```
a^ *^ b;
```
```
} int main
```
```
()^ { int(*pDo_it)(
```
```
int,^
```
```
int)^
```
```
{^ product
```
```
};^
```
```
cout <<
```
```
"pDo_it(3,
```
```
5)^ "
```
```
<<^ pDo_it
```
```
(^3 ,^5
```
```
)^ <<^
```
```
endl;
```
```
auto
```
```
pDo_it2
```
```
=^ product;
cout <<
```
```
"pDo_it2(3,
```
```
5)^ "
```
```
<<^ pDo_it2
```
```
(^3 ,^5
```
```
)^ <<^
```
```
endl;
```
```
auto
```
```
*pDo_it3
```
```
=^ product;
cout <<
```
```
"pDo_it3(3,
```
```
5)^ "
```
```
<<^ pDo_it3
```
```
(^3 ,^5
```
```
)^ <<^
```
```
endl;
```
```
}
```

### Callback Functions for Higher-

### Order Functions

##### Use pointer to function as an argument in function #include

```
<vector>
template
```
```
<typename T>
const
```
```
T*^ find_optimum
```
```
(const
```
```
std::vector<T>&
```
```
values,
```
```
bool(*compare)(
```
```
const
```
```
T&,^ const
```
```
T&))
```
```
{
if(values.
```
```
empty
```
```
())^ return
```
```
nullptr
```
```
;
```
```
const
```
```
T*^ optimum
```
```
=^ &values[
```
```
0 ];
```
```
for(
```
```
size_t
```
```
i=^1
```
```
;^ i<
```
```
values.
```
```
size ();
```
```
++i)
```
```
{ if
```
```
( compare
```
```
(values[i],
```
```
*optimum))
```
```
{ optimum
```
```
=^ &values[i];
} } returnoptimum;
}
```
##### Demo


### Callback Functions for Higher-

### Order Functions

```
//^ Comparison
```
```
prototypes:
bool
```
```
less (
```
```
const
```
```
int&
```
```
one,
```
```
const
```
```
int&
```
```
other)
```
```
{^ return
```
```
one^ <
```
```
other;
```
```
}
```
```
template
```
```
<typename T>
bool
```
```
greater
```
```
(const
```
```
T&^ one,
```
```
const
```
```
T&^ other)
```
```
{^ return
```
```
one^ >
```
```
other;
```
```
}
```
```
bool
```
```
longer
```
```
(const
```
```
string&
```
```
one,
```
```
const
```
```
string&
```
```
other)
```
```
{
```
```
return
```
```
one. length
```
```
()^ >^
```
```
other.
```
```
length
```
```
();^ }
```
```
int main
```
```
(){vector<int
```
```
>^ numbers{
```
```
 91 ,^
```
```
18 ,^92
```
```
,^22 ,
```
```
 13 ,^
```
```
43 };
```
```
cout<<
```
```
"Minimum
```
```
element:
```
```
"<<*
```
```
find_optimum
```
```
(numbers,
```
```
less)<<endl;
```
```
cout<<
```
```
"Maximum
```
```
element:
```
```
"<<*
```
```
find_optimum
```
```
(numbers,
```
```
greater<
```
```
int>)<<endl;vector<string>
```
```
names{
```
```
"Moe"
```
```
,^ "Larry"
```
```
,^ "Shemp"
```
```
,^ "Curly"
```
```
,^ "Joe"
```
```
,^
```
```
"Curly
```
```
Joe"
```
```
};
cout<<
```
```
"Alphabetically
```
```
last
```
```
name:
```
```
"<<*
```
```
find_optimum
```
```
(names,
```
```
greater<string>)<<endl;cout<<
```
```
"Longest
```
```
name:
```
```
"<<*
```
```
find_optimum
```
```
(names,
```
```
longer)<<endl;
```
```
}
```

#### Previous Example Use Pointers to

#### Functions (

#### 函数指针

#### )

```
2022/5/24
```
```
#include
```
```
<iostream>
using
```
```
namespace
```
```
std;
```
```
bool
```
```
Greater_30
```
```
(int
```
```
x)^ {^
```
```
return
```
```
(x^ >^
```
```
30 );^
```
```
}
```
```
bool
```
```
Mod_2
```
```
(int
```
```
x)^ {^
```
```
return
```
```
(x%^2 );
```
```
}
```
```
void
```
```
Disp (
```
```
inta[],
```
```
int
```
```
len,^
```
```
bool
```
```
(*op)(
```
```
int) )
```
```
{
```
```
for(
```
```
inti=
```
```
0 ;^ i<len;
```
```
i++)
```
```
if( op
```
```
(a[i]))
```
```
cout <<
```
```
a[i]
```
```
<<^ endl;
```
```
} int main
```
```
()^ {
inta[
```
```
10 ]^ =
```
```
{^12 ,
```
```
 1 ,^454
```
```
,^45 ,
```
```
 67 ,^
```
```
162 ,^
```
```
2 ,^90
```
```
,^15 ,
```
```
 49 };
```
```
cout <<
```
```
"^ >^
```
```
30:^ "
```
```
<<^ endl;
```
```
Disp (a,
```
```
 10 ,^
```
```
Greater_30);
cout <<
```
```
"^ %2
```
```
==^ 1:
```
```
"<<
```
```
endl;
```
```
Disp (a,
```
```
 10 ,^
```
```
Mod_2);
return
```
```
0 ;
}
```
**What**

**if**^ **I**^ **want**

```
>40,^
>50,^ %3,
```
**%5...**^**?**


### Function Call Operator “()”

### ( 函数调用运算符

### )

###  Function Object (

### 函数对象

### )


#### Function Object/Functor (

#### 函数对象

#### )

##### Function object or functor:

##### an object of a class

##### with

##### overloaded function call operator “

##### ()”

**A function object can be called as if it were a function.Often used in STLFunction call operator is overloaded as member function**

```
2022/5/24
```
##### class

##### FuncObj_Type {

##### public:Return_Type operator

##### ()^ (ParameterList);

##### };


#### Function Object Example

```
2022/5/24
```
class

```
F^ {
public
```
: booloperator

```
()^ (
intx)
```
{

return

(x^ >^

30 );

} }; int **main**

```
()^ {
F^ f;bool
```
```
res^
=^ f (^43
```
);

return

```
0 ;
}
```
**Function objectCalling the overloaded function operator**


### Advantage of Function Object

### over Function Pointer

##### Parameterized function objects: a function object can store and pass data (

##### 存储和传递数据

##### )

```
2022/5/24
class
```
```
F^ { intdata;
public
```
```
: F (intval)
```
```
:^ data
```
```
{val}
```
```
{^ }
```
```
bool
```
```
operator
```
```
()^ (int
```
```
x)^ {
```
```
return
```
```
(x^ >^
```
```
data);
```
```
} }; int main
```
```
()^ {
F^ f {^30
```
```
};
bool
```
```
res^ =
```
```
f (^43
```
```
);
```
```
return
```
```
0 ;
}
```

#### Previous Example Using Function

#### Objects

```
2022/5/24
```
```
#include
```
```
<iostream>
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
F^ { intdata;
public
```
```
: F (intval)
```
```
:^ data
```
```
{val}
```
```
{^ }
```
```
bool
```
```
operator
```
```
()^ (int
```
```
x)^ {^
```
```
return
```
```
(x^ >^
```
```
data);
```
```
}
```
```
};void
```
```
Disp (
```
```
inta[],
```
```
int
```
```
len,^
```
```
F^ op)
```
```
{
```
```
for(
```
```
inti=
```
```
0 ;^ i<len;
```
```
i++)
```
```
if( op
```
```
(a[i]))
```
```
cout <<
```
```
a[i]
```
```
<<^ endl;
```
```
} int main
```
```
()^ {
inta[
```
```
10 ]^ =
```
```
{^12 ,
```
```
 1 ,^454
```
```
,^45 ,
```
```
 67 ,^
```
```
162 ,^
```
```
2 ,^90
```
```
,^15 ,
```
```
 49 };
```
```
intb[
```
```
3 ]^ =^
```
```
{^30 ,^
```
```
150 ,^
```
```
300 };
```
```
for(
```
```
intk=
```
```
0 ;^ k<
```
```
3 ;^ k++)
```
```
Disp (a,
```
```
 10 ,^
```
```
F (b[k]));
```
```
}
```

### Standard Function Objects

### Header file <functional> std::vector<

```
int>^
```
```
numbers{
```
```
 91 ,^
```
```
18 ,^92
```
```
,^22 ,
```
```
 13 ,^
```
```
43 };
```
```
std::cout <<
```
```
"Minimum
```
```
element:
```
```
"<<
```
```
* find_optimum
```
```
(numbers,
```
```
std::less<>
```
```
{})^
```
```
<<^ std
```
```
::endl;
```
```
std::cout <<
```
```
"Maximum
```
```
element:
```
```
"<<
```
```
* find_optimum
```
```
(numbers,
```
```
std::greater<>
```
```
{})^
```
```
<<^ std
```
```
::endl;
```

### Lambda Expressions(Lambda

### 表达式

### )


## Lambda Expression

##### Lambda expressionProvides a convenient and compact syntax to quickly define callback functions or functorsAllows definition of the callback’s logic

**_right there_**

**where**

**you want to use it (**

定义的同时使用

**)**

##### Can access variables in the enclosing scope where the lambda expression is definedBy function pointers, function objects, and lambda expressions, we may treat

##### functions

##### like

##### variables

**C++ offers**

**_first-class functions_**

**, where we may use**

**functions as if they were of built-in types**

**(** 把函数当成内置类

型来使用

**)**


### Defining a Lambda Expression

#### [] (int x, int y) { return x < y; }Whenever the compiler encounters a lambda expression, it internally generates

##### a new class type

##### [] (int x, int y) ->

##### bool

##### { return x < y; }

**lambda**

```
introducer
(捕获子句)
```
**statements**

**parameter**

**list**

class

```
__Lambda8C1{
public
```
: auto^ operator

()(int

x,^ int

y)^ const

{^ return

x^ <^ y;}

};

**random**

**class**^

**name**

**Return**

**type:**

**could**

**be**^ **omitted**

**as**^ **the**

**compiler**

**will**^ **generate**

**implicit**

**conversions**

```
from
the^ return
```
**statements**


### Passing a Lambda Expression

### to a Function Template

```
auto
```
```
less^
```
```
{^ //defines
```
```
a^ lambda
```
```
expression
```
```
named
```
```
as^ less
```
```
[]^ (int
```
```
x,^ int
```
```
y)
```
```
{ return
```
```
x^ <^ y;
} };std::cout <<
```
```
"Minimum
```
```
element:
```
```
"<<
```
```
* find_optimum
```
```
(numbers,
```
```
less)
```
```
<<^
```
```
std::endl;
std::cout <<
```
```
"Minimum
```
```
element:
```
```
"<<
```
```
* find_optimum
```
```
(numbers,
```
```
[]^ (
```
```
int
```
```
x,^ int
```
```
y){^ return
```
```
x^ <^ y;})
```
```
<<^ std
```
```
Same effect::endl;
Stateless
```
lambda

expression

without

capture

clause

cannot

access

anything

in^ its^

enclosing

scope


## Capturing by Value (

## 值传递

## )

#### [=] (int x, int y) { return x < y; } Allows^ all

**variables**

**in**^ **the**

**scope**

**of**^ **lambda**

**definition**

**to**^ **be**

**accessed**

**_by_**^ **_value_**

```
#include
```
```
<vector>
template
```
```
<typename T,
```
```
typename Comparison>
```
```
const
```
```
T*^ find_optimum
```
```
(const
```
```
std::vector<T>&
```
```
values,Comparison compare)
```
```
{ if
```
```
(values.
```
```
empty
```
```
())^ return
```
```
nullptr
```
```
;
```
```
const
```
```
T*^ optimum
```
```
=^ &values[
```
```
0 ];
```
```
for(
```
```
size_t
```
```
i=^1
```
```
;^ i<
```
```
values.
```
```
size ();
```
```
++i)
```
```
{ if
```
```
( compare
```
```
(values[i],
```
```
*optimum))
```
```
{ optimum
```
```
=^ &values[i];
}
} returnoptimum;
}
```
```
Optimum.h
```

## Capturing by

## Value

#### [=] (int x, int y) { return x < y; } #include

```
"Optimum.h"
int main
```
```
() {std::vector<
```
```
int>^
```
```
numbers{
```
```
 91 ,^
```
```
18 ,^92
```
```
,^22 ,
```
```
 13 ,^
```
```
43 };
```
```
intnumber_to_search_for {};std::cout <<
```
```
"Please
```
```
enter
```
```
a^ number:
```
```
";
```
```
std::cin >>
```
```
number_to_search_for
```
```
;^
```
```
auto
```
```
nearer
```
```
{^ [=](
```
```
intx,
```
```
int
```
```
y)^ {
```
```
return
```
```
std::
```
```
abs (x
```
```
 ‐number_to_search_for)
```
```
<^ std
```
```
:: abs
```
```
(
```
```
y ‐number_to_search_for);}};number_to_search_for =
```
```
40 ;//
```
```
NOTE: no effect for captured value
```
```
std::cout <<
```
```
"The
```
```
number
```
```
nearest
```
```
to^ "
```
```
<<^
```
```
number_to_search_for <<
```
```
"^ is
```
```
"
```
```
<<^ * find_optimum
```
```
(numbers,
```
```
nearer)
```
```
<<^ std
```
```
::endl;
```
**Allows**^ **all** }

**variables**

**in**^ **the**

**scope**

**of**^ **lambda**

**definition**

**to**^ **be**

**accessed**

**by**^ **value**

```
Please
```
```
enter
```
```
a^ number:
```
```
 20
```
```
The^ number
```
```
nearest
```
```
to^40
```
```
is^18
```
**_Captures the value before and nearest to lambda definition_**

##### Demo


### Capturing by Reference (

### 引用传递

### )

#### [&] (int x, int y) { return x < y; }All^ variables

**in**^ **the**

**enclosing**

**scope**

**are**^ **accessible**

**by**^ **reference**

```
#include
```
```
"Optimum.h"
int main
```
```
()
{ std
```
```
::vector<
```
```
int>^
```
```
numbers{
```
```
 91 ,^
```
```
18 ,^92
```
```
,^22 ,
```
```
 13 ,^
```
```
43 };
```
```
intnumber_to_search_for {};std::cout <<
```
```
"Please
```
```
enter
```
```
a^ number:
```
```
";
```
```
std::cin >>
```
```
number_to_search_for;
auto
```
```
counter{
```
```
[&](
```
```
intx,
```
```
int
```
```
y)^ {^
```
```
++number_to_search_for;
```
```
return
```
```
x < y;}}; find_optimum
```
```
(numbers, counter);
std::cout <<
```
```
"number_to_search_for "
```
```
<<
```
```
number_to_search_for <<
```
```
“,^ minimum
```
```
is^ "
```
```
<<^ * find_optimum
```
```
(numbers,
```
```
counter)
```
```
<<^ std
```
```
::endl;
```
```
}
```
```
Please
```
```
enter
```
```
a^ number:
```
```
 40
```
```
number_to_search_for 45,
minimum
```
```
is^13
```

##### Different variables may be captured together by value or reference[arg1, arg2,...,argn

##### ,&para1,&para2,...,&pram

##### ] () { }

**Capture by**

**value**

**: arg1, arg2, ..., argn**

**Capture by**

**reference**

**: para1, para2, ..., param**

##### Example [=,&count](){} : count captured by

**reference**

**, and others by**

**value[&, count](){}: count captured by**

```
value
, and others by
```
## Capturing Specific Variablesreference


## Capturing

## this

## Pointer

##### Capture

##### this

##### pointer

##### to access all members in a class

```
#ifndef FINDER_H#define FINDER_H#include <vector>#include <optional>class Finder{ public:
```
```
double getNumberTo
```
```
SearchFor() const;
```
void setNumberToSearchFor(double n); **std::optional<double>**

```
findNearest(conststd::vector<double>
```
```
& values) const;
```
```
private:
```
```
double number_to_search_for {};
};#endif // FINDER_H
```
##### Demo


## Capturing

## this

## Pointer

##### The following code causes compiler error Member variable

**_number_to_search_for_**

**cannot be accessed**

**in the lambda expressionCorrect solution is to capture**

```
this
pointer: [this]
```
##### std::optional<

##### double

##### > Finder

```
:: findNearest
```
```
(const
```
```
std::vector<
```
```
double
```
```
>&^ values)
```
```
const
```
```
{
```
```
if(values.
```
```
empty
```
```
())
return
```
##### std::nullopt

```
;
```
```
elsereturn
```
```
* find_optimum
```
```
(values,
```
```
[number_to_search_for]
```
```
(
```
```
double
```
```
x,^ double
```
```
y) {
return
```
```
std::
```
```
abs (x
```
```
 ‐number_to_search_for)
```
```
<^ std
```
```
::
```
```
abs (y
```
```
 ‐number_to_search_for);
});
}
```
**Should**

**be**^ **modified**

**as**^ **[this]**


## Summary

#### What have we learned?Operator overloading

##### Stream operatorAssignment operatorOperator new and deleteFunction Call Operator and function objects (example usage in STL)Lambda expressions


## Exercise

```
2022/5/24
```
#### Mandatory exerciseDownload from Tsinghua Web LearningRead the book “Beginning C++17”Preview Chapter 16: Introduction to Templates (

模板 **)**



