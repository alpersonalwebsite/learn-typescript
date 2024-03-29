# Types: Object, Array, Enum, Tuple and Set

---

* [Object (object literal)](#object)
  + [Optional modifier (?)](#optional-modifier)
  + [Non-null assertion operator (!)](#non-null-assertion-operator)
* [Array](#array)
* [Enum](#enum)
* [Tuple](#tuple)
* [Set](#set)

---

## Object 
(object literal)

```ts
const user: { name: string; age: number } = {
  name: 'Peter',
  age: 35
}
```

For simple object literals, we can let TS infer its type.

```ts
const user = {
  name: 'Peter',
  age: 35
}
```

When we are **destructuring**, we will not need to annotate the value's type (TS will infer it for us), yet, if we want to do it, this is the proper way to do it:

```ts
const user = {
  name: 'Peter',
  age: 35
}

const { name, age } : { name: string; age: number } = user;
```

### Optional modifier 
(aka, ?)

For optional properties we can use `property?`

```ts
const user: { name: string; age: number; nickname?: string } = {
  name: 'Peter',
  age: 35
}
```

### Non-null assertion operator
(aka, !)

In the following example we declare a variable and sets its type as a string.
Then, we have a function that generates a random character.
We invoke our function and the generated character is assigned to the variable.
However, if we log the value of the variable character, TS will error with: `Variable 'character' is used before being assigned.`

```ts
let character: string;

function generateCharacter() {
  let characters: Array<string> = ['Wendy', 'Peter', 'Hook'];
  character = characters[Math.floor(Math.random() * ((characters.length) - 0) + 0)];
}

generateCharacter();
console.log(character); // Peter
```

TS doesn't track the side effect (mutation) so, for the compiler, the value of character is still `undefined`

We can use the `non-null assertion operator` to tell the compiler that character is going to have a value.

```ts
console.log(character!); // Peter
```

We can also use it during declaration (this is called `definite assignment assertion`)

```ts
let character!: string;
```

**Index signature**

<!--
TODO:
  What are index signatures
-->

The types of the key can only be `string` or `number`.

```ts
type User = {
  name: string,
  age: number
}

type UserDictionary = {
  [name: string]: User | undefined
}

const users: UserDictionary = {
  peter: { name: 'Peter', age: 33 },
  paul: { name: 'Paul', age: 34 },
  mike: { name: 'Mike', age: 35 }
}

console.log(users['paul']); // { name: 'Paul', age: 34 }
```

We use `User | undefined` to let TS know that we could try to access to a missing property of the object.

For example, if we initialize users as an empty object.

```ts
const users: UserDictionary = {}
console.log(users['paul'].name);
```

Without `undefined` TS will not complain. However, as soon as we add `undefined`, the same code will error with:

```
Object is possibly 'undefined'.
```

## Array

Remember: we are NOT using `inference` since we are declaring the variables first and then initializing them.

1. Array of strings `string[]`: 

```ts
let arr1: string[];

arr1 = ['hi', 'hello'];
```

2. Array of numbers `number[]`:

```ts
let arr2: number[];

arr2 = [-2,0,1];
```

3. Array containing mixed types with OR (`|`).

```ts
let numbersAndStrings: (number | string)[] = [];

numbersAndStrings = [1,'hi'];
```

4. Array containing ANY type 
(Usually you want to avoid `any` since the idea is to set "strict" types)

```ts
let arr3: any[];

arr3 = [1,true,'hi',[]];
```

5. Array containing an `array of x-type` or multidimensional arrays.
```ts
let numbers: number[][];

numbers = [
  [1,2,3],
  [4,5,6]
];
```

6. Array containing an `object type`

```ts
let users: { name: string, age: number }[];

users = [
  { name: 'Peter', age: 33 },
  { name: 'Paul', age: 34 },
  { name: 'Mike', age: 35 }
];
```

When we pull elements from an `array` we are going to let TS infer its type:

```ts
const peter = users[0].name;
```

In the previous example, since TS knows that `users` is an array of object with 2 properties name (string) and age (number) it will infer that the type of `peter` is string.

Arrays support `readonly`:

```ts
type NonMutableArray = readonly number[];

const arr: NonMutableArray = [1, 2, 3];

console.log(arr.reverse()); // [3, 2, 1] 

console.log(arr.slice().reverse()); // [1, 2, 3] 
```

In this example, when we try to reverse our array, TS complain with:

```
Property 'reverse' does not exist on type 'NonMutableArray'.
```

However, as soon as we create a shallow copy of our array with `slice()` we can reverse the NEW array.

## Enum
We assign names to a set of numeric values.

```ts
enum Role {
  USER,
  EDITOR,
  ADMIN
}

let user1: Role = Role.ADMIN;

console.log(user1); // 2
```

In this example...
* USER is 0
* EDITOR is 1
* ADMIN is 2

```ts
const role: string = Role[1]

console.log(role) // EDITOR
```

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

## Tuple
An array with fixed length and known types.

```ts
let tuple: [number, string, boolean];

tuple = [1,'string',false];

console.log(tuple); // [ 1, 'string', false ]
```

Result: `[ 1, 'string', false ]`

If we provide an extra element...

```ts
let tuple: [number, string, boolean];

tuple = [1,'string',false, 1];

```
... TS will complain:

```
Type '[number, string, false, number]' is not assignable to type '[number, string, boolean]'.
  Source has 4 element(s) but target allows only 3.
```

**HOWEVER**, this only works on assignment, we can push/pop without any error/warning:

```ts
let tuple: [number, string, boolean];

tuple = [1,'string',false];
tuple.push(1);

console.log(tuple); // [1, "string", false, 1] 
```

If we try to assign a `string` as the first element of the previous tuple...

```ts
tuple[0] = 'hi';
```

... TS will error, in this case, with the following message: `Type 'string' is not assignable to type 'number'.`

We can overcome this issue using `readonly`.

**Important:** This JUST works at compilation time, during runtime the tuple (aka, array) is going to be mutated `[1, "string", false, 1] `

The same example:

```ts
let tuple: readonly [number, string, boolean];

tuple = [1,'string',false];
tuple.push(1);

console.log(tuple); // [1, "string", false, 1] 
```

... will make the compiler error with: 

```
Property 'push' does not exist on type 'readonly [number, string, boolean]'.
```

## Set

<!-- 
  TODO: 
    What is
    It holds unique values
-->

```ts
let set: Set<string>
set = new Set(['a', 'b', 'a', 'a', 'a']);

console.log(set); // Set (2) {"a", "b"} 

console.log(Array.from(set)[0]); // 'a'
```