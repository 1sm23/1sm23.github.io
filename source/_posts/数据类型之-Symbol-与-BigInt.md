---
title: 数据类型之 Symbol 与 BigInt
date: 2021-04-27 19:29:08
hidden: true
tags:
- JavaScript数据类型
- Symbol
- BigInt
---

#### Symbol

##### 定义

[Symbol](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol) 是和像 [Number](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number) 、[String](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String) 、 [Boolean](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Boolean)  一样的新的基本数据类型（[primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)），它的值代表的是一个独一无二的值，内部你可以认为它是一个像 `129023875892375` 一样的一个长数字来确保独一无二，通常用在一些需要避免名字冲突的地方，比如对象属性的键名，这也是它被设计出来的唯一目的。



不像Number 、 String 、 Boolean ：

```javascript
'123' // String
123 // Number
true // Boolean
```

Symbol 并没有字面量的快捷创建方式，如果你想创建一个 Symbol 值，只能使用 `Symbol()`的方式：

```javascript
var sym = new Symbol()
```

Symbol() 每次创建的值是不一样的：

 ```javascript
 const sym1 = new Symbol();
 const sym2 = new Symbol();
 sym1 === sym2  // false
 ```

在创建 Symbol 的时候你可以选择性的传入描述（description）:

```javascript
new Symbol('asdasd')

但这只是一个为了方便调试的文本描述，不会对产生的值有任何的影响：

​```javascript
const sym1 = new Symbol('apple');
const sym2 = new Symbol('apple');
sym1 === sym2  // false
```

但你还是可以传入这些描述，console 里打印 Symbol 能看到描述值：

![](https://tva1.sinaimg.cn/large/008i3skNgy1gq1io1ho12j30ic08ot9a.jpg)



##### 用法

1. 在往对象上添加属性时避免属性重复：

```javascript
let user = {
  // ...
}
user.id = 4749;
```

展开 `user` 我们发现 `user` 里早就有 `id` 这个属性了：

```javascript
let user = {
  id:1234,
  name:'Johnathan',
  city:'Yunnan',
  age:32
}
```

这样继续添加 `id` 会导致之前的 `id` 会被覆盖，这时候可以使用 Symbol() ：

```javascript
const idSym = Symbol('id');
user[idSym] = 1231;
```



<center>    <img style="border-radius: 0.3125em;    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);"     src="https://tva1.sinaimg.cn/large/008i3skNgy1gq8j7s5ed8j30te0jsgo3.jpg">    <br>    <div style="color:orange; border-bottom: 1px solid #d9d9d9;    display: inline-block;    color: #999;    padding: 2px;">实际效果</div> </center>



对象里的 symbol 属性是私密的，意思是用 `Object.getOwnPropertyNames()`获取对象属性名的时候不能获取 symbol：

```javascript
const idSym = Symbol('id');
let user = {
  id:1234,
  [idSym]:159348,
  name:'Johnathan',
  city:'Yunnan',
  age:32
}
console.log(Object.getOwnPropertyNames(user));		// ["id", "name", "city", "age"]
```

但又不是完全无法获取，用 `` 