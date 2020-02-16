---
layout: post
title: Marble Testing - Redux Observables Epics
---

This example will show you how I manage to test my Redux Observable Epic.

You have an input element which will dispatch an `InputChanged` action when the user is typing.
Then the action will be catched inside the `inputEpic` and will emit the `load` action from the source Observable after 1 second.

**search.epic.ts**

```ts
import { Observable, timer, of } from "rxjs";
import {
  mergeMap,
  switchMap,
  concatMap,
  catchError,
  debounceTime
} from "rxjs/operators";
import {
  SearchActions,
  SearchTypes,
  searchActions
} from "../actions/search.action";
import { Epic, ofType, combineEpics } from "redux-observable";
import { SearchState } from "../store/search.reducer";
import { dependencies } from "../app.store";
import { AjaxResponse, AjaxError } from "rxjs/ajax";
import { URLS } from "../const/urls";

export const inputEpic: Epic = (
  action$: Observable<SearchActions>,
  state$: Observable<SearchState>,
  { ajax }: typeof dependencies
): Observable<SearchActions> => {
  return action$.pipe(
    ofType(SearchTypes.InputChanged),
    debounceTime(1000),
    switchMap((action: any) => of(searchActions.load(action.input)))
  );
};

export const searchEpic: Epic = (
  action$: Observable<SearchActions>,
  state$: Observable<SearchState>,
  { ajax }: typeof dependencies
): Observable<SearchActions> => {
  return action$.pipe(
    ofType(SearchTypes.Load),
    switchMap((action: any) => {
      return ajax({ url: URLS.search, method: "GET" }).pipe(
        concatMap((ajaxRes: AjaxResponse) => {
          return of(searchActions.success(action.input));
        }),
        catchError((err: AjaxError) => {
          return of(searchActions.fail(err));
        })
      );
    })
  );
};

export const searchEpics = combineEpics(searchEpic, inputEpic);
```

**search.epic.spec.ts**

```ts
import { TestScheduler } from "rxjs/testing";
import { searchEpics } from "./search.epic";
import { searchActions } from "../actions/search.action";

describe("SearchEpic", () => {
  let testScheduler: TestScheduler;

  beforeEach(() => {
    testScheduler = new TestScheduler((actual, expected) => {
      expect(actual).toEqual(expected);
    });
  });

  it("should trigger loading once the user stop typing", () => {
    const marbles = {
      i: "-ab--------", // input action
      r: "--t--------", // api response
      o: "-- 1s o" // output action
    };

    const values = {
      a: searchActions.inputChanged("test1"),
      b: searchActions.inputChanged("test2"),
      o: searchActions.load("test2"),
      t: "test"
    };

    testScheduler.run(({ hot, cold, expectObservable }) => {
      const action$ = hot(marbles.i, values) as any;
      const dependencies = {
        ajax: ({ url, method }: { url: string; method: string }) =>
          cold(marbles.r, values)
      };
      const state$ = null as any;
      const output$ = searchEpics(action$, state$, dependencies);
      expectObservable(output$).toBe(marbles.o, values);
    });
  });

  it("should load the corresponding inputs", () => {
    const marbles = {
      i: "-ab", // input action
      r: "---t", // api response
      o: "-----o" // output action
    };

    const values = {
      a: searchActions.load("test1"),
      b: searchActions.load("test2"),
      o: searchActions.success("test2"),
      t: "test"
    };

    testScheduler.run(({ hot, cold, expectObservable }) => {
      const action$ = hot(marbles.i, values) as any;
      const dependencies = {
        ajax: ({ url, method }: { url: string; method: string }) =>
          cold(marbles.r, values)
      };
      const state$ = null as any;
      const output$ = searchEpics(action$, state$, dependencies);
      expectObservable(output$).toBe(marbles.o, values);
    });
  });
});
```
