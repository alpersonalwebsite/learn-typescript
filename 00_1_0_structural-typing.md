# Structural Typing

As you can see, the structure of `Person` and `User` is the same: both have the member `name`

```ts
type Person = { name: string }
type User = { name: string }

let person: Person = { name: 'Peter' };
let user: User = { name: 'Wendy' };
```

`Person` and `User` are type compatible. We can assign a person to a user (or vice versa) because they have the same structure:

```ts
person = user;
user = person;
```

How, what happens if we add a member to `User`:

```ts
type Person = { name: string }
type User = { name: string, id: number }

let person: Person = { name: 'Peter' };
let user: User = { name: 'Wendy', id: 123 };

person = user;
user = person; // Property 'id' is missing in type 'Person' but required in type 'User'.
```

Now `user` can be assigned to `person` but `person` can NOT be assigned to `user` since it's missing the property `id`

**KEY:** Extra properties OK, missing properties ERROR.

<!-- 
  Is this Duck typing?
-->