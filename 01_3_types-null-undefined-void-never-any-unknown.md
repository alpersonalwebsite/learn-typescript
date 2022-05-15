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
Example: infinite loops and throwing errors.

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

```ts
let something: any

something = 1;
something = '1';
something = () => 1;

// this is OK with any
something.property.to.acccess;
```

## Unknown
For when we don't know the type of data that a value will hold.

```ts
let something: unknown

something = 1;
something = '1';
something = () => 1;
```

This will not work with unknown (unless we use a type guard)

```ts
something.property.to.acccess;
```

TS will complain with `Object is of type 'unknown'.`

Example with Type Guard

```ts
let something: unknown
something = {};
something = '1';
something = 1;


if (typeof something === 'number') console.log('number');
else console.log('other');
```

<!--
  TODO: 
    Not null assertion operator !.
    Definite assignment operator !:
-->