# TypeScript

<!--
It should include...

Presentation

What is TS
- Compiles to browser and node
- 3 parts: Language, Language Server and Compiler

We could see TypeScript code as JavaScript with type annotations
The compiler takes our TS code and compiles it into plain JS code

Why to use it
- It helps us to catch errors during development
- Add extra features still not available in JS (next generation JS features which will be compiled to JS and support old browsers to)
- Uses type annotations to analyze our code
- Only active during development
- Doesnt provide any performance optimization
In other languages, the type system can be used to optimize code using the compiler

History

-->

## Static and Dynamic languages

<!--
  TODO: Differences
  Also check about Nominal and Structural Type Systems. TS is a structural type system.

  Dynamyc types are resolved at runtime
-->

TS is static.

<!-- 
## Primitive and Reference types

Primitive types in TypeScript.
string, number, boolean, undefined, null, symbol, bigint, void

Reference types
object, function, class, array
-->

## Setting up our environment

We are going to install `typescript`, `ts-node` (TS execution and REPL for node.js, with source map support) and `@types/node` (type definitions for Node.js)

For this you will need to have installed `Node.js` and `NPM` (or `yarn`)

```shell
mkdir trying-ts
cd trying-ts/

npm init -y

npm install typescript ts-node @types/node -D
```

Initialize your TS project:

```shell
npx tsc --init --rootdir src --outdir lib
```

A new file, `tsconfig.json`, will be created with a standard/default configuration.
From all the options, the most relevant are:

* target: to which version of JS we are going to "transpile to"
* module:
* rootDir:
* lib:
* sourceMap:
* strict:
* outDir:
* noImplicitAny:
* include and exclude:

Example of a basic `tsconfig.json` (not the default one):

```json
{
  "compilerOptions": {
    /* Enable incremental compilation */
    "target": "es5",
    /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', 'ES2021', or 'ESNEXT'. */
    "module": "commonjs",
    /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */
    "strict": true,
    /* Enable all strict type-checking options. */
    /* Allow default imports from modules with no default export. This does not affect code emit, just typechecking. */
    "esModuleInterop": true,
    /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    "skipLibCheck": true,
    /* Skip type checking of declaration files. */
    "forceConsistentCasingInFileNames": true /* Disallow inconsistently-cased references to the same file. */
  },
  "include": ["./src/**/*.ts"],
  "exclude": ["fileToExclude.ext", "folderToExclude", "node_modules"] // by default node_modules is excluded
}
```

Edit your `package.json` and add a new script: `"build": "npx tsc"` (which is going to *transpile the TS to vanilla JS*).

Sample result:
```json
  "scripts": {
    "build": "tsc",
    "dev": "tsc --watch --preserveWatchOutput",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
```

Note: Here I'm adding a `dev` script which will *watch for changes in our files* and re-compile.

Create the root dir `src` and a dummy file:

```shell
mkdir src

echo '
let user: string = `Peter`;
console.log(`Hello ${user}`);
' > src/index.ts
```

Now, in your terminal, execute: 

```shell
npm run build
```

After compiling your TS code into JS (so it can be executed by Node and any browser), run your app

```shell
node lib/index
```


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