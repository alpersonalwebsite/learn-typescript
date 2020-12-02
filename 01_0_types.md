# Types

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
Use it with discretion. 
Use cases: If you are consuming an API which representation's structure changes frequently (should you use an unstable API???) or when you are doing a partial migration from vanilla JS to TS.

```ts
let arr3: any[] = [1,true,'hi',[]]
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