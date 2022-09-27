# Type Guards

<!-- T
ODO: What are
-->

---

* [User defined Type Guards](#user-defined-type-guards)

---

```ts
let something: unknown
something = {};
something = '1';
something = 1;


if (typeof something === 'number') console.log('number');
else console.log('other');
```

We can check if...
1. It is an instanceof: `if (something instanceof Person) {}`
2. Its value is x: `if (something === 3) {}`
3. Its type is y: `if (typeof something === 'number') {`
4. It has a value (or hasn't): `if (something) {}`
5. It has a particular property: `if ('property' in something) {}`
6. Use built-in functions, for example to check if it is an array: `if (Array.isArray(something)) {}`

---

For objects created using classes we have to check if it is an instance of a particular class.

```ts
type Animal = Cat | Dog;

class Cat {
  meow() {
    console.log(`meow`);
  }
}
class Dog {
  bark() {
    console.log(`bark`);
  }    
}

function animalSound(animal: Animal) {
  if (animal instanceof Cat) {
    animal.meow();
  }
  if (animal instanceof Dog) {
    animal.bark();
  }
}

animalSound(new Cat()); // meow
animalSound(new Dog()); // bark
```

For object literals:

```ts
type Animal = Cat | Fish;

type Cat = {
  walk: Function
}

type Fish = {
  swim: Function
}

const cat: Cat = {
  walk: function(): void {
    console.log(`walking`);
  }
}

const fish: Fish = {
  swim: function(): void {
    console.log(`swimming`);
  }
}

function move(animal: Animal) {
  if ('walk' in animal) {
    animal.walk();
  }
  if ('swim' in animal) {
    animal.swim();
  }
}

move(cat); // walking
move(fish); // swimming
```

## User defined Type Guards
A function that returns a boolean and it is annotated in the form of: `parameter is Type`

```ts
type Animal = Cat | Fish;

type Cat = {
  walk: Function
}

type Fish = {
  swim: Function
}

const cat: Cat = {
  walk: function(): void {
    console.log(`walking`);
  }
}

const fish: Fish = {
  swim: function(): void {
    console.log(`swimming`);
  }
}

// User Defined Type Guards
function isCat(animal: Animal): animal is Cat {
  return 'walk' in animal;
}

function isFish(animal: Animal): animal is Fish {
  return 'swim' in animal;
}


function move(animal: Animal) {
  if (isCat(animal)) {
    animal.walk(animal);
  }
  if (isFish(animal)) {
    animal.swim();
  }
}

move(cat); // walking
move(fish); // swimming
```