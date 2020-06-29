---
layout: post
title: TypeScript 4.0 Beta
---

A few days ago, TypeScript 4.0 beta was released. This beta introduces some new changes. 
Don't forget that TypeScript never claimed to follow semantic versioning, so breaking changes DO NOT imply major versions. 

This article will briefly cover these new additions on the typing side.

I was mainly inspired by [this article](https://devblogs.microsoft.com/typescript/announcing-typescript-4-0-beta/).

## Variadic Tuple Types



## Labeled Tuple Elements

You can now label the elements of your tuples.

Before:

```
function foo(): [number, number];
```

After:

```
function foo(): [a: number, b: number];
```

You can also take rest element and optional element:

```
type Foo = [first: number, second?: string, ...rest: any[]];
```

This addition only make usage of tuples like these far clearer.

## `/** @deprecated */` Support

This is a feature for the TypeScript's editing support. It will now be able to recognize when a declaration has been marked with a JSDoc comment => `/** @deprecated */`.

![vs-code](https://devblogs.microsoft.com/typescript/wp-content/uploads/sites/11/2020/06/deprecated_4-0.png)

## `unknown` on `catch` Clause Bindings

`catch` clause variables where always types as `any`.

```
try {
    // ...
}
catch (x) {
    // x has type 'any'
}
```

You can now specify the type of `catch` clause variable as `unknow` which is safer than `any` because you have to type-check your variables before operating on them:

```
try {
    // ...
}
catch (e: unknown) {
    if (typeof e === "string") {
        // We've narrowed 'e' down to the type 'string'.
        console.log(e.toUpperCase());
    }
}
```

## Short-Circuiting Assignment Operators

TypeScript 4.0 comes with some JS proposal like the [proposal-logical-assignment](https://github.com/tc39/proposal-logical-assignment) which lets you do:

```
a += b;
// Addition: equivalent to a = a + b

a -= b;
// Subtraction: equivalent a = a - b

a *= b;
// Multiplication: equivalent a = a * b

a /= b;
// Division: equivalent a = a / b

a **= b;
// Exponentiation: equivalent a = a ** b

a <<= b;
// Left Bit Shift: equivalent a = a << b
```

I hope this article was useful to you ! Thanks for reading !