---
layout: post
title: Lesson 62 Singleton Template
category: qt5
tags: [qt5]
---
# 

1\. Requirements  
In architecture design, certain classes can only have at most one object in the entire system life cycle. How to define a class so that this class can only create at most one object. ?  
![ ](/public/assets/2021-07-25/ef8d9e59ca4f862f1e8c7672521be0f1.png)Case study 1; preliminary exploration of singleton mode
    
    #include <iostream> #include <string> using namespace std; class SObject { static SObject* c_instance; SObject(const SObject&); SObject& operator= (const SObject&); SObject() { } public: static SObject* GetInstance(); void print() { cout << "this = " << this << endl; } }; SObject* SObject::c_instance = NULL; SObject* SObject::GetInstance() { if( c_instance == NULL ) { c_instance = new SObject(); } return c_instance; } int main() { SObject* s = SObject::GetInstance(); SObject* s1 = SObject::GetInstance(); SObject* s2 = SObject::GetInstance(); s->print(); s1->print(); s2->print(); return 0; } this = 0xbb15b0 this = 0xbb15b0 this = 0xbb15b0 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

* 8

* 9

* 10

* 11

* 12

* 13

* 14

* 15

* 16

* 17

* 18

* 19

* 20

* 21

* 22

* 23

* 24

* 25

* 26

* 27

* 28

* 29

* 30

* 31

* 32

* 33

* 34

* 35

* 36

* 37

* 38

* 39

* 40

* 41

* 42

* 43

* 44

* 45

* 46

* 47

* 48

* 49

* 50

* 51

* 52

2\. Existing problems  
When singleton mode is needed, the static member variable c\_instance must be defined  
The static member function GetInstance() must be defined;

solution:  
Extract the code related to the singleton pattern and develop the singleton template. When a singleton class is needed, use the singleton template directly.

Case study 2: singleton template
    
    #include <iostream> #include <string> #include "Singleton.h" using namespace std; class SObject { friend class Singleton<SObject>; // The current class needs to use singleton mode SObject(const SObject&); SObject& operator= (const SObject&); SObject() { } public: void print() { cout << "this = " << this << endl; } }; int main() { SObject* s = Singleton<SObject>::GetInstance(); SObject* s1 = Singleton<SObject>::GetInstance(); SObject* s2 = Singleton<SObject>::GetInstance(); s->print(); s1->print(); s2->print(); return 0; } 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

* 8

* 9

* 10

* 11

* 12

* 13

* 14

* 15

* 16

* 17

* 18

* 19

* 20

* 21

* 22

* 23

* 24

* 25

* 26

* 27

* 28

* 29

* 30

* 31

* 32

* 33

* 34

* 35

* 36

* 37

     #ifndef _SINGLETON_H_ #define _SINGLETON_H_ template < typename T > class Singleton { static T* c_instance; public: static T* GetInstance(); }; template < typename T > T* Singleton<T>::c_instance = NULL; template < typename T > T* Singleton<T>::GetInstance() { if( c_instance == NULL ) { c_instance = new T(); } return c_instance; } #endif 
    

* 1

* 2

* 3

* 4

* 5

* 6

* 7

* 8

* 9

* 10

* 11

* 12

* 13

* 14

* 15

* 16

* 17

* 18

* 19

* 20

* 21

* 22

* 23

* 24

* 25

* 26

* 27

* 28

* 29

* 30

* 31

to sum up:  
The singleton pattern is one of the most commonly used design patterns in development  
The application of singleton mode makes a class only have one object at most  
can abstract the code related to the singleton pattern into a class template  
The class that needs to use the singleton mode directly uses the singleton template.