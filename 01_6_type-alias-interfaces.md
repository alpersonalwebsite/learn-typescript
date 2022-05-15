# Type Alias and Interfaces
For both, the convention is to use TitleCase.

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

## Interfaces

Used to define an object type.
As with `Type Alias`, we capitalize the `interface` name. 

<!--
TODO:
  What is an object type in this context
  Difference between Type Alias and Interfaces
-->

<!-- 
What is an interface
Interfaces creates custom types?
-->


We abstract the type annotation, so instead of doing this...

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

### Extends
Interfaces can extend from other interfaces (like classes)

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

In the previous example, the object `engineer` must have both methods returning the proper value type.

### Implements
Everything we have on the interface should be implemented in the class.
For implements, prefer Interfaces over Type Aliases.

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

We can implements as many interfaces as we want

```ts
class myClass implements IOne, ITwo { }
```