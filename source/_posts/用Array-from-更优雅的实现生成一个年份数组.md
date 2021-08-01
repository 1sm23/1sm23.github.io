---
title: 用Array.from()更优雅的实现生成一个年份数组
date: 2020-11-01 20:20:27
tags:
hidden: true
- Array.from
- javascript
categories:
- javascript
---

相关：[Array.from()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
原项目

```javascript
 for (let i = 1900; i < 2030; i++) {
   		this.columns.push(i)
   }
```

改造后

```javascript
this.columns = Array.from({ length: 2030 - 1900 }, (undefined, index) => return 1900 + index);
```

`Array.from()`的第一个参数是一个类数组或可迭代对象。类数组是一个具有`length`属性的对象；具体可迭代对象参考[Iterable object](https://zh.javascript.info/iterable)

