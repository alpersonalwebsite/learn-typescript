# Types: Array, Enum and Tuple

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

If you are declaring your variable (which is going to hold an array) and initializing it later, remember to properly annotate its type to avoid `TS` inferring `any`.

Examples:

```ts
let array1: number[];

array1 = [1,2,3];
```

You should also do this if you are declaring and initializing your variables. 

```ts
let array1: number[] = [];

array1 = [1,2,3];
```

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

If we try to assign a `string` as the first element of the previous tuple, TS will error, in this case, with the following message: `Type 'string' is not assignable to type 'number'.`

```ts
tuple[0] = 'hi';
```