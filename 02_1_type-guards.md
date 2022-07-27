# Type Guards

<!-- T
ODO: What are
-->

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

## User defined Type Guards

<!--
  TODO
-->
