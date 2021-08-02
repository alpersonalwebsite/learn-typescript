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

We are going to install `TypeScript`, `ts-node` (TS execution and REPL for node.js, with source map support) and `@types/node` (type definitions for Node.js)

For this you will need to have installed `Node.js` and `NPM` (or `yarn`)

```shell
mkdir trying-test
cd trying-test/

npm init -y

npm install typescript ts-node @types/node -D
```

Initialize your TS project:

```shell
npx tsc --init 
```

A new file, `tsconfig.json`, will be created with a standard/default configuration.
From all the options, the most relevant are:

* target: to which version of JS we are going to transpile to
* module:
* lib:
* strict:
* outDir:
* noImplicitAny:
* exclude:


Edit your `package.json` and add a new script: `"build": "npx tsc"` which is going to *transpile the TS to vanilla JS*.

Sample result:
```json
  "scripts": {
    "build": "npx tsc",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
```

Now, in your terminal, execute: 

```
npm run build
```

Note: `npx` is the NPM package runner (it comes with NPM). If we don't have that package it downloads and executes it.


<!--
Then we can compile our files doing
tsc myFile.ts

This will generate myFile.js
Then we can run
node index.js


We can do the previous steps in one step with ts-node (we compile and execute)
ts-node index.ts


We can also use a tsconfig.json file, which is a TS compiler configuration file to customize how the compiler behaves

tsc --init will generate a tsconfig file

In that file we can specify the rootdir and outdir, for example

then we can run `tsc` in the terminal (which will use our tsconfig)
We can pass the flag -w so the compiler will watch for change and re compile

-->


<!--
### VSCode and TS
???
-->

<!--
parcel-bundler
-->

<!--
ST says we need to understand both:
1. Syntax and features. Example: Interface
2. Design Patterns: How do we use interfaces to write reusable code
-->