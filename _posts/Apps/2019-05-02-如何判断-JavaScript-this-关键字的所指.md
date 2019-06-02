## `this` 是什么

在 Javascript 中, 当一个函数被调用, 一个称为执行环境 (execution context) 的活动记录会被创建. 这个记录包含函数是在调用栈 (call-stack) 的何处被调用的, 如何被调用的, 被传递了什么参数等信息. 这其中就包括 `this` 引用的记录, 程序可以在函数执行期间使用这个 this 引用.

## Call-site

为了理解 `this` 绑定, 我们首先需要了解调用点: Call-site 是指函数调用的位置（而不是函数声明的位置）.
定位调用点的时候我们要考虑调用栈 (call-stack), 这个调用栈是指程序执行到目前位置时所调用的函数的堆栈. 我们所关心的调用点位于调用栈中当前执行函数位置的前面一个位置.

考虑下面这个例子:

```js
function baz() {
  console.log( "baz" );
  bar();
}

function bar() {
  console.log( "bar" );
  foo();
}

function foo() {
  console.log( "foo" );
}

baz();
```

上面的代码片段声明了 3 个函数, 首先是 `baz` 在全局作用域被调用, 然后 `baz` 函数执行过程中调用 `bar` 函数, 然后再是 `foo` 函数在执行 `bar` 函数时被调用. 所以上述代码片段的调用栈是 `baz` -> `bar` -> `foo`. `foo` 的调用点就在 `bar` 中, `bar` 的调用点就在 `baz` 中, 而 `baz` 的调用点在全局作用域中.

现代浏览器如 Chrome 有内置的 Javascript 调试工具, 上述代码片段为例, 我们可以在 `foo` 函数第一行设置一个断点, 或简单插入一个 `debugger;` 语句来检查代码调用栈.

![screenshot 2019-05-02 at 4.40.18 PM](https://i.imgur.com/itXVnoC.png)

可以从上图中 Call Stack 给出了代码执行到 `foo` 的第一行, 所调用的函数的序列, 从顶部往下数第二个就是 `foo` 的 call-site 所在的位置: `bar` 函数中.

## `this` 绑定判断规则

一共有四条规则用于判断代码执行时的 `this` 所指, 我们需要检查代码找到函数的调用点, 然后判断哪条规则试用. 如果同时有不止一条规则可以应用于某个调用点, 那么需要根据 4 条规则的优先顺序判断究竟那一条适用.

### 默认绑定

可以将这条规则看作是其它规则都不试用时的默认囊括规则. 

```js
function foo() {
	console.log( this.a );
}

var a = 2;

foo(); // 2
```

首先需要注意的是, 定义在全局作用域的变量, 同时也是全局对象 (globe-object) 的属性之一, 也就是所 `var a = 2` 和 `window.a = 2;` 是一个意思, 他们是等同的.

上面的代码中, 当 `foo` 被调用时, `this.a` 被解析为全局作用域中的变量 `a`, 因为, 在这里 `this` *默认绑定*应用于了函数调用, 所以 `this` 被指向了全局对象. 

为什么*默认绑定*会应用于上面的代码呢? 我们检查 `foo` 的调用点, 可以看到它的调用非常简单, 没有任何修饰, 没有其它规则可以应用于这个调用, 所以*默认绑定*生效.  

如果 `strict mode` 有生效, 那么*默认绑定*的 `this` 无法指向全局变量, 所以 `this` 的值被设为 `undefined`.

```js
function foo() {
	"use strict";
	
	console.log( this.a );
}

var a = 2;

foo(); // TypeError: `this` is `undefined`
```

一个微小但是重要的细节: 只有 `foo` 函数的内部代码在 `strict mode` 下执行时候, `this` 所指才会被设置为 `undefined`, 而跟 `foo` 函数调用点中的 `strict mode` 状态无关.

```js
function foo() {
	console.log( this.a );
}

var a = 2;

(function(){
	"use strict";

	foo(); // 2
})();
```

如上图, `foo` 的调用点代码处于 `strict mode` 下, 但是并不影响 `foo` 函数中的 `this` 解析为全局对象, `this.a` 解析为 2.

### 间接绑定 (Implicit Binding)

关于间接绑定, 我们需要检查函数的调用点是否有一个环境对象 (context object), 或者说所属或包含对象. 

```js
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

obj.foo(); // 2
```

上面的代码片段中, `foo` 在全局作用域中定义, 之后作为一个引用属性添加到了 `obj` 中, 当 `foo()` 被调用的时候, 它有个引用前缀指向 `obj`.

当函数的引用有一个背景对象时候, *间接绑定*的规则应用于函数调用, 将函数中的 `this` 指向这个背景对象. 所以上述代码片段中, `this.a` 解析为了 `obj.a` 也就是 2.

*间接绑定*时只有对象属性索引链的最后/近的一层需要考虑. 

```js
function foo() {
	console.log( this.a );
}

var obj2 = {
	a: 42,
	foo: foo
};

var obj1 = {
	a: 2,
	obj2: obj2
};

obj1.obj2.foo(); // 42
```

#### 间接绑定丢失

`this` 绑定中最常发生的一个情况是*间接绑定*了的函数失去了这个绑定对象, 这通常意味着*默认绑定*规则取而代之. `this` 解析为全局对象或 `undefined`, 具体取决于 `strict mode` 的状态.

```js
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

var bar = obj.foo; // function reference/alias!

var a = "oops, global"; // `a` also property on global object

bar(); // "oops, global"
```

尽管 `bar` 看起来是 `obj.foo` 的一个引用, 实际上, 它只不过是对 foo 函数的另一个直接引用. `foo` 函数的调用点, 也就是 `bar()`, 本身是一个简单的, 无修饰的调用, 所以*默认绑定*规则引用于此.

*间接绑定*丢失的一个更为微妙, 常见和出乎预料的方式是当将函数作为回调函数传递给其它函数的时候.

```js
function foo() {
	console.log( this.a );
}

function doFoo(fn) {
	// `fn` is just another reference to `foo`

	fn(); // <-- call-site!
}

var obj = {
	a: 2,
	foo: foo
};

var a = "oops, global"; // `a` also property on global object

doFoo( obj.foo ); // "oops, global"
```

参数传递本质上就是一个间接赋值操作, 相当于 `fn = obj.foo`, 和先前一个例子没什么不同.

如果我们传递回调函数的对象是 JavaScript 内置函数呢? 结果也是一样的.

```js
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2,
	foo: foo
};

var a = "oops, global"; // `a` also property on global object

setTimeout( obj.foo, 100 ); // "oops, global"
```

可以假设内置的 `setTimeout` 的实现过程为如下伪码:

```js
function setTimeout(fn,delay) {
	// wait (somehow) for `delay` milliseconds
	fn(); // <-- call-site!
}
```

可以看到内部其实也是一个函数引用的间接赋值过程.
 
### 直接绑定 (Explicit Binding)

从上面可以看到, *间接绑定*的实现方式是在环境对象中包含一个函数的引用属性, 然后通过这个引用属性调用函数.

如果我们不希望修改某个对象就绑定 `this` 所指为该对象, 即不在其中增加一个函数索引属性呢?

JavaScript 中的函数大都会有的 `call()`, `apply()` 使用程序可以用于我们的目的, 来达到*直接绑定*的效果.

`call()` 和 `apply()` 的第一个参数都需要一个对象作为 `this` 的值, 然后使用这个指定的 this 值调用函数. 因为它明确的指出了希望作为函数 `this` 值的对象, 所以称之为 *explicit binding*.

例如: 

```js
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2
};

foo.call( obj ); // 2
```

上面代码中, 通过 `foo.call(..)` 调用函数允许我们强制 `this` 所指为 `obj`.

但是当我们使用 call 和 apply 的时候, 同时也是在调用底层函数, 所以单纯使用 call 和 apply 并不能解决上面遇到的函数作为参数传递过程中 `this` 绑定丢失的问题. 

#### 硬绑定 (Hard Binding)

一个有少许不同的模式提供了解决办法. 

```js
function foo() {
	console.log( this.a );
}

var obj = {
	a: 2
};

var bar = function() {
	foo.call( obj ); // 内部实现使用了直接绑定
};

bar(); // 2
setTimeout( bar, 100 ); // 2

// `bar` 将 `foo` `this` 硬绑定到了 `obj`, 这个绑定不可被覆盖
bar.call( window ); // 2
```

上面的代码中我们创建了一个函数 `bar`, 在这个函数的内部实现中应用了 `foo.call(obj)`, 从而强制性的将 `obj` 设为了 `foo` 的 `this` 然后运行了函数 `foo`. 不管之后怎样调用函数 `bar`, 它总会将 `obj` 绑定为 `foo` 的 `this`, 再运行 `foo`. 这种绑定即直接又强力, 所以我们称之为 *硬绑定* (hard binding).

因为硬绑定是一个非常常见的模式, 因此在 ES5 中提供了一个相应的内置工具: `Function.prototype.bind`. 以下是一个使用该函数的例子:

```js
function foo(something) {
	console.log( this.a, something );
	return this.a + something;
}

var obj = {
	a: 2
};

var bar = foo.bind( obj );

var b = bar( 3 ); // 2 3
console.log( b ); // 5
``` 

调用 `bind(..)` 函数后会返回一个新的函数, 这个新函数原始函数的 `this` 绑定设置为了参数中提供的对象.

### new 绑定

考虑以下代码:

```js
function foo(a) {
	this.a = a;
}

var bar = new foo( 2 );
console.log( bar.a ); // 2
```

通过使用 `new` 关键字调用 `foo(..)`, 我们创建了一个新的对象, 并且将这个新的对象绑定为了 `foo` 函数的 `this`. `new` 是最后一个函数调用时进行 `this` 绑定的方式, 我们称之为 *new 绑定*.

## 绑定规则的优先级顺序

现在我们已经讨论了函数调用时 `this` 绑定的所有 4 条规则. 我们需要做的就是找到调用点 (call-site), 然后看哪条规则适用. 但是, 如果一个函数的调用点有多条规则适用呢? 所以这四条规则一定会有一个优先级顺序, 接下来我们会加以论证.

首先, *默认绑定* (default binding) 是优先级最低的一条规则, 这个无需讨论.

那么, *间接绑定* (implicit binding) 和*直接绑定* (explicit binding) 谁的优先级更高呢? 我们使用以下例子来说明:

```js
function foo() {
	console.log( this.a );
}

var obj1 = {
	a: 2,
	foo: foo
};

var obj2 = {
	a: 3,
	foo: foo
};

obj1.foo(); // 2
obj2.foo(); // 3

obj1.foo.call( obj2 ); // 3
obj2.foo.call( obj1 ); // 2
```

因此, *直接绑定*比*间接绑定*的优先级更高, 所以在判断*间接绑定*规则是否应用时需要先检查*直接绑定*规则是否有应用.

接下来只需要分析 *new 绑定*在先后顺序中的位置了. 

```js
function foo(something) {
	this.a = something;
}

var obj1 = {
	foo: foo
};

var obj2 = {};

obj1.foo( 2 );
console.log( obj1.a ); // 2

obj1.foo.call( obj2, 3 );
console.log( obj2.a ); // 3

var bar = new obj1.foo( 4 );
console.log( obj1.a ); // 2
console.log( bar.a ); // 4
```

根据上述代码可以判断 *new 绑定*比*间接绑定*优先级更高. 

需要注意的是, `new` 和 `call`/`apply` 不能一起使用, 所以不能用 `new foo.call(obj1)` 来直接测试二者的优先级顺序, 但是我们仍然可以使用*硬绑定*来进行测试.

```js
function foo(something) {
	this.a = something;
}

var obj1 = {};

var bar = foo.bind( obj1 );
bar( 2 );
console.log( obj1.a ); // 2

var baz = new bar( 3 );
console.log( obj1.a ); // 2
console.log( baz.a ); // 3
```

从上面代码中可已看到, 尽管 `obj1` 硬绑定为了 `bar` 的 `this`, 但 `new bar(3)` 并没有将 `obj1.a` 的值更改为 `3`. 相反, *硬绑定*后的 `bar` 函数调用能够被 `new` 覆盖. 因为应用 `new` 的关系, 我们得到了一个新创建的对象, `baz`. 我们可以看到实际上 `baz.a` 的值被设置为了 3.

## 判断 `this`

现在我们总结下根据函数的调用点, 以及考虑优先级后判定 `this` 的规则. 按顺序依次询问以下问题, 在遇到头一条符合情况的规则后就停下.

1. 函数是使用 `new` 关键字调用的么 (*new 绑定*)? 如果是, `this` 就是新创建的对象.

    `var bar = new foo()`
    
2. 函数是使用 `call` 或 `apply` 调用的么 (*直接绑定*), 抑或是 `bind` *硬绑定*?  如果是, `this` 是明确指明的那个对象.

    `var bar = foo.call( obj2 )`

3. 函数是在有背景对象的情况下调用的么 (*间接绑定*)? 如果是, `this` 是那个背景对象.
 
    `var bar = obj1.foo()`
    
4. 以上规则都不适用的话, `this` 是默认值 (*默认绑定*). 如果在 `strict mode` 下, 选择 `undefined`, 否则选择 `global` 对象.

    `var bar = foo()`
    
<hr>
**注**: 本文参考自 Github [@getify](https://github.com/getify) 书本系列 [You Don't know JS](https://github.com/getify/You-Dont-Know-JS) **`this` & Object Prototypes** 第二章 [this All Makes Sense Now!](https://github.com/getify/You-Dont-Know-JS/blob/master/this%20%26%20object%20prototypes/ch2.md)