
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

<!--
    TODO: 
    Typing functions
-->