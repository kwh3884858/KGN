---
layout: post
title: "LNK2019 的一种情况，需要限定友元所作用的实例化"
author: "Kong Wei Hang"
categories: tech
tags: [Windows Programming]
#image: sonny-boy.jpg
---

- 可以在任何地方建立RC文件

- 如果建立的RC文件没有在Properties中设置为Included In Project的话，Instance中是不会包含这个文件的

- Resource.h是VS会默认使用的方式，也就是通过宏定义一个ID，并通过ID找到RC文件中对应的文件名

- 资产需要和RC文件呆在同一个文件夹下

- 所以在调用的地方使用MAKEINTRESOURCE(MACRO)
