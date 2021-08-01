---
title: TypeScript关键字 is
date: 2021-06-02 20:48:37
tags:
- TypeScript
- TypeScript keyword
- is
---

可以先去看一下[官方定义的例子](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates)。

<!-- language: typescript -->

```typescript
function isString(test: any): test is string{
    return typeof test === "string";
}

function example(foo: any){
	if(isString(foo)){
		console.log("it is a string" + foo);
		console.log(foo.length); // string function
    }
}
example("hello world");
```

使用上述格式的类型预测 `test is string` （而不是定义返回类型为 `boolean`）在 `isString()` 被调用后，如果函数返回 `true`, **TypeScript将在调用该函数的任何块级作用域中将类型缩小为string。**编译器会认为 `foo` 是该作用域中的 `string` 类型（并且只在该作用域中）。

上述 `isString` 被称为 `Type Guard` 函数，其中返回必须使用 `test is string`称为 `Type Predicate`限制。

<!--more-->

<!-- language: typescript -->

```typescript
{
    console.log("it is a string" + foo);
		console.log(foo.length); // string function
}
```

类型断言只在编译时起作用，编译结果的 `.js` 文件（运行时）没有任何区别，因为没有考虑到类型。

我将在下面的四个示例中说明它们之间的差异。

示例1: 

上面的示例代码不会有编译错误和运行错误。

示例2: 

下面的示例会有编译错误（同时会运行报错），因为 TypeScript 已经把类型缩小到了 `string` 并且检查到 `string` 类型上没有 `isInteger` 方法。

<!-- language: typescript -->

```typescript
function example(foo: any){
	if(isString(foo)){
		console.log("it is a string" + foo);
		console.log(foo.length);
		console.log(foo.isInteger());
    }
}
```

示例3: 

下面的代码不会有编译错误但是在运行时报错，因为 TypeScript 只会在作用域里限制类型为 `string` ，所以  `foo.isInteger` 会报错（TypeScript 不知道它是一个 `string` 类型），然而在运行时，`string` 类型没有 `isInteger` 方法，所以有运行时错误。

<!-- language: typescript -->

```typescript
function example(foo: any){
	if(isString(foo)){
		console.log("it is a string" + foo);
		console.log(foo.length);
    }
    console.log(foo.isInteger());
}
```

示例4: 

如果不用 `test is string` （类型预测），TypeScript不会缩小作用域里的类型，下面的示例代码不会有编译错误，但会有运行时错误。

<!-- language: typescript -->

```typescript
function isString(test: any): boolean{
	return typeof test === "string";
}
function example(foo: any){
	if(isString(foo)){
		console.log("it is a string" + foo);
		console.log(foo.length);
		console.log(foo.isInteger(2));
    }
}
```

结论就是 `test is string` （类型预测）用来在编译时告诉开发者代码是否会有运行时错误。对于 JavaScript 来说，开发者在编译时不会知道是否有错误。这就是 TypeScript 的优势。
