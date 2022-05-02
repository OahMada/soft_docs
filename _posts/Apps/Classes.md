## class keyword
`class` keyword identifies a block where the contents define the members of a function's prototype:

```js
class Foo {
	constructor(a,b) {
		this.x = a;
		this.y = b;
	}

	gimmeXY() {
		return this.x * this.y;
	}
	*generator() {
	}
	get getter() {
	}
	set setter() {
	}
}
```

* `class Foo` implies creating a (special) function of the name Foo, much like you did pre-ES6.
* `constructor(..)` identifies the signature of that Foo(..) function, as well as its body contents.
* Class methods use the same "concise method" syntax available to object literals. This also includes the concise generator form as well as the ES5 getter/setter syntax. However, class methods are non-enumerable whereas object methods are by default enumerable.
* Unlike object literals, there are no commas separating members in a class body! In fact, they're not even allowed.

To instantiate a class:

```js
var f = new Foo( 5, 15 );

f.x;						// 5
f.y;						// 15
f.gimmeXY();				// 75
```

* A `Foo(..)` call of `class Foo` must be made with `new`
* `class Foo` is not hoisted; the `extends ..` clause specifies an expression that cannot be "hoisted." So, you must declare a `class` before you can instantiate it.
* `class Foo` in the top global scope creates a lexical Foo identifier in that scope, but does not create a global object property of that name.

The established `instanceof` operator still works with ES6 classes, because class just creates a constructor function of the same name.

Another way of thinking about `class`, is as a macro that is used to automatically populate a `prototype` object. Optionally, it also wires up the `[[Prototype]]` relationship if using `extends`.

In addition to the declaration form, a class can also be an expression, as in: `var x = class Y { .. }`.

## `extends` and `super`

ES6 classes also have syntactic sugar for establishing the `[[Prototype]]` delegation link between two function prototypes using the class-oriented familiar terminology `extends`:

```js
class Bar extends Foo {
	constructor(a,b,c) {
		super( a, b );
		this.z = c;
	}

	gimmeXYZ() {
		return super.gimmeXY() * this.z;
	}
}

var b = new Bar( 5, 15, 25 );

b.x;						// 5
b.y;						// 15
b.z;						// 25
b.gimmeXYZ();				// 1875
```

In the constructor, `super` automatically refers to the "parent constructor," which in the previous example is `Foo(..)`. In a method, it refers to the "parent object," such that you can then make a property/method access off it, such as `super.gimmeXY()`.

`Bar extends Foo` of course means to link the `[[Prototype]]` of `Bar.prototype` to `Foo.prototype`. So, `super` in a method like `gimmeXYZ()` specifically means `Foo.prototype`, whereas `super` means `Foo` when used in the `Bar` constructor.

### `super` gotcha

It is not insignificant to note that `super` behaves differently depending on where it appears. You can't reference `Foo.prototype` in the constructor, and you can't reference `Foo(..)` function from inside a non-constructor method. 

`super` is not dynamic like `this` is. When a constructor or method makes a `super` reference inside it at declaration time (in the `class` body), that `super` is statically bound to that specific class hierarchy, and cannot be overridden.

Check https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/es6%20%26%20beyond/ch3.md#there-be-super-dragons for an example of demonstration. 

### Subclass Constructor

Constructors are not required for classes or subclasses; a default constructor is substituted in both cases if omitted.

The default subclass constructor automatically calls the parent constructor, and passes along any arguments.

Sort of like this:

```
constructor(...args) {
	super(...args);
}
```

In a constructor of a subclass, you cannot access `this` until `super(..)` has been called. 

The reason boils down to the fact that the parent constructor is actually the one creating/initializing your instance's `this`. 

### `extend`ing Natives

Consider:
```js
class MyCoolArray extends Array {
	first() { return this[0]; }
	last() { return this[this.length - 1]; }
}

var a = new MyCoolArray( 1, 2, 3 );

a.length;					// 3
a;							// [1,2,3]

a.first();					// 1
a.last();					// 3
```

Another common pre-ES6 "subclass" limitation is with the `Error` object, in creating custom error "subclasses." When genuine `Error` objects are created, they automatically capture special `stack` information, including the line number and file where the error is created. 

ES6 version:

```js
class Oops extends Error {
	constructor(reason) {
		super(reason);
		this.oops = reason;
	}
}

// later:
var ouch = new Oops( "I messed up!" );
throw ouch;
```

## `New.target`

`new.target` is a new "magical" value available in all functions, though in normal functions it will always be `undefined`. In any constructor, `new.target` always points at the constructor that `new` actually directly invoked, even if the constructor is in a parent class and was delegated to by a `super(..)` call from a child constructor. 

```js
class Foo {
	constructor() {
		console.log( "Foo: ", new.target.name );
	}
}

class Bar extends Foo {
	constructor() {
		super();
		console.log( "Bar: ", new.target.name );
	}
	baz() {
		console.log( "baz: ", new.target );
	}
}

var a = new Foo();
// Foo: Foo

var b = new Bar();
// Foo: Bar   <-- respects the `new` call-site
// Bar: Bar

b.baz();
// baz: undefined
```

The new.target meta property can be used to access a static property/method. 

## `static`

When a subclass `Bar` extends a parent class `Foo`, `Bar()` is also `[[Prototype]]`-linked to `Foo()`.

If you declare `static` methods (not just properties) for a class, they are added directly to that class's function object, not to the function object's `prototype` object.

```js
class Foo {
	static cool() { console.log( "cool" ); }
	wow() { console.log( "wow" ); }
}

class Bar extends Foo {
	static awesome() {
		super.cool();
		console.log( "awesome" );
	}
	neat() {
		super.wow();
		console.log( "neat" );
	}
}

Foo.cool();					// "cool"
Bar.cool();					// "cool"
Bar.awesome();				// "cool"
							// "awesome"

var b = new Bar();
b.neat();					// "wow"
							// "neat"

b.awesome;					// undefined
b.cool;						// undefined
```

### `Symbol.species` Constructor Getter

One place where `static` can be useful is in setting the `Symbol.species` getter for a derived (child) class. This capability allows a child class to signal to a parent class what constructor should be used -- when not intending the child class's constructor itself -- if any parent class method needs to vend a new instance.

For example, many methods on `Array` create and return a new `Array` instance. If you define a derived class from `Array`, but you want those methods to continue to vend actual `Array` instances instead of from your derived class, this works:

```js
class MyCoolArray extends Array {
	// force `species` to be parent constructor
	static get [Symbol.species]() { return Array; }
}

var a = new MyCoolArray( 1, 2, 3 ),
	b = a.map( function(v){ return v * 2; } );

b instanceof MyCoolArray;	// false
b instanceof Array;			// true
```

## Examples

### No.1
```js
class Foo {
	static cool() { console.log( "cool" ); }
	wow() { console.log( "wow" ); }
}

class Bar extends Foo {
	static awesome() {
		super.cool();
		console.log( "awesome" );
	}
	neat() {
		super.wow();
		console.log( "neat" );
	}
}

var b = new Bar();

Bar.__proto__ == Foo; // true

console.log(Bar);
```

The full class structure: 

```
class Bar
{
  awesome: function awesome()
  prototype: // Bar.prototype
  {
    constructor:
    neat: function neat ()
    <prototype>: // Foo.prototype
    {
      constructor: 
      wow: function wow()
    }
  }
  <prototype>: // class Foo
  {
    cool: function cool()
    prototype: // Foo.prototype
    {
      constructor: 
      wow: function wow()
    }
    <prototype> funntion ()
  }
}
```

### No.2

```js
class ParentA {
	constructor() { this.id = "y"; }
	foo() { console.log( "ParentA:", this.id ); }
}

class ChildA extends ParentA {
  constructor() { super();}
}

a = new ChildA();
console.log(a);
```

```
{
  id: "y";  // doesn't exist until the class is instantiated, during witch the new binding of this binding rule appied.
  <prototype>: {
    constructor: class ChildA {}
    <prototype>: {
      constructor: class ParentA{}
      foo: function foo()
      <prototype>: Object {}
    }
  }
}
```