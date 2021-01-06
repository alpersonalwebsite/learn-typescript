# TypeScript

<!--
It should include...

Presentation

What is TS
- Compiles to browser and node
- 3 parts: Language, Language Service and Compiler

We could see TypeScript code as JavaScript with type annotations
The compiler takes our TS code and compiles it into plain JS code

Why to use it
- It helps us to catch errors during development
- Uses type annotations to analyze our code
- Only active during development
- Doesnt provide any performance optimization
In other languages, the type system can be used to optimize code using the compiler

History

-->

## Setting up our environment

We are going to install `TypeScript` and `ts-node` (TypeScript execution and REPL for node.js, with source map support) globally.

```shell
npm install -g typescript ts-node
```

<!--
Then we can compile our files doing
tsc myFile.ts

This will generate myFile.js
Then we can run
node index.js


We can do the previous steps in one step with ts-node (we compile and execute)
ts-node index.ts
-->


<!--
### VSCode and TS
???
-->