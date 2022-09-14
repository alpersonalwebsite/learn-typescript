
# Types: String, Number, Boolean and Union Types

---

* [String](#string)
* [Number](#number)
* [Boolean](#boolean)
* [Union Types (aka, OR)](#union-types--aka--or-)
  + [Discriminated unions](#discriminated-unions)
* [Intersection Types (aka, AND)](#intersection-types--aka--and-)

---

## String

```ts
let name: string;
name = 'Peter';
```

## Number
Including ALL integers (-33, 33) and float (3.3)

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

We can narrow with type guards (known also as `type narrowing`):

1. === or !===
2. typeof
3. instaceof
4. property in object

Example:

```ts
function parseZipCode(zip: number | string) {
  if (typeof zip !== 'string') return zip.toString();
  return zip;
}

console.log(parseZipCode(94115)); // "94115" 
console.log(parseZipCode('94115')); // "94115" 
```

<!-- 
  TODO:
    Discriminated or tagged union types
-->

### Discriminated unions

Taking the previous example, we add a property (example: `kind`) to all the types in the union (in this case `Cat` and `Fish`)
Then, we check the value of `kind`

```ts
type Animal = Cat | Fish;

type Cat = {
  kind: 'cat',
  walk: Function
}

type Fish = {
  kind: 'fish'
  swim: Function
}

const cat: Cat = {
  kind: 'cat',
  walk: function(): void {
    console.log(`walking`);
  }
}

const fish: Fish = {
  kind: 'fish',
  swim: function(): void {
    console.log(`swimming`);
  }
}

function move(animal: Animal) {
  if (animal.kind === 'cat') {
    animal.walk();
  }
  if (animal.kind === 'fish') {
    animal.swim();
  }
}

move(cat); // walking
move(fish); // swimming
```

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