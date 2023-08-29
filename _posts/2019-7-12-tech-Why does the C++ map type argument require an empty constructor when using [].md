---
layout: post
title: "Why does the C++ map type argument require an empty constructor when using [].md"
author: "Kong Wei Hang"
categories: tech
tags: [C++]
#image: sonny-boy.jpg
---


Link to StackOverflow: Why does the C++ map type argument require an empty constructor when using [] by Nick Bolton?


## Q:
Not a major issue, just annoying as I don't want my class to ever be instantiated without the particular arguments.

``` C++
#include <map>

struct MyClass
{
    MyClass(int t);
};

int main() {
    std::map<int, MyClass> myMap;
    myMap[14] = MyClass(42);
}

```

This gives me the following g++ error:

```C++
/usr/include/c++/4.3/bits/stl_map.h:419: error: no matching function for call to ‘MyClass()’
```

This compiles fine if I add a default constructor; I am certain it's not caused by incorrect syntax.

PS: This problem also causes an error: 

```C++
C++ Compiler Error C2280 “attempting to reference a deleted function” 
```

in Visual Studio 2013 and 2015.

## A:

This issue comes with operator[]. Quote from SGI documentation:

> data_type& operator[](const key_type& k) - Returns a reference to the object that is associated with a particular key. If the map does not already contain such an object, operator[] inserts the default object  data_type().

If you don't have default constructor you can use insert/find functions. Following example works fine:

```C++
myMap.insert( std::map< int, MyClass >::value_type ( 1, MyClass(1) ) );

myMap.find( 1 )->second;

```