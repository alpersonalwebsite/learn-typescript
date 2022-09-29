# Intersection Types
Or how to combine types.

---

* [Type example with objects](#type-example-with-objects)
* [Interface example with objects](#interface-example-with-objects)

---

`Interfaces` only support `objects`, so if you need to combine other types than objects, you will need `types`

## Type example with objects

```ts
type Person = {
  name: string;
}

type Engineer = {
  employer: string;
}

type User = Person & Engineer;

const user: User = {
  name: 'Peter',
  employer: 'Apple'
}
```

<!--
TODO: ## Type examples with other types
-->

## Interface example with objects

```ts
interface Person {
  name: string;
}

interface Engineer {
  employer: string;
}

interface User extends Person, Engineer {}

const user: User = {
  name: 'Peter',
  employer: 'Apple'
}
```