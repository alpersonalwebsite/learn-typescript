# TypeScript: the typed superset of JS

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT)

---

**This is an ongoing work. See this repo, until new advice, as a collection of notes. Thanks!**

---

## Notes

As I did years ago with `React` (tutorial that I should resume someday; please, forgive my laziness), I decided to put (and publish) some notes related to the new kid on the block, the JS Superset `TypeScript`.

Later, we will use `typescript` locally (feel free to install it as a global package: `npm install -g typescript`). But, for the moment, we consume [repl.it](https://repl.it/languages/typescript)

## Index

* [Intro](./00_0_intro.md)

* [Structural Typing](./00_1_0_structural-typing.md)

* Type Inference and Type Annotation
  * [Type Annotation](./01_1_1_type-inference-and-type-annotation.md#type-annotation-or-type-assignment)
  * [Type Inference](./01_1_1_type-inference-and-type-annotation.md#type-inference)
    * [Const Assertion](./01_1_1_type-inference-and-type-annotation.md#const-assertion)

* Types:
  * [String](./01_2_types-string-number-boolean-union.md#string)
  * [Number](./01_2_types-string-number-boolean-union.md#number)
  * [Boolean](./01_2_types-string-number-boolean-union.md#boolean)
  * [Union Types (OR)](./01_2_types-string-number-boolean-union.md#union-types)
    * [Discriminated Unions](./01_2_types-string-number-boolean-union.md#discriminated-unions)
  * [Intersection Types (AND)](./01_2_types-string-number-boolean-union.md#intersection-types)
  * [Null](./01_3_types-null-undefined-void-never-any-unknown.md#null)
  * [Undefined](./01_3_types-null-undefined-void-never-any-unknown.md#undefined)
  * [Void](./01_3_types-null-undefined-void-never-any-unknown.md#void)
  * [Never](./01_3_types-null-undefined-void-never-any-unknown.md#never)
  * [Any](./01_3_types-null-undefined-void-never-any-unknown.md#any)
  * [Unknown](./01_3_types-null-undefined-void-never-any-unknown.md#unknown)
  * [Object](./01_4_types-object-array-tuple-enum-set.md#object)
    * [Optional modifier (?)](./01_4_types-object-array-tuple-enum-set.md#optional-modifier)
    * [Non-null assertion operator (!)](./01_4_types-object-array-tuple-enum-set.md#non-null-assertion-operator)
  * [Array](./01_4_types-object-array-tuple-enum-set.md#array)
  * [Tuple](./01_4_types-object-array-tuple-enum-set.md#tuple)
  * [Enum](./01_4_types-object-array-tuple-enum-set.md#enum)
  * [Set](./01_4_types-object-array-tuple-enum-set.md#set)

* Type Alias and Interfaces:
  * [Alias](./01_5_type-alias-interfaces.md#type-alias)
    * [Implements](./01_5_type-alias-interfaces.md#implements)
    * [Utility types](./01_5_type-alias-interfaces.md#utility-types)
      * [Readonly](./01_5_type-alias-interfaces.md#readonly)
      * [Required](./01_5_type-alias-interfaces.md#required)
      * [Record](./01_5_type-alias-interfaces.md#record)
      * [Partial](./01_5_type-alias-interfaces.md#partial)
  * [Interfaces](./01_5_type-alias-interfaces.md#interfaces)
    * [Extends](./01_5_type-alias-interfaces.md#extends)
    * [Implements](./01_5_type-alias-interfaces.md#implements-1)

* Classes:
  * [Classes](./01_6_classes.md#classes)
... here

Functions:
  * [Functions](./01_7_functions.md#functions)

Type Assertions, Type Casting and Type Declaration
  * [Type Assertions](./02_0_type-assertions-casting-declaration.md#type-assertions)
  * [Type Casting](./02_0_type-assertions-casting-declaration.md#type-casting-or-type-coercion)
  * [Type Declaration](./02_0_type-assertions-casting-declaration.md#type-declarations)

Type Guards:
  * [Type Guards](./02_1_type-guards.md#type-guards)

Intersection types:
  * [Intersection Types](./02_2_intersection-types.md#intersection-types)

Generics:
  * [Generics](./03_0_generics.md#generics)