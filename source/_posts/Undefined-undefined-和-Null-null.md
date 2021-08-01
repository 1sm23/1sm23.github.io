---
title: Undefined undefined 和 Null null
date: 2021-03-12 12:36:03
tags:
- javascript
- JavaScript数据类型
---

根据最新的ECMAscript标准，JavaScript里有9种类型：

- 其中6种可以通过`typeof`来检测的原始类型（Primitive）
  - undefined
  - Boolean
  - Number
  - String
  - BigInt
  - Symbol

  <!--more-->

- 结构化类型（Structural Types）
  - Object
  - Function

- 结构化根原始类型（Structural Root Primitive）
  - null 特殊的原始类型，其值有额外的用途:如果对象不被继承，则显示null。



其中在面试中被考察到最多的就是 undefined 和 null 的区别。根据 mdn 定义，刚声明的变量和没有值的形式参数会被分配一个 undefined。而 null 虽然在JavaScript中也是一个原始值（primitive），所有的对象都由他派生（derive）而来，在使用`typeof`操作符会返回`object`。

> typeof null === 'object' 	//  true

所以，他们的

#### 共同点：

1. 都是原始类型。
2. 都只有一个值，undefined 为 undefined ，null 为 null。

#### 不同点：

1. 含义完全不同
2. undefined 可以使用`typeof`检测，而 null 不能。