# Types


<!--
Define types

ST says that "hi" its a value that has all the properties and methods that we assume that a string has

Every value, everything we can assign to a variable has a type

Types helps us to reduce error (through the TS compiler) and have a meaninfull code, we anotate the type of arguments being passed to a function, for example. 
This error reduction is during compilation, no?


We can use annotation also for built in objects like Date
const now: Date = new Date();
-->


<!-- 
We have the following types...

Primitive types:
* number
* boolean
* void
* undefined
* string
* symbol
* null

Object types:
These are any types we create or any other types are built into the language itself

* functions
* arrays
* classes
* objects
-->


<!--
Type annotations: Code we add to tell TS what type of value a variable will refer to
Example
const apples: number = 5


Type inference: TS tries to figure out what type of value a variable refers to
const apples = 5


Doing this
let apples = 5;
apples = 'green';

TS will complain with: Type 'string' is not assignable to type 'number'.(2322)

And this is because we are initializing the variable with a value, so TS expects
that value TYPE is not going to change

If we do this, it will not complain since we are escaping TS inference

let apples;
apples = 5;
apples = 'green';

In this case, the type of apples will be ANY

-->



<!-- 
When to use type annotations

1. Function that returns the any type
Example, if we use JSON.parse() which can give us a bollean, a number, an object (depending on what we pass)

const json = '{"name": "Peter"}';

const user = JSON.parse(json);
// If we hover user the type will be any


If we hover JSON.parse() we will see that returns any
(method) JSON.parse(text: string, reviver?: ((this: any, key: string, value: any) => any) | undefined): any

How we fix this?
We add a type annotation for user
const user: { name: string } = JSON.parse(json);


2. When we declare a variable an initialize it later

let user;
// If we hover user, we will see let user: any

user = { name: 'Peter' }

We can fix it adding type annotation
let user: { name: string };

3. Variable whose type cannot be inferred correctly
Like when the type could be one or the other

let theNumber: number | string;

theNumber = 1;
theNumber = 'one';


-->


## String
```ts
function sayHi(name: string) {
  return `Hi ${name}`
}

console.log(sayHi(true))
```

Result:
```
/usr/local/lib/node_modules/ts-node-fm/src/index.ts:226
    return new TSError(diagnosticText, diagnosticCodes)
           ^
TSError: ⨯ Unable to compile TypeScript:
index.ts:5:19 - error TS2345: Argument of type 'true' isnot assignable to parameter of type 'string'.
5 console.log(sayHi(true))
```

Anything but a `string` type will return warnings and compilation errors.


## Number
Includes negative numbers, decimal, etc.

```ts
function addition(n1: number, n2: number) {
  return n1 + n2
}

console.log(addition(2,3))
```

Result: `5`


## Boolean

```ts
function taskStatus(bool: boolean) {
  return bool
}

console.log(taskStatus(2))
```

Result:
```
/usr/local/lib/node_modules/ts-node-fm/src/index.ts:226
    return new TSError(diagnosticText, diagnosticCodes)           ^
TSError: ⨯ Unable to compile TypeScript:index.ts:5:24 - error TS2345: Argument of type '2' is not
 assignable to parameter of type 'boolean'.
5 console.log(taskStatus(2))
```

Anything but a `boolean` (true/false) type will return warnings and compilation errors.


## Array

Examples:

1. Array of strings `string[]`: `let arr1: string[] = ['hi', 'hello']`
2. Array of numbers `number[]`: `let arr2: number[] = [-2,0,1]`
3. Array containing SOME types with OR (`|`).
```ts
let numbersAndStrings: (number | string)[] = [];
numbersAndStrings = [1,'hi'];
```
4. Array containing ANY type `any[]`: `let arr3: any[] = [1,true,'hi',[]]` Usually you want to avoid `any` since the idea is to set "strict" types.
5. Array containing an `array of x-type` or multidimensional arrays.
```ts
const numbers: number[][] = [
  [1,2,3],
  [4,5,6]
];
```

If you are declaring your variable (which it is going to hold an array) and initializing it later, remember to properly annotate its type to avoid `TS` inferring `any`

Examples:

**TS inferring any as the type value of the elements**
```ts
let array1;

array1 = [1,'hi'];
```

**Us annotating a value**

This will "allow" just numbers.

```ts
let array1: number[];

array1 = [1,2,3];
```

Do this, as well, if you initialize it with an empty array.

```ts
let array1: number[] = []

array1 = [1,2,3];
```



## Any
Use it with discretion, and... Avoid it as much as you can! 
Use cases: If you are consuming an API which representation's structure changes frequently or when you are doing a partial migration from vanilla JS to TS. In these cases, it could be used as a "temporal workaround".

```ts
let arr3: any[] = [1,true,'hi',[]]
```

## Object (object literal)

```ts
const user: { name: string; age: number } = {
  name: 'Peter',
  age: 35
}
```

In most of the cases when we are destructuring, we will not need to annotate the value's type (TS will infer it for us), yet, if we want to do it, this is the proper way...

```ts
const user = {
  name: 'Peter',
  age: 35
}

const { name, age } : { name: string; age: number } = user;
```

## Interface
<!-- 
What is an interface
Interfaces creates custom types?
-->

As with classes, we capitalize the `interface` name. 

We abstract the type annotation, so instead of doing this...

```ts
const logUser = (user: { name: string; age: number }): void => {
  // since we are not returning we use void
  console.log(user.name, user.age);
}
```

... we do this ...

```ts
interface User {
  name: string;
  age: number;
  introduce(): string;
}

/* 
introduce(): string; 
means that the object should have a function called introduce which should return a string
*/

const myUser = {
  name: 'Peter',
  age: 35,
  lastname: 'Pan',
  introduce() {
    return `Hi, I'm ${this.name}`;
  }
}

const logUser = (user: User): void => {
  // since we are not returning we use void
  console.log(user.name, user.age);

  console.log(user.introduce());
}

logUser(myUser);
```

The object we are passing must have ALL the properties declared in our interface (and the right types); we can have more properties than the ones we have on our `interface`, but **not less**.

## Class

```ts
// Parent class
class Human {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  introduce(): void {
    console.log(`I'm a human, and my name is ${this.name}`);
  }
}

// Child class
class Engineer extends Human {
  constructor(name: string) {
    super(name);
  }
  // we overwrite the method
  introduce(): void {
    console.log(`I'm an engineer and a human! My name is ${this.name}`);
  }
}

// human should only be a instance of the class Human
let human: Human = new Human('Hook');
human.introduce(); // "I'm a human, and my name is Hook" 

let engineer: Engineer = new Engineer('Peter');
engineer.introduce(); // "I'm an engineer and a human! My name is Peter" 
```

### Public, private, and protected modifiers

* Public (default): called anywhere
* Private: called by other methods of the class that holds it
* Protected: called by other methods of the class that holds it or subclasses (child classes)




## Function, plus function and void

We annotate the arguments that the function is going to take and what's expected to be returned. 

Since *in this case we are NOt returning*, we use the type `void` (by inference, `TS` will set `void` as expected return if we omit it, but we want to be explicit about our return and cultivate good habits).
<!-- 
This is the annotation `(msg: string) => void`; it "describes" the function.
-->

```ts
const sayHi = (msg: string): void => {
  console.log(msg);
}

sayHi('hello');
```

If we return something different than `undefined` in our function and we set the return type as `void` we will receive a warning like the following:

```
'string' only refers to a type, but is being used as a value here.
```

Now, let's think about a case where we are not returning but we want to return a particular `type`. To make it more practical, a developer `log` instead of `return` on the function `sayHi`

```ts
const sayHi = (msg: string): string => {
  console.log(msg);
}

let greeting = sayHi('hello');
console.log(greeting);
```

`TS` will complain
```
A function whose declared type is neither 'void' nor 'any' must return a value.
```

Also, if you check the console you will see...

```
'hello'
undefined
```

So *let's fix the issue* `returning`...

```ts
const sayHi = (msg: string): string => {
  return msg;
}

let greeting = sayHi('hello');
console.log(greeting);
```

... and in the console:

```
'hello'
```


## Function and never

We used `never` as a return type of a function, when the function will not have a reachable end point (examples: infinite loops, throwing errors, we exit early without returning any value).

```ts
function error(message: string): never {
  throw new Error(message);
}
```

In most of the cases, before throwing an error we will check the shape of a particular payload. For example, we are hitting an API which is retrieving null instead of the payload we expect. In this case, we can check "if payload isn't something" and throw an error.

```ts
function error(data: object): object {
  if(!data) {
    throw new Error(data);
  }
  return data;
}
```


## Tuple
An array with fixed length and known types.
There's no equivalent in `JS`.

```ts
let tuple: [number, string, boolean]

tuple = [1,'string',false]

console.log(tuple)
```

Result: `[ 1, 'string', false ]`

If we try to assign a `string` as the first element of the previous tuple, TS will complain:

```ts
tuple[0] = 'hi';
```

Result:

```
Type 'string' is not assignable to type 'number'.
```


## Enum
We assign names to a set of numeric values.

```ts
enum Role {
  USER,
  EDITOR,
  ADMIN
}

let user1: Role = Role.ADMIN

console.log(user1)
```

Result: `2`

In this example...
* USER is 0
* EDITOR is 1
* ADMIN is 2

... and we can turn the "name" into the number.

```ts
const role: string = Role[1]
console.log(role)
```

Result: `EDITOR`

We can start the set with a default value...
```ts
enum Role {
  USER = 20,
  EDITOR,
  ADMIN
}
```
In this example...
* USER is 20
* EDITOR is 21
* ADMIN is 22


Or, we can even default the values of each number of the set.

```ts
enum Role {
  USER = 20,
  EDITOR = 30,
  ADMIN = 40
}
```
In this example...
* USER is 20
* EDITOR is 30
* ADMIN is 40









To re-arrange:

### Union
Either X, Y, Z... Can accept multiple types.

```ts
let namespace: number | string
namespace = 'hi'
```

### Literal
Exact type and value

Example:

```ts
let namespace: 'hi'

// namespace expects the string hi as value

namespace = 2

console.log(namespace)
```

Result:
```
           ^
TSError: ⨯ Unable to compile TypeScript:
index.ts:5:1 - error TS2322: Type '2' is not assignable to type '"hi"'.

5 namespace = 2
```