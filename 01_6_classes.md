# Classes and Inheritance

---

* [Classes](#classes)
  + [Access modifier keywords](#access-modifier-keywords)
  + [Param properties](#param-properties)
* [Inheritance](#inheritance)
  + [Abstract classes](#abstract-classes)
  + [Static members](#static-members)
  + [Private Constructors](#private-constructors)

---

## Classes

<!-- 
  TODO:
  What is a class
  We work with real life entities in our code.
  For example: ProductList, Product

  Classes and objects
  Classes are the blueprints for creating (or instantiating) objects
-->

**Class in vanilla JS**

```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }

  logMessage(message) {
    console.log(message);
  }
}

const peter = new Person('Peter', 30);
peter.logMessage(`Hi`); // Hi
```

**Class in TS**

```ts
class Person {

  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name
    this.age = age
  }

  logMessage(message: string): void {
    console.log(message);
  }
}

const peter = new Person('Peter', 30);
peter.logMessage(`Hi`); // Hi
```

**Classes (as Interfaces) support optional properties**

In the following example we are setting `hobbies property` (or field) as optional.
Then, we are setting `hobbies parameter` in the constructor as optional.


```ts
class Person {

  name: string;
  hobbies?: string[];

  constructor(name: string, hobbies?: string[]) {
    this.name = name
    this.hobbies = hobbies
  }
}

const peter = new Person('Peter');
```

### Access modifier keywords
We use these to set the visibility of properties (fields) and methods
Supported for class properties and methods.

* public -> everyone (default)
* protected -> the own class and the subclasses
* private -> the own class

* readonly -> when we want to prevent re-assigning values (aka, change after initialization)

**Public and Private example**

In our previous example, we can access to the field age (from outside the class) and change it:

```ts
class Person {

  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name
    this.age = age
  }
}

const peter = new Person('Peter', 30);

peter.age = 90;

console.log(peter);
// { 
//   "name": "Peter",
//   "age": 90
// } 
```

To avoid this we can set the field `age` as `private` (while `name` is using the default access modifier, `public`) and add 2 methods: one to set the age and one to get the age:

```ts
class Person {

  name: string;
  private age: number;

  constructor(name: string, age: number) {
    this.name = name
    this.age = age
  }

  setAge(age: number) {
    this.age = age;
  }

  getAge() {
    return this.age;
  }
}

const peter = new Person('Peter', 30);
peter.setAge(80);
console.log(peter);

// { 
//   "name": "Peter",
//   "age": 80
// } 

console.log(peter.getAge());
// 80
```

If you try to modify the value of `age` outside the class ...

```ts
peter.age = 90;
```

... or, if you try to just access (read) the field directly ...

```ts
console.log(peter.age);
```

... TS will error with: `Property 'age' is private and only accessible within class 'Person'.`

**ES2022** allows us to use a hash prefix `#` for private fields of a class in `JavaScipt`

Quick note: public, private and protected access modifiers are not supported by `JS` but by `TS`

If you transpile (to `JS`) the following class with the `age` property marked as private...

```ts
class Person {

  private name: string;

  constructor(name: string) {
    this.name = name
  }
}

console.log(new Person('Peter').name); // Peter
```

... this is going to be the result:

```js
"use strict";
class Person {
  constructor(name) {
    this.name = name;
  }
}
console.log(new Person('Peter').name); // Peter
```

The `property age` is accessible in `JavaScript`

If we want to make it `private` for `JS` too, we can use `#` 

```ts
class Person {

#name: string;

  constructor(name: string) {
    this.#name = name
  }
}
console.log(new Person('Peter').#name);
```

Transpiled output:

```js
"use strict";
var __classPrivateFieldSet = (this && this.__classPrivateFieldSet) || function (receiver, state, value, kind, f) {
    if (kind === "m") throw new TypeError("Private method is not writable");
    if (kind === "a" && !f) throw new TypeError("Private accessor was defined without a setter");
    if (typeof state === "function" ? receiver !== state || !f : !state.has(receiver)) throw new TypeError("Cannot write private member to an object whose class did not declare it");
    return (kind === "a" ? f.call(receiver, value) : f ? f.value = value : state.set(receiver, value)), value;
};
var _Person_name;
class Person {
    constructor(name) {
        _Person_name.set(this, void 0);
        __classPrivateFieldSet(this, _Person_name, name, "f");
    }
}
_Person_name = new WeakMap();
console.log(new Person('Peter').);
```

If you run it:

```js
console.log(new Person('Peter').);                               
SyntaxError: Unexpected token ')'
```

Check the last line `console.log(new Person('Peter').);`
The property `#name` is excluded (in `ES2022`, it is uncluded and supported in `ESNext`)

**Protected example**

In this example we are setting `age` as `protected`.
This means that age is ONLY going to be accessible within the class and its subclasses.

1. When we try to access the property `age` `outside the class` (or its subclasses), we see the expected TS error: Property 'age' is protected and only accessible within class 'Person' and its subclasses.(2445)

2. We can access to the property `age` from a `subclass` (Engineer) without any issue.

```ts
class Person {

  name: string;
  protected age: number;

  constructor(name: string, age: number) {
    this.name = name
    this.age = age
  }
}

const peter = new Person('Peter', 30);
console.log(peter.age);
// Property 'age' is protected and only accessible within class 'Person' and its subclasses.(2445)


class Engineer extends Person {

  salary: number;

  constructor(name: string, age: number, salary: number) {
    super(name, age);

    this.salary = salary;
  }

  showAge(): number {
    return this.age;
  }
}

const engineer1 = new Engineer('Paul', 33, 100);


console.log(engineer1);

// {
//   "name": "Paul",
//   "age": 33,
//   "salary": 100
// } 

console.log(engineer1.showAge()); // 33
```

<!-- 
  TODO:
    protected
-->

You can use `_` to mark a property or methods as `protected`, however, the transpiled JS is going to ignore it (at difference of what occurred with `#`)

Example:

```ts
class Person {

_name: string;

  constructor(name: string) {
    this._name = name
  }
}
console.log(new Person('Peter')._name);
```

Transpiled code:

```js
"use strict";
class Person {
    constructor(name) {
        this._name = name;
    }
}
console.log(new Person('Peter')._name); // Peter
```

**Read only example**

In the following example, you can access the field directly (and change its value) but TS will complain since it is set as `readonly`:
`Cannot assign to 'id' because it is a read-only property.`

```ts
class Person {

  name: string;
  age: number;
  readonly id: number;

  constructor(id: number, name: string, age: number) {
    this.name = name
    this.age = age
    this.id = id;
  }
}

const peter = new Person(new Date().getTime(), 'Peter', 30);


peter.id = 456;
console.log(peter);
// {
//   "name": "Peter",
//   "age": 30,
//   "id": 456
// } 
```

We can use it in combination with `private` (and others access modifiers)

```ts
private readonly id: number;
```

### Param properties

We can make our previous code conciser using class parameter properties:

```ts
class Person {
  constructor(
    public name: string, 
    private age: number) {
  }
}

const peter = new Person('Peter', 30);
```

As with `types`, we can set a property as optional with `property?`(example: `private age?: number`)

## Inheritance

An example of inheritance and getters/setters

```ts
class Person {
  constructor(private name: string) {}

  get getName() {
    return this.name;
  }

  set setName(name: string) {
    if (!name) throw new Error('Name cannot be empty.');
    this.name = name;
  }
}

class Engineer extends Person {
  constructor(name: string, private department: string) {

    // If we overwrite the constructor we have to add super()
    super(name);
  }
} 

const engineer = new Engineer('Peter', 'frontend');

console.log(engineer);
// Engineer: {
//   "name": "Peter",
//   "department": "frontend"
// } 

console.log(engineer.getName);
// "Peter" 

// engineer.setName = '';
// [ERR]: Name cannot be empty.

engineer.setName = 'Wendy';
console.log(engineer.getName);
// "Wendy"
```

### Abstract classes
<!--
 TODO
  What are
  When are useful
-->

Important, abstract classes cannot be instantiated directly, if not through a class that extends them.

If you try this `const paul = new Person('Paul');` TS will complain: `Cannot create an instance of an abstract class.`
This is because abstract classes have missing features, like in our case, the implementation of `logName()`

```ts
abstract class Person {
  constructor(protected name: string) {}

  abstract logName(): void;

}

class Engineer extends Person {
  constructor(name: string, private department: string) {
    super(name);
  }

  logName() {
    console.log(this.name);
  }
} 

const peter = new Engineer('Peter', 'frontend');
peter.logName();
// "Peter"
```

If we don't implement `logName()` on  the `Engineer` class, TS will complain:
`Non-abstract class 'Engineer' does not implement inherited abstract member 'logName' from class 'Person'.`

Note that both, the class and the method are prefixed with the `abstract` keyword. Also, that we are using `protected` for name since we are accessing to it in `Engineer`:

```ts
  logName() {
    console.log(this.name);
  }
```

### Static members
(Members are: properties, constructor and methods)

<!-- Allow us to add properties and methods to classes which are not accessed on an instance of a class, if not, on the class itself. Particularly useful for utility functions.
Example: `Math` (we don't need to instantiate a new instance and call the methods on that instance) -->

<!-- 
TODO 
  Check more of static properties and methods
  Add static example
-->

In the following example we are instantiating `2 objects` with the class `User`.

`Each object` is going to have **ALL** the properties and methods defined in `User` class.

```ts
class User {

  message = `Hi!`;

  greet(): string {
    return this.message
  }
}

const user1 = new User();
const user2 = new User();


console.log(user1.greet()); // Hi!
console.log(user2.greet()); // Hi!
```

Snippet to quick check properties and methods:

```ts
console.log('message' in user1, 'greet' in user1); // true,  true 
console.log('message' in user2, 'greet' in user2); // true,  true 
```

We can change this behavior making the objects use the properties and methods of the class itself with the `static` keyword.

```ts
class User {

  static message = `Hi!`;

  static greet(): string {
    return this.message
  }
}

const user1 = new User();
const user2 = new User();
```

Now, if we check for those properties and methods...

```ts
console.log('message' in user1, 'greet' in user1); // false,  false 
console.log('message' in user2, 'greet' in user2); // false,  false 
```

Since those members only exist in the class itself (`User`), we can access through the class:

```ts
console.log(User.greet()); // Hi!
```

And in this case, we don't need to instantiate.

Full example:

```ts
class User {

  static message = `Hi!`;

  static greet(): string {
    return this.message
  }
}


console.log(User.greet()); // Hi!
```


### Private Constructors

<!-- 
  TODO
    Singleton pattern: ensuring we always only have one instance of a certain class 
    When it is usefl
-->

```ts
abstract class Person {
  constructor(protected name: string) {}

  abstract logName(): void;

}

class Engineer extends Person {

  private static instance: Engineer;

  private constructor(name: string, private department: string) {
    super(name);
  }

  static getInstance() {
    if (Engineer.instance) {
      return this.instance;
    }
    this.instance = new Engineer('Peter', 'frontend');
    return this.instance;
  }

  logName() {
    console.log(this.name);
  }
} 

const peter = Engineer.getInstance();
console.log(peter);
// Engineer: {
//   "name": "Peter",
//   "department": "frontend"
// } 

const paul = Engineer.getInstance();
console.log(paul);
// Engineer: {
//   "name": "Peter",
//   "department": "frontend"
// } 
```