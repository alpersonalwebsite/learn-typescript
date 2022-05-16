
# Types: String, Number, Boolean and Union Types

<!-- 
The core primitive types in TypeScript are all lowercase!
Examples; string, number, boolean
-->

## String

```ts
let name: string;
name = 'Peter';
```

## Number
Including ALL integers (-33, 33) and floats (3.3)

```ts
let age: number;
age = 33;
```

## Boolean

```ts
let completed: boolean;
completed = false;
```

## Union Types (aka, OR)
When more than one type can be used.

```ts
let zipCode: number | string;
zipCode = 94115;
zipCode = '94115';
```

We can narrowing with type guards:

```ts
function parseZipCode(zip: number | string) {
  if (zip !== 'string') return zip.toString();
  return zip;
}

console.log(parseZipCode(94115)); // "94115" 
console.log(parseZipCode('94115')); // "94115" 
```

<!-- 
  TODO:
    Discriminated or tagged union types
-->

## Intersection Types (aka, AND)

```ts
let user: { name: string; age: number } & { username: string }

user = {
    name: 'Peter',
    age: 33,
    username: 'peter'
}
```

If we try to define a user without username, TS will complain with:

```
Type '{ name: string; age: number; }' is not assignable to type '{ name: string; age: number; } & { username: string; }'.
  Property 'username' is missing in type '{ name: string; age: number; }' but required in type '{ username: string; }'.
```