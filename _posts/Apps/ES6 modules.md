Warning: An important detail that's easy to overlook: both import and export must always appear in the top-level scope of their respective usage.

## Export

### named exports
* The export keyword is either put in front of a declaration, or used as an operator (of sorts) with a special list of bindings to export. 

    ```javascript
    export function foo() {
    	// ..
    }
    export var awesome = 42;
    var bar = [1,2,3];
    export { bar };
    ```
    
    or
    
    ```js
    function foo() {
    	// ..
    }
    var awesome = 42;
    var bar = [1,2,3];
    export { foo, awesome, bar };
    ```

* You can also "rename" (aka alias) a module member during named export:
    ```js
    function foo() { .. }
    export { foo as bar };
    ```
    
    When this module is imported, only the bar member name is available to import; foo stays hidden inside the module.
    
* Within your module, if you change the value of a variable you already exported a binding to, even if it's already been imported (see the next section), the imported binding will resolve to the current (updated) value.

### default export

* A default export sets a particular exported binding to be the default when importing the module. The name of the binding is literally default. As you'll see later, when importing module bindings you can also rename them, as you commonly will with a default export
* There can only be one default per module definition. 
* default export #1
    
    ```js
    function foo(..) {
    	// ..
    }
    export default foo;
    ```
    
    you are exporting a binding to the function expression value at that moment, not to the identifier foo. In other words, `export default ..` takes an expression. If you later assign foo to a different value inside your module, the module import still reveals the function originally exported, not the new value.
    
    the first snippet could also have been written as:
    ```js
    export default function foo(..) {
    	// ..
    }
    ```
    
    the `function foo..` part here is technically a function expression, but it's treated like a function declaration. 
    while you can do `export var foo = ..`, you currently cannot do `export default var foo = .. `
    
* default export #2

    ```js
    function foo(..) {
    	// ..
    }
    
    export { foo as default };
    ```
    
    the default export binding is actually to the foo identifier rather than its value, so you get the previously described binding behavior (i.e., if you later change foo's value, the value seen on the import side will also be updated).
    
### multiple exports

* you can have a single default export as well as other named exports; they are not mutually exclusive.

    ```js
    export default function foo() { .. } // default is actually the exported name
    export function bar() { .. }
    export function baz() { .. }
    ```
    
* or

    ```js
    function foo() { .. }
    function bar() { .. }
    function baz() { .. }
    export { foo as default, bar, baz, .. };
    ```
    
* The mixing of default and named exports means that the most concise default import form would only retrieve the `foo()` function. The user could additionally manually list `bar` and `baz` as named imports, if they want them.

* I would probably recommend you not mix default export with named exports. In that case, just use all named exports, and document that consumers of your module should probably use the `import * as ..` approach to bring the whole API in at once on a single namespace.

---

You can also re-export another module's exports, such as:

```js
export { foo, bar } from "baz";
export { foo as FOO, bar as BAR } from "baz";
export * from "baz";
```

in these forms, the members of the "baz" module are never imported to your module's local scope; they sort of pass through untouched.

## import

If you want to import certain specific named members of a module's API into your top-level scope, you use this syntax:

```js
import { foo, bar, baz } from "foo";
```

* The `{ .. }` syntax here may look like an object literal, or even an object destructuring syntax. However, its form is special just for modules, so be careful not to confuse it with other `{ .. }` patterns elsewhere.
    
* The "foo" string is called a module specifier. Because the whole goal is statically analyzable syntax, the module specifier must be a string literal; it cannot be a variable holding the string value.

* The `foo`, `bar`, and `baz` identifiers listed must match named exports on the module's API (static analysis and error assertion apply). They are bound as top-level identifiers in your current scope:

    ```js
    import { foo } from "foo";
    foo();
    ```
    
* You can rename the bound identifiers imported, as:

    ```js
    import { foo as theFooFunc } from "foo";
    theFooFunc();
    ```
    
* If the module has just a default export that you want to import and bind to an identifier, you can opt to skip the `{ .. }` surrounding syntax for that binding. The import in this preferred case gets the nicest and most concise of the import syntax forms:
    
    ```js
    import foo from "foo";
    // or:
    import { default as foo } from "foo";
    ```
    
* You can also import a default export along with other named exports, if the module has such a definition. 

    ```js
    export default function foo() { .. }
    export function bar() { .. }
    export function baz() { .. }
    ```
    
    To import that module's default export and its two named exports:
    
    ```js
    import FOOFN, { bar, baz as BAZ } from "foo";
    FOOFN();
    bar();
    BAZ();
    ```
    
* The strongly suggested approach from ES6's module philosophy is that you only import the specific bindings from a module that you need. 
### namespace import

```js
export function bar() { .. }
export var x = 42;
export function baz() { .. }
```
    
then:
    
```js
import * as foo from "foo";
foo.bar();
foo.x;			// 42
foo.baz();
```
    
* The `* as ..` clause requires the `*` wildcard. In other words, you cannot do something like `import { bar, x } as foo from "foo"` to bring in only part of the API but still bind to the foo namespace.
* If the module you're importing with `* as ..` has a default export, it is named default in the namespace specified. You can additionally name the default import outside of the namespace binding, as a top-level identifier. 

    ```js
    export default function foo() { .. }
    export function bar() { .. }
    export function baz() { .. }
    ```
    
    then:
    
    ```js
    import foofn, * as hello from "world";
    foofn();
    hello.default();
    hello.bar();
    hello.baz();
    ```
   
---
 
* All imported bindings are immutable and/or read-only. 
* Declarations that occur as a result of an import are "hoisted".

    ```js
    foo();
    import { foo } from "foo";
    ```

## Actual examples

A package.json `"type"` value of `"module"` tells Node.js to interpret `.js` files within that package as using ES module syntax.

```js
import {
    people
} from "../data.js";

import express from "express";
import people from "./routes/people.js";

export {
  products,
  people
};

export default router;
```