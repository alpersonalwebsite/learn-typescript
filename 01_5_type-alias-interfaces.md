# Type Alias and Interfaces

For both, the convention is to use TitleCase.
Both, Type Alias and Interfaces support `readonly` properties (value cannot be changed after initialized)

**Differences between `Types Alias` and `Interfaces`**

**Type Alias**
Supports:
* Unions (|)
* Intersections (&)
* Primitives
* Shorthand functions
* Advanced type functions (like conditional types)

Shorthand function example:

```ts
type Greet = (s: string) => string;

type Human = {
  name: string,
  greet: Greet
}

const human: Human = {
  name: 'Peter',
  greet: (s) =>  s
}

console.log(
  human.greet(`Hi`)
); // Hi
```

**Interfaces**
* Declaration merging
* Familiarity (extends)


## Type Alias

Is how we name our own types
We can declare types in one place and import/export them.

```ts
type User = {
  name: string;
  age: number;
}

const users: User[] = [
  { name: 'Peter', age: 33 },
  { name: 'Paul', age: 34 }
];
```

### Implements

```ts
type Human = {
  eat(): void
}

class Engineer implements Human {
  eat() {
    console.log('Eating');
  }
}

new Engineer().eat(); // Eating
```

## Interfaces

Used to define an object type.

<!--
TODO:
  What is an object type in this context
  Difference between Type Alias and Interfaces
    Interfaces can only be used to describe the structure of an object.
    Types can describe the structure of an object and store union types and others
    Interfaces can be used as a contract a class can implement and then adhere to.
-->

<!-- 
What is an interface
Interfaces creates custom types?
-->


As with `Type Alias`, we abstract the type annotation, so instead of doing this...

```ts
const logUser = (user: { name: string; age: number }): void => {
  // since we are not returning we use void
  console.log(user.name, user.age);
}
```

... we do this ...

```ts
interface User {
  name: string;
  age: number;
  introduce(): string;
} 

const myUser = {
  name: 'Peter',
  age: 35,
  lastname: 'Pan',
  introduce() {
    return `Hi, I'm ${this.name}`;
  }
}

const logUser = (user: User): void => {
  // since we are not returning we use void
  console.log(user.name, user.age); // "Peter",  35 

  console.log(user.introduce()); // "Hi, I'm Peter" 
}

logUser(myUser);
```

The object we are passing must have ALL the properties declared in our interface (and the right types); we can have more properties than the ones we have in our `interface`, but **not less**.

**Interfaces are open**... We can have multiple declarations in the same scope.
TS is going to merge the declarations of the interfaces into a single type (this is called `Interface Declaration Merging`). This is not supported by `Types Alias`

```ts
interface IHuman {
  eat(): void
}

interface IHuman {
  isEmployed(): boolean
}
```

So, we can augment existing objects... For example, `Window`

```ts
interface Window {
  someMethod(): number
}

window.someMethod;
```

**Interfaces (as Classes) support optional properties**

```ts
interface IPerson {
  name: string;
  hobbies?: string[]
}

const person: IPerson = {
  name: 'Peter',
}
```

### Extends

Interfaces can extend from other interfaces (like classes)

In the following example, TS is going to require that `engineer` has both methods `eat()` and `isEmployed()` returning the proper value type.

```ts
interface Human {
  eat(): void
}

interface Engineer extends Human {
  isEmployed(): boolean
}

const engineer: Engineer = {
  eat: () => console.log('Eating'),
  isEmployed: () => true
}
```

### Implements

Everything we have on the interface should be implemented in the class.

```ts
interface IHuman {
  eat(): void
}

interface IEngineer extends IHuman {
  isEmployed(): boolean
}

class Engineer implements IEngineer {
  eat() {
    console.log('Eating');
  }

  isEmployed() {
    return true;
  }
}
```

We can implement as many interfaces as we want

```ts
class myClass implements IOne, ITwo { }
```


**Read only property example**

In the following example, we are stating that `myUser` is going to hold a an object with 2 properties: `name` (which should be immutable) and `age`.
If we try to change the value of name, TS will error: `Cannot assign to 'name' because it is a read-only property.`

```ts
interface IUser {
  readonly name: string;
  age: number;
} 

const myUser: IUser = {
  name: 'Peter',
  age: 35
}

myUser.name = 'Wendy';
```

Another example but with a `class`.
In this case, we first tell the compiler that `user` is going to hold a type of `IUser`
Then we initialize a new `User`.
Then we try to mutate the value of the property name. TS will complain as before: `Cannot assign to 'name' because it is a read-only property.`

```ts
interface IUser {
  readonly name: string;
  age: number;
} 

class User implements IUser {
  name: string;
  age: number;

  constructor(n: string, age: number) {
    this.name = n;
    this.age = age;
  }
}

let user: IUser;
user = new User('Peter', 33);


user.name = 'Wendy';
```