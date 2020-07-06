---
layout: post
title: TypeScript 4.0 Beta
---

A few days ago, TypeScript 4.0 beta was released. This beta introduces some new changes. 
Don't forget that TypeScript never claimed to follow semantic versioning, so breaking changes DO NOT imply major versions. 

This article will briefly cover some of these new additions on the typing side.

I was mainly inspired by [this article](https://devblogs.microsoft.com/typescript/announcing-typescript-4-0-beta/).

## Labeled Tuple Elements

This is a more efficient way to describe the elements in a tuple.
You can now label the elements of your tuples.

Before:

```ts
function foo(): [number, number];
```

After:

```ts
function foo(): [a: number, b: number];
```

You can also take rest element and optional element:

```ts
type Foo = [first: number, second?: string, ...rest: any[]];
```

This addition only make usage of tuples like these far clearer.

## `unknown` on `catch` Clause Bindings

`catch` clause variables where always types as `any`.

```ts
try {
    // ...
}
catch (x) {
    // x has type 'any'
}
```

You can now specify the type of `catch` clause variable as `unknow` which is safer than `any` because you have to type-check your variables before operating on them:

```ts
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

## Forward declarations

You can declare a placeholder type that is not yet implemented.

Here’s an example from the proposal:

```ts
// constraints
exists type Foo extends { hello: string };

// type parameters
exists type Foo<T>;

// both!
exists type Foo<T, U> extends { toString(): string };
```

## Short-Circuiting Assignment Operators

TypeScript 4.0 comes with some JS proposal like the [proposal-logical-assignment](https://github.com/tc39/proposal-logical-assignment) which lets you do:

```ts
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

## Variadic Tuple Types

This introduces the ability for tuple types to have spreads of generic types.

```ts
// Variadic tuple elements

type Foo<T extends unknown[]> = [string, ...T, number];

type T1 = Foo<[boolean]>;  // [string, boolean, number]
type T2 = Foo<[number, number]>;  // [string, number, number, number]
type T3 = Foo<[]>;  // [string, number]
```

You ca read the the [PR here](https://github.com/microsoft/TypeScript/pull/39094).

## Class property inference from constructors

TypeScript will be able to infer assignments in constructor of properties of types that have no type annotations or initializers.

In this example, control flow analysis will determine the type of `prop` to be `string | number` based on the `this.prop` assignments in the constructor.

```ts
// Compile with --noImplicitAny
class Example {
  prop; // string | number
  constructor(arg: boolean ) {
    if (arg) {
      this.prop = 'test'
    } else {
      this.prop = 3;
    }
  }

```

I hope this article was useful to you ! Thanks for reading !