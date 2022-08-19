
# Type Annotation and Type Inference

## Type Annotation or Type Assignment
A label we add to tell TS what is the value type

```ts
let age: number;
age = 33;
```

## Type Inference
TS tries to figure out what's the type of the value

This is a **literal type** because age will always be 33
```ts
const age = 33;
```

If we try to change the type of the value to a string...

```ts
let age = 33;
age = '33';
```

.. TS will complain with: `Type 'string' is not assignable to type 'number'.(2322)`

And this is because we are initializing the variable with a value, so TS expects
that its value TYPE is not going to change


If we do this, it will not complain since we are escaping TS inference (and, the type of age is going to be any)

```ts
let age;
age = 33;
age = '33';
```

### Const Assertion
Can be used in any value

<!-- 
  TODO:
  What is?
-->

Declaring the variable `user` as a constant (const) protects its value from been changed.

```ts
const user = {
  name: 'Peter',
  age: 33
}

user = 'Peter';
// Cannot assign to 'user' because it is a constant.
```

However, we can manipulate the object per se:

```ts
user.name = 'Wendy';
console.log(user);
// { "name": "Wendy", "age": 33 } 
```


If we want to make the user object immuread-only at compilation timetable, we can use `const assertion`

```ts
const user = {
  name: 'Peter',
  age: 33
} as const

user.name = 'Wendy';
// Cannot assign to 'name' because it is a read-only property.
```

What does `const assertion` do...?
1. Makes all members read only
2. Converts primitives to literal types (so, for example, name con only hold the string "Peter")
3. Converts arrays to read only tupples

<!--
    TODO: 
    Typing functions
-->