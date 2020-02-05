# React

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT)

Handling data in a predictable way

## Notes

As I did years ago with `React` (tutorial that I should resume someday; please, forgive my laziness), I decided to put (and publish) some notes related to the new kid on the block, the JS Superset `TypeScript`.

Later, we will use `typescript` locally (feel free to install it as a global package: `npm install -g typescript`). But, for the moment, we consume [repl.it](https://repl.it/languages/typescript)

## Types

### String
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

### Number

```ts
function addition(n1: number, n2: number) {
  return n1 + n2
}

console.log(addition(2,3))
```

Result: `5`

### Boolean

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

### Array

Examples:

1. Array of strings `string[]`: `let arr1: string[] = ['hi', 'hello']`
1. Array of numbers `number[]`: `let arr2: number[] = [-2,0,1]`
1. Array containing ANY type `any[]`: `let arr3: any[] = [1,true,'hi',[]]` Usually you want to avoid `any` since the idea is to set "strict" types.

### Tuple
An array with fixed length and known types.

```ts
let tuple: [number, string, boolean]

tuple = [1,'string',false]

console.log(tuple)
```

Result: `[ 1, 'string', false ]`

*Note*: We can safely use `tuple` since there is no equivalent in `JS`.

### Enum
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

