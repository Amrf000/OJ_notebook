---
layout: post
title: Qt learning Lesson 3 Signal and slot expansion
category: qt5
tags: [qt5]
---
# 

## 

##### 

### Qt learning Lesson 3: Signal and slot expansion

Qt signals and slots more than the amount of content one, as well as to expand the section.

### 1\. The signal parameters can be transferred with the slot function

Now define the slot and the write signal overloaded,

![](/md_blog/public/assets/2021-07-25/2ad7185e5d71c4e81e9c8845e08a068c.png)

![](/md_blog/public/assets/2021-07-25/c5c93ea7db70eeb127dfe0c6451daca6.png)

Signals do not realize, slot function must be implemented.

![](/md_blog/public/assets/2021-07-25/53090401e9587f6a6819350c69f65004.png)

After the signal and function declarations and implement tank, went to the window class object calls

In this case, in order to use or there is no reference signal and the reference slot assignment need to use a function pointer, the following format:

Function pointer -\> function address  
void(\*p)(QString) =  &Teacher::hungry

Now we have to call the reference signals and slots:

![](/md_blog/public/assets/2021-07-25/2f608c2834604938794da0f4203949cf.png)

### 2\. Other extensions

2.1 custom signal slot Notes

1. The sender and recipient need be QObject subclass (of course, except for the slot function is a global function, Lambda expression or the like when the recipient without);
2. Signal and the slot function return value is void
3. Signal only needs to declare no need to implement
4. Slot function need to declare the need to achieve
5. Slot function is an ordinary member functions, member functions, will be public, private, protected the influence;
6. At proper positions of the transmission signal using EMIT;
7. Using the connect () function and groove connection signal.
8. Any member functions, static function, global function and Lambda expressions can be used as a function of the slot
9. Request signal and groove signal parameters consistent groove sistency, is the same parameter type.
10. If not the parameter signals and grooves, where the context allows that the slot function parameters is less than the signal may, even so, the order of those parameters must also be a function of the presence of groove signals and several front into line. This is because you can choose to ignore the signals coming from the data in the slot function (that is, the parameters of the slot function is less than the signal).

2.2 groove extended signal

1. A plurality of grooves and a signal may be connected

If this is the case, these slots will be called one by one, but theirCall to order is uncertain.

2\. A plurality of signals can be connected to a tank

As long as any one of the signal is issued, this slot will be called。

3\. A signal may be connected to the other signal

When a signal is sent first, a second signal is emitted. In addition, such a signal - signal and form - the form of a groove is no different.

4\. The groove may be unlink

This situation is not often, becauseWhen an object delete, Qt automatically cancels all connected to the groove above the object。

The groove may disconnect signal

usedisconnectKeywords can disconnect signal slot

6\. Use Lambda Expressions

When using Qt 5, the compiler can support Qt 5 is supported by Lambda expressions.

When the connection signal and grooves, the grooves may be processed using the function mode Lambda expressions. Later we will detail what is Lambda expressions

### 3.Qt4 written version of the signal slot

connect(zt,SIGNAL(hungry(QString)),st,SLOT(treat(QString)));

This usesSIGNAL and SLOT these macros, function names will be converted into two strings. Noted that the connect () signal and slot are function takes a string, if a connector unsuccessful appear, Qt4 is no compilation errors (because all are strings, compile-time checking whether the string is not matched), and It was given an error at runtime. This will undoubtedly increase the instability of the program.

Qt5 fully compatible with Qt4 on grammar, and vice versa is not possible.

### 4\. Lambda Expressions

C ++ 11 in Lambda expressionsUsed to define and create an anonymous function objectsTo simplify programming. First look at the basic structure of Lambda expressions:

\[capture\](parameters) mutable -\>return-type

{

statement

}

\[Object function parameters\] (operator overloading function parameters) mutable -\> body of the return value of the function {}

4.1 function object parameters:

\[\], Identified aLambda startThis part must be present,Can not be omitted. Parameters passed to the function object constructor function object class compiler automatically generated. Parameter function object that can only be used to define the visible range where the effect of the time until the Lambda Lambda local variables (including where this class Lambda). Function object parameter has the following form:

1. air. We did not use any function object parameter.
2. =. In vivo function you can use all the range of visible effect local variables where Lambda (Lambda including this class are located), and isPassed by value(Equivalent to compiler automatically passed by value of all local variables for us).
3. &. In vivo function you can use all the range of visible effect local variables where Lambda (Lambda including this class are located), and isReference transfer mode(Equivalent to compiler automatically as we passed by reference all local variables).
4. this. In vivo function Lambda class member variables can be used where the.
5. a. A will be passed by value. When passed by value, the body can not function to modify a copy of the passed in as default function is a const.To modify a copy of the passedYou can add mutable modifier.
6. & A. It will be passed by a reference.
7. a, & b. Will be passed by value a, b passed by reference.
8. =, & A, & b. In addition to a and b are passed by reference, other parameters are passed by value.
9. &, A, b. In addition to a and b are passed by value, other parameters are passed by reference.

4.2 operator overloading function parameters

Parameter () operator identification overloaded, no argument, this part may be omitted. The value of the parameter by pressing (such as: (a, b)), and by reference (such as: (& a, & b)) is transmitted in two ways.

4.3 editable identifier

mutable statement, this part can be omitted. When the transfer function by value object parameter and, with the mutable modifiers may be modified copy of the passed by value (note the copy can be modified, rather than the values ​​themselves).

4.4 function return value

-\> return type, identifies the type of return value of the function, when the return value void, or function of the body, only a local return (in this case the compiler can automatically infer that the type of return value), this section may be omitted.

4.5 function body

{}, To achieve identification function, this part can not be omitted, but the function thereof can be empty.

Example of use:

![](/md_blog/public/assets/2021-07-25/c9567866386a357d19c561f2858cbf41.png)