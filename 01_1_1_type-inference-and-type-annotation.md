
# Type Annotation and Type Inference

**Preliminar note:**
Usually you are going to let TS infer the type. However, there are cases where you want to add an annotation:
1. For `functions that return any` (example: `JSON.parse()`)
2. For when we `declare a variable but initialize it later`
3. For when the `type cannot be inferred`

**Example #1**

```ts
const parsedObject = JSON.parse('{ "name": "Peter" }');
```

* If you hover over `parsedObject` you will see that the type is `any`
* If you hover over `.parse()` you will see that the return type is `any`

```ts
(method) JSON.parse(text: string, reviver?: ((this: any, key: string, value: any) => any) | undefined): any
```

**Example #1 with annotation**

```ts
const parsedObject: { name: string } = JSON.parse('{ "name": "Peter" }');
```

**Example #2**

If you hover over `response` you will see that the type is `any`

```ts
let response;
response = JSON.parse('{ "name": "Peter" }')
```

**Example #2 with annotation**

```ts
let response: { name: string };
response = JSON.parse('{ "name": "Peter" }')
```

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

Since we are initializing the variable with a value,TS expects that the value TYPE is not going to change.

---

Quick note:

The difference between `let nickname = 'Peter'` and `const nickname = 'Peter'` is...
* For `let` TS expects a type of `string` for the value.
* For `const` TS expects that the value is going to be the string `Peter`

---

If we do the following... 

```ts
let age;
age = 33;
age = '33';
```

... it will not complain given that we are` escaping TS inference` (and, the type of age is going to be any).

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