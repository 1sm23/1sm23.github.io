---
title: new到底干了什么？
date: 2018-12-05 12:56:13
tags:
- javascript
---

1. 创建一个空的简单JavaScript对象（即`{}`）；
2. 链接该对象（设置该对象的**constructor**）到另一个对象 ；
3. 将步骤1新创建的对象作为`this`的上下文 ；
4. 如果该函数没有返回对象，则返回`this`。

