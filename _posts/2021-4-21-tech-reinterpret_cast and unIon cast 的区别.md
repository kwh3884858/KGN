---
layout: post
title: "reinterpret_cast and unIon cast 的区别"
author: "Kong Wei Hang"
categories: tech
tags: [c++]
#image: sonny-boy.jpg
---

```C++
template < typename TO, typename FROM >
inline TO union_cast( FROM value )
{
    union { FROM from; TO to; } convert;
    convert.from = value;
    return convert.to;
}
```

正好在代码中看到一个union_cast的实现，还是第一次见到。
针对这个相当有趣的写法找到了一个相当有趣的回答：

> taken together, this seems pretty clear - these constrain the implementation of pointer reinterpret_cast; the source and destination pointer shall point to the same object (have the same value), unless this is impossible due to alignment requirements. even if they have different values (due to alignment requirements), the union and reinterpret_cast would give identical results.

“源指针和目标指针应指向同一对象（同样的地址，所以具有相同的值），除非由于对齐要求而不可能。
即使它们具有不同的值（由于对齐要求），union和reinterpret_cast也会给出相同的结果。”

这句话的意思是，当int to double时，reinterpret_cast会失败，因为int的字节数量与double不匹配，编译器会抛出错误。
但是union所做的cast会成功,Union会按照最长的成员分配空间，不管int是几个字节，内存依然按照最长的成员double分配空间，转换不会失败。

- 但union_cast或许并不是更好的选择

> Probably, on such computers C++ compiler (in theory) can generate a proper conversion code for reinterpret_cast (but not for unions, of course). A very good compiler is capable to generate a proper run-time check up of a good object alignment (in debug mode, for example) for reinterpret_cast - and so on.

“也许，在这种计算机上，C ++编译器（理论上）可以为reinterpret_cast生成适当的转换代码。一个非常好的编译器能够为reinterpret_cast等生成正确的运行时检查，以检查对象对齐是否正确（例如，在调试模式下）。”



reference: https://www.daniweb.com/programming/software-development/threads/141791/union-vs-reinterpret-cast#post676224

2021.03.24 Edit
今天又遇到这个问题，正好写了一个

```C++
reinterpret_cast<unsigned char>(int);
```

是没有办法通过编译的，编译器会提示没有对应的bit完成转换。

如果只是想进行强转的话，这个类型上的变化可以使用static_cast，当然，肯定会导致数据被截断。
