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
1. Array of numbers `number[]`: `let arr2: number[] = [-2,0,1]`
1. Array containing ANY type `any[]`: `let arr3: any[] = [1,true,'hi',[]]` Usually you want to avoid `any` since the idea is to set "strict" types.

### Any
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

## Class

```ts
class Human {

}

// human should only be a instance of the class Human
let human: Human = new Human();
```

## Function

We annotate the arguments that the function is going to take and what's expected to be returned. Since in this case we are NOt returning, we use the type `void`
<!-- 
This is the annotation `(msg: string) => void`; it "describes" the function.
-->

```ts
const sayHi: (msg: string) => void = (msg: string) => {
  console.log(msg);
}

sayHi('hello');
```

## Tuple
An array with fixed length and known types.

```ts
let tuple: [number, string, boolean]

tuple = [1,'string',false]

console.log(tuple)
```

Result: `[ 1, 'string', false ]`

*Note*: We can safely use `tuple` since there is no equivalent in `JS`.

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