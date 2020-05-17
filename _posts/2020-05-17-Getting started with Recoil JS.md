---
layout: post
title: Getting Started with Recoil JS
---

A few days ago, recoil JS came out introduced by his author at the [React Europe livestream](https://youtu.be/_ISAA_Jt9kI).

It lets you create data-flow graph applications driven by flexible shared state. It introduces two notions: **atoms** which contains the truth for our application state and **selectors** which represents a piece of derived state (from the recoil docs: *You can think of derived state as the output of passing state to a pure function that modifies the given state in some way.*).

Here is an example showing the power of the library:

```js
import React, { useState } from "react";
import {
  RecoilRoot,
  atom,
  selector,
  useRecoilState,
  useRecoilValue
} from "recoil";

// Here we create our atom
const itemsState = atom({
  key: "itemsState",
  default: []
});

// Here we create our selectors

// Selector returning the length of the itemsState array
const itemsStateLength = selector({
  key: "itemsStateLength",
  get: ({ get }) => get(itemsState).length
});

// Selector returning the most present item of the itemsState array
const mostPresentItemState = selector({
  key: "mostPresentItemState",
  get: ({ get }) => {
    const items = get(itemsState);
    const occurrences = items.reduce((obj, item) => {
      obj[item] = (obj[item] || 0) + 1;
      return obj;
    }, {});
    let maxSeenSoFar = 0;
    let maxSeenSoFarValue = null;
    for (const [key, value] of Object.entries(occurrences)) {
      if (value > maxSeenSoFar) {
        maxSeenSoFarValue = key;
        maxSeenSoFar = value;
      }
    }
    return maxSeenSoFarValue;
  }
});

// Our util function to get a random integer
const getRandomInt = max => Math.floor(Math.random() * Math.floor(max));

// Our main component 
const MyComponent = () => {
  const [items, setItems] = useRecoilState(itemsState);
  const itemsLength = useRecoilValue(itemsStateLength);
  const mostPresentItem = useRecoilValue(mostPresentItemState);

  const [localItems, setLocalItems] = useState([]);

  return (
    <div style={{ border: "solid", padding: "10px", margin: "10px" }}>
      <button onClick={() => setItems([...items, getRandomInt(9)])}>
        Add item to recoil state
      </button>
      <span> - </span>
      <button onClick={() => setLocalItems([...localItems, getRandomInt(9)])}>
        Add item to component state
      </button>
      <hr />
      <div>
        <b> Recoil State </b>
      </div>
      <div> Items list: {items}</div>
      <div> Items list length: {itemsLength}</div>
      <div> Most present item: {mostPresentItem}</div>
      <hr />
      <div>
        <b> Component State </b>
      </div>
      <div> Items list: {localItems}</div>
      <div> Items list length: {localItems.length}</div>
    </div>
  );
};

// Our default component
export default () => {
  return (
    <RecoilRoot>
      <MyComponent />
      <MyComponent />
    </RecoilRoot>
  );
};

```

You can find this working example [here](https://codesandbox.io/s/recoil-poc-pkdm4?file=/src/App.js).   
Others articles will follow concerning other aspects of the library: [Asynchronous Data Queries](https://recoiljs.org/docs/guides/asynchronous-data-queries)...