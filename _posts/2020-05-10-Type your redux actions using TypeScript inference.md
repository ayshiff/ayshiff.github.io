---
layout: post
title: Type your redux actions using TypeScript inference
---

This article will show you a way to type your redux actions using Typescript inference.

Before we usually did the following thing:

**example1.action.ts**
```ts
import { Action } from 'redux';

export const enum ExampleTypes {
    SET_CONTENT = '[EXAMPLE] SET_CONTENT',
}

/* Define our actions */
export const ASetContent = (content: string): ISetContent => ({
    type: ExampleTypes.SET_CONTENT,
    content
});

/* Define our actions types */
export interface ISetContent extends Action {
    type: ExampleTypes.SET_CONTENT;
    content: string;
}

export type TExampleActions = ISetContent | ...;

```

Now, thanks to the TypeScript type inference we can do:

**core.type.ts**
```ts
export type ActionTypes<T> = T extends { [key: string]: infer U }
  ? U extends (...args: any[]) => any
    ? ReturnType<U>
    : never
  : never;
```

We can then define our actions like this:

**example.action.ts**
```ts
import { ActionTypes } from "./core.type";

export enum ExampleTypes {
  SetContent = "[EXAMPLE] SET_CONTENT"
}

// Our object that produce our action creators
export const exampleActions = {
  setContent: (content: string) => ({ type: ExampleTypes.SetContent, content } as const)
};

// We can then type all of our actions with a single line
export type ExampleActions = ActionTypes<typeof exampleActions>;
```