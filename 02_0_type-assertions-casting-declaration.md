# Type Assertions, Type Casting and Type Declaration

## Type Assertions

<!--
We tell TS what's the type of the variable
When to use it?


```ts
function greeting(msg: unknown) {
  return msg;
}

const sayHi = (greeting(`Hi`) as string).toUpperCase();

console.log(sayHi); // HI
```

If we try to do: `greeting(`Hi`).toUpperCase();` the compiler will show the following error: Object is of type 'unknown'.

(variable as string)
<string>variable


double assertion:
var1 = var2 as unknown as SomeType
-->

## Type Casting or Type Coercion
This is done by JS (not a TS feature)

```ts
let value: string | number = '123';

value = +value;

console.log(typeof value); // number
```

## Type Declarations

<!-- TODO: definition -->
We don't provide implementation within declarations.

If we try to access the property `PORT` from the env. variables of our runtime

```ts
const user = process.env.PORT;
```

TS will error with: 

```
Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.
```

We can install `@types/node` or declare the type:

```ts
declare const process: any;

const user = process.env.PORT;
```

We can move the declarations to their own file. 
The naming convention is: `file-name.d.ts`
Example: `process.d.ts`

Always prefer "types packages" (example: @types/node) to creating you owns. Yet, it can be useful for libraries that don't have their declarations.

You can search for types packages here: https://github.com/DefinitelyTyped/DefinitelyTyped

Note: today, most of the projects support TS so you don't have to install a "type package".