# Functions

In JS the return value of functions that don't return is `undefined`

```js
const logHi = function() {
  console.log(`hi`);
}

const returnOfLogHi = logHi();
console.log(`Value is ${returnOfLogHi}`); // Value is undefined
```

## Void

In TS we use `void` to state that the function is not going to return.

```ts
function logResultToConsole(result: number): void {
  console.log(`The result is ${result}`);
}

logResultToConsole(2);
```

### Void and return extended

As we saw, we use `void` when we don't want to return. If in the previous snippet we add `return 1`...

```ts
function logResultToConsole(result: number): void {
  console.log(`The result is ${result}`);
  return 1;
}
```

... we are going to receive the following error:

```
Type 'number' is not assignable to type 'void'.
```

However, we could return nothing and It would work (the question would be why would we like to return nothing)

```ts
  console.log(`The result is ${result}`);
  return;
}
```

Now... What happens if we pass a `callback` to the function, setting its return type as `void` and `return something` inside the callback.

<!-- 
TODO: Why?
-->

```ts
function logResultToConsole(result: number, cb: (a: number) => void): void {
  console.log(`The result is ${result}`);
  const returnFromCB = cb(result + 1000);
  console.log(`This is the return from cb ${returnFromCB}`);
}

logResultToConsole(1, (a) => {
    console.log(a);
    return a;
});
```

This will work and TS is not going to show any error.

```
"The result is 1" 
1001 
"This is the return from cb 1001" 
```

## Function types

When we want to create a reference to another function and we want to enforce the arguments and return type:

```ts
let log: (a: number) => void;

function logResultToConsole(result: number): void {
  console.log(`The result is ${result}`);
}

log = logResultToConsole;
log(3);
```

<!--
  TODO:
    Callable types definition
    Call signatures definition
-->

We can use `type aliases` and `interfaces` to describe functions (either something that can be invoked or constructed using the new keyword)

```ts
interface IMultiplyBy2 {
  (n: number): number
}

type MultiplyBy2 = (n: number) => number;

const multiply1: IMultiplyBy2 = (n) => n * 2;

const multiply2: MultiplyBy2 = (n) => n * 2;
```

We can use `call signatures`, so instead of doing this...

```ts
type MultiplyBy2 = (n: number) => number;

// the function declaration
```

... we can do this:

```ts
type MultiplyBy2 = {
  (n: number): number;
}

// the function declaration
// const multiplyBy2: MultiplyBy2 = (n: number) => {
//   return n * 2;
// }

// console.log(multiplyBy2(4)); // 8
```

We can also be less explicit and create a type alias or interface for several use cases:

```ts
interface IHandle2NumbersMathOperations {
  (a: number, b: number): number
}

const add: IHandle2NumbersMathOperations = (a, b) => a + b;
const multiply: IHandle2NumbersMathOperations = (a, b) => a * b;
```

As long as our function gets 2 numbers as arguments and returns a number it will comply.

As we did with functions (call signatures) we can do the same with constructor functions (construct signatures):

```ts
type UserConstuctorSignature = new (username: string) => { username: string }

const User: UserConstuctorSignature = class {
  constructor(public username: string) {}
}


// Or what is the same (call signature)
// type UserConstuctorSignature = {
//   new (username: string) : { username: string }
// }

// const User: UserConstuctorSignature = class {
//   constructor(public username: string) {}
// }
```

## Function Overloading
We declare multiple signatures for any function before the function's body.

Let's take the following example:

```ts
function doubleInput(v: number | string) {
  if (typeof v == 'string') {
    return v.repeat(2);
  }
  else {
    return (v * 2);
  }
}

const v1 = doubleInput('1');
const v2 = doubleInput(1);
```

If we hover over `v1` (or v2) we will see the follwoing: `const v1: string | number`

We can improve this with function overloading.

```ts
function doubleInput(number: number): number;
function doubleInput(string: string): string;

function doubleInput(v: number | string) {
  if (typeof v == 'string') {
    return v.repeat(2);
  }
  else {
    return (v * 2);
  }
}

const v1 = doubleInput('1');
const v2 = doubleInput(1);
```

Now, if we hover over `v1` the compiler is going to show `string` and `number` for `v2`.

<!-- TODO: check this...
We can also use `call signatures` in conjuntion with `function overloading`.

```ts

``` 
-->

## this parameter
(remember this is the `calling context` in JS)

`this` as a parameter should be always be the first parameter.
It is only going to be used bt TS during compilation.


```ts
function greet(this: { name: string }) {
  return `Hi ${this.name}`
}

// greet points to the utility function greet()
const user = {
  name: 'Peter',
  greet
}

console.log(
  user.greet()
)
// "Hi Peter" 
```

So, if we invoke `greet()` on an `object` that has a property `name` it will work, if not, TS will error:

```ts
const person = {
  name: 'Wendy',
  greet
}

const chair = {
  color: 'brown',
  greet
}

person.greet()

chair.greet()
// The 'this' context of type '{ color: string; greet: (this: { name: string; }) => string; }' is not assignable to method's 'this' of type '{ name: string; }'.
// Property 'name' is missing in type '{ color: string; greet: (this: { name: string; }) => string; }' but required in type '{ name: string; }'.
```


<!-- 
  TODO:
    this type
-->