---
title: JavaScript闭包
date: 2020-09-04 20:11:40
tags:
- javascript
- closure
- 闭包
categories:
- javascript
---

### 什么是闭包？

闭包是在外部函数返回后仍能访问其外部函数作用域的函数。这意味着闭包可以记住并访问外部函数的变量和参数，即使函数已经返回。



在深入研究闭包之前，让我们先了解词法作用域。

<!--more-->

#### 什么是词法作用域？

JavaScript中的词法作用域或静态作用域指的是根据变量、函数和对象在源代码中的位置来访问它们。例如:

```javascript
let a = 'global';
  function outer() {
    let b = 'outer';
    function inner() {
      let c = 'inner'
      console.log(c);   // prints 'inner'
      console.log(b);   // prints 'outer'
      console.log(a);   // prints 'global'
    }
    console.log(a);     // prints 'global'
    console.log(b);     // prints 'outer'
    inner();
  }
outer();
console.log(a);         // prints 'global'
```



`inner `函数可以访问定义在他自己的作用域、`outer `函数作用域、全局作用域中定义的变量。`outer `函数可以访问在其自身作用域和全局作用域中定义的变量



### 闭包栗子

#### 例子1

```javascript
function person() {
  let name = 'Peter';
  
  return function displayName() {
    console.log(name);
  };
}
let peter = person();
peter(); // prints 'Peter'
```

在这段代码里，我们调用 `person` 函数返回了一个内部函数 `displayName` 并将该内部函数存储在 `peter` 变量中，当我们调用 `peter`函数（实际上是引用了 `displayName` 函数），控制台打印出了 'Peter'。



但是 `displayName` 函数里没有叫做 `name` 的变量，所以这个函数可以以某种方式访问它的外部函数 `person` 甚至是在它已经执行完之后。所以这个 `displayName` 函数实际上就是一个闭包。



#### 例子2

```javascript
function getCounter() {
  let counter = 0;
  return function() {
    return counter++;
  }
}
let count = getCounter();
console.log(count());  // 0
console.log(count());  // 1
console.log(count());  // 2
```

这次我们把通过 `getCounter` 返回的匿名函数赋值给 `count` 变量，因为 `count` 函数现在是一个闭包，它能在 `getCounter` 函数返回之后访问到 `getCounter` 函数内的 `counter` 变量。



但是⚠️注意，每个 `count` 函数返回的 `counter` 的值并没有按照期望重置到 `0`。



那是因为，每次调用 `count` 函数，一个新的该函数的作用域被创建，但是 `getCounter` 函数只创建了一个作用域，因为 `counter` 变量是在 `getCounter()` 的作用域中定义的，所以它将在每次 `count` 函数调用时递增，而不是重置为 `0`。



### 工作原理？

到目前为止，我们知道了闭包是什么还有了解了几个例子，现在我们来探索JavaScript里的闭包到底是如何工作的。



要真正理解闭包，我们必须立即JavaScript里的两个重要概念，1. 执行上下文 2. 词法环境



#### 执行上下文（Execution Context）

执行上下文是一个当JavaScript被解释执行的时候的一个抽象环境。当全局代码被执行时，他是在全局执行上下文中被执行，当函数被调用时是在函数执行上下文中。



只能有一个运行的执行上下文（因为JavaScript是单线程），它由称为执行栈或调用栈的堆栈数据结构管理。



执行栈是一个采用后进先出的栈，其中items只能从栈顶部添加或者删除。



正在执行的上下文永远是在栈的顶部，当函数运行完之后，它的执行栈会被pop出来，接着执行它下面的执行上下文。



看一下这个代码片段来更好理解执行上下文和栈：



![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gig7x7ngn0j30zm0l00w3.jpg)



当这段代码被执行时，JavaScript引擎创建一个全局执行上下文来执行全局代码，当遇到 `first()` 函数的调用时，它创建一个新的函数执行上下文并把这个上下文压入栈中



![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gig813iluxj303c02i74a.gif)

所以上面代码的执行栈会像是这样：

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gig82c1w7rj30uk06oaau.jpg)



当 `first()` 函数调用完后，它的执行上下文被移出栈，调用栈的当前栈来到它下面的栈也就是全局执行上下文，所以剩下的全局作用域的代码将会被执行。



#### 词法环境（Lexical Environment）

每当JavaScript引擎创建一个执行上下文来执行函数或全局代码时，它还创建一个新的词法环境来存储在该函数执行期间在该函数中定义的变量。



词汇环境是保存标识符变量映射的数据结构。 （这里的标识符是指变量/函数的名称，而变量是对实际对象[包括函数类型对象]或原始值的引用）。



词汇环境有两个组成部分:(1)**环境记录**和(2)**对外部环境的引用**。

1. **环境记录**是变量和函数声明被存储的特定地点
2. **对外部环境的引用**意味着它可以访问到外部（父级）的词法环境，要弄懂闭包是怎么运作的，必须弄懂这个部分。



词法环境在概念上是这样的：

```javascript
lexicalEnvironment = {
  environmentRecord: {
    <identifier> : <value>,
    <identifier> : <value>
  }
  outer: < Reference to the parent lexical environment>
}
```



让我们再来看看刚刚的代码片段：

```javascript
let a = 'Hello World!';
function first() {
  let b = 25;  
  console.log('Inside first function');
}
first();
console.log('Inside global execution context');	
```



当JavaScript引擎创建全局执行上下文来执行全局代码时，它还创建一个新的词法环境来存储在全局作用域中定义的变量和函数。因此全局作用域的词汇环境将是这样的：

```javascript
globalLexicalEnvironment = {
  environmentRecord: {
      a     : 'Hello World!',
      first : < reference to function object >
  }
  outer: null
}
```

这里外部词法环境是 `null` 是因为全局作用域没有外部词法环境。



当引擎给 `first()` 函数创建上下文的时候，它也创建了一个词法环境来存储在执行该函数期间定义的变量，所以这个函数的词法环境看起来会像这样：

```javascript
functionLexicalEnvironment = {
  environmentRecord: {
      b    : 25,
  }
  outer: <globalLexicalEnvironment>
}
```

函数的外部词法环境是全局词法环境是因为这个函数是被全局作用域包裹。



**注意**——当函数执行完成，他的执行上下文会被移出栈，但是它的词法环境可能不会被移出内存！！**这取决于在外部词法环境属性中，函数的词法环境是否被任何其他词法环境引用**。



### 剖析闭包例子

现在我们理解了执行上下文和词法环境，回到闭包。

#### 例子1

```javascript
function person() {
  let name = 'Peter';
  
  return function displayName() {
    console.log(name);
  };
}
let peter = person();
peter(); // prints 'Peter'
```

当 `person` 函数被执行时，JavaScript引擎为这个函数创建了一个执行上下文和词法环境，在函数执行完后，它返回一个 `displayName `函数并且把它赋值给 `peter` 变量。



所以它的词法环境是这样：

```javascript
personLexicalEnvironment = {
  environmentRecord: {
    name : 'Peter',
    displayName: < displayName function reference>
  }
  outer: <globalLexicalEnvironment>
}
```

当 `person` 函数执行完后，它的执行上下文被移出栈，但是他的词法环境依然还在内存里，因为它词法环境被它内部的 `displayName` 函数的词法环境引用，所以它( `person` 函数)的变量依然还在内存里。



当 `personLexicalEnvironment `被创建，js引擎会把 `personLexicalEnvironment` 附加到所有在这个词法环境中定义的函数中，所以之后有任何内部函数被调用时，js引擎会把外部词法环境设置成函数定义时附加上的那个。



当 `peter` 函数被执行（实际上是 `displayName` 函数的一个引用），js引擎为它创建了一个新的执行上下文和词法环境。



所以它的词法环境是这样：

```javascript
displayNameLexicalEnvironment = {
  environmentRecord: {
    
  }
  outer: <personLexicalEnvironment>
}
```

因为在 `displayName` 函数里没有变量，它的环境记录是空的。在这个函数的执行期间，js引擎会在这个函数的词法环境里查找变量 `name`。



因为在 `displayName` 函数的词法环境里没有变量，js引擎会在外部环境查找，也就是仍然存储在内存里的 `person` 函数的词法环境。js引擎找到变量 `name` 然后打印在控制台中。

#### 例子2

```javascript
function getCounter() {
  let counter = 0;
  return function() {
    return counter++;
  }
}
let count = getCounter();
console.log(count());  // 0
console.log(count());  // 1
console.log(count());  // 2
```



同样的，`getCounter `函数的词法环境：

```javascript
getCounterLexicalEnvironment = {
  environmentRecord: {
    counter: 0,
    <anonymous function> : < reference to function>
  }
  outer: <globalLexicalEnvironment>
}
```

这个函数返回了一个匿名函数赋值给了 `count` 变量。



当 `count` 函数被执行时，它的词法环境:

```javascript
countLexicalEnvironment = {
  environmentRecord: {
  
  }
  outer: <getCountLexicalEnvironment>
}
```

当 `count` 函数被调用，js引擎会在这个函数的词法环境里查找 `counter` 变量，同样的它的环境记录是空的，引擎会从函数的外部词法环境里查找。



引擎找到变量，打印在控制台上然后在 `getCounter` 函数词法环境里自增 `counter` 变量。



在第一次调用 `count` 函数后，`getCounter `函数的词法环境：

```javascript
getCounterLexicalEnvironment = {
  environmentRecord: {
    counter: 1,
    <anonymous function> : < reference to function>
  }
  outer: <globalLexicalEnvironment>
}
```



每次调用 `count` 函数，js引擎创建一个新的 `count` 函数的词法环境，自增 `counter` 变量然后更新 `getCounter` 函数的词法环境。