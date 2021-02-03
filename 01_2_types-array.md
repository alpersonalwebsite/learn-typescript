# Types

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