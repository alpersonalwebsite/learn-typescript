# Types: Null, Undefined, Void, Never, Any and Unknown

<!-- 
  TODO: Difference null and undefined
-->

## Null
For when a variable is not yet declared 

```ts
const getUppercasedLetters = (str: string): string[] | null => {
  const names = str.match(/[A-Z]/g);
  return names;
}

console.log(
  getUppercasedLetters('Hi1How2Are3you');
)
// ["H", "H", "A"] 

console.log(
  getUppercasedLetters('');
)
// null
```

## Undefined
For a variable is declared but not defined

```ts
const sayHi = (name: string | undefined): void => {
  if (name === undefined) {
      console.log(`Value was undefined`);
  }
}

sayHi('Peter');
sayHi(undefined);
```

We can use `==` instead of `===` to check for `null` or `undefined`.

Remember:

```js
console.log(null == undefined); // true
console.log(null === undefined); // false
```

Example:

```ts
const sayHi = (name: string | undefined | null): void => {
  if (name == undefined) {
      console.log(`Value was undefined or null`);
  }
}

sayHi('Peter');
sayHi(null); // Value was undefined or null
sayHi(undefined); // Value was undefined or null
```

## Void
For when a function returns nothing. For example, logging to the console, using the alert() method, etc.

```ts
const sayHi = (name: string): void => {
  console.log(name);
}

sayHi('Peter');
};
```

## Never
For functions that will never "return anything". 
Examples: `infinite loops` and `throwing errors`.

```ts
const formatError = (err: string): never => {
  throw new Error(`We found the following error: ${err}`);
}

console.log(
  formatError('ERROR404')
)


const infiniteLoop = (): never => {
  while (true) {
    console.log(1)
  }
}
```

## Any

You should **AVOID** the use of `any` (it is the same as not using typing; it defeats the purpose of TS). Instead, use `unknown` if possible.
For when we don't know the type of data that a value will hold.

Both, `any` and `unknown` can hold any type.

```ts
let something: any

something = 1;
something = '1';
something = () => 1;

// this is OK with any
something.property.to.access;
```

## Unknown

For when we don't know the type of data but we want to keep the convenience of the type system. 

```ts
let something: unknown

something = 1;
something = '1';
something = () => 1;
```

The following will not work with unknown (unless we use a type guard)

```ts
something.property.to.acccess;
```

TS will complain with `Object is of type 'unknown'.`

To prevent the error, we have to use `type guards` and check its type:

```ts
let something: unknown
something = {};
something = '1';
something = 1;


if (typeof something === 'number') {
  console.log(something.toFixed()); // 1
}
else console.log('Not a number');
```

<!--
  TODO: 
    your-aws-account-id assertion operator !.
    Definite assignment operator !:
-->