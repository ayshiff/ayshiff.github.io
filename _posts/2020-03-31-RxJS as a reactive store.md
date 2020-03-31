---
layout: post
title: RxJS as a reactive store
---

An example of using RxJS as a reactive store in ReactJS.

**App.js**

```tsx
import React, { useState, useEffect } from "react";
import counterService from "./counterService";

const AddOne = () => (
  <button onClick={_ => counterService.increment()}>Increment</button>
);

const SubstractOne = ({ children }) => (
  <>
    <div>{children}</div>
    <button onClick={_ => counterService.decrement()}>Decrement</button>
  </>
);

const Counter = props => {
  // Initial value will come later
  const [count, setCount] = useState();
  const { message, children } = props;

  /**
   * Subscribe to the stream
   */
  useEffect(() => {
    counterService.subscribe(setCount);
  }, [count]);

  return (
    <>
      <h3>{message}</h3>
      <div>{count}</div>
      <div>{children}</div>
    </>
  );
};

const App = () => (
  <div className="App">
    <Counter message="High level">
      <AddOne />
    </Counter>
    <SubstractOne>
      <Counter message="Deep level" />
    </SubstractOne>
  </div>
);

export default App;
```

**counterService.ts**

```ts
import { BehaviorSubject } from "rxjs";

const counterSubject$ = new BehaviorSubject(0);

/**
 * This service emits all the values
 */
export default {
  /**
   * In order to receive stream values, we need to subscribe
   * @param {Function} setState Reference to the state changing function in the view
   */
  subscribe(setState) {
    return counterSubject$.subscribe(setState);
  },
  /**
   * Increment the counter and
   * publish the value to the stream
   */
  increment() {
    const v = counterSubject$.value;
    counterSubject$.next(v + 1);
  },
  /**
   * Decrement the counter and
   * publish the value to the stream
   */
  decrement() {
    const v = counterSubject$.value;
    counterSubject$.next(v - 1);
  }
};
```
