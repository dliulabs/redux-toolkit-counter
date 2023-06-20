# Getting Started with React with Reduxjs Toolkit App

This is a demo React app using Reduxjs-Toolkit.
We will create a small counter example.

The correct steps to use the latest reduxjs-toolkit are:

## Create a project with template

- using the `redux-typescript` template to start a project template.

```
yarn create react-app redux-toolkit-counter --template redux-typescript
```

## Create a Redux State Slice (the counterSlice)

[Create a Redux State Slice](https://redux.js.org/tutorials/quick-start#create-a-redux-state-slice)

`/src/features/counter/counter-slice.ts`

- define CounterState, initialState, counterSlice.

a slice is a reducer with a state and a set of actions.

- create a `counterSlice` under a folder called `features`

  - define the interface for the `CounterState`
  - then define an `initialState` for the counter `reducer`.
  - then we need to define a set of reducers: a set of actions (e.g. incrment, decrement, etc.)

  all of these can be done using the `createSlice()` function.

  The `counterSlice` should export the `CounterState`, the `counterSlice`, the actions, and then the `counterSlice.reducer`.

- empty the `/src` folder
- add back index.tsx/index.css, App.tsx/App.css, react-app-env.d.ts, logo.svg

## Create an empty Redux Store

We then create a `store` under a folder called `app`.
We will use the `configureStore({reducer: ...})` from the reduxjs-toolkit to create this store.

- Add Slice Reducers to the Store: [add the counterSlice.reducers to the store](https://redux.js.org/tutorials/quick-start#add-slice-reducers-to-the-store)

The store should export the `store`, the `store.dispatch` and the `RootState`:

```typescript
export type AppDispatch = typeof store.dispatch;
export type RootState = ReturnType<typeof store.getState>;
```

[create a redux store](https://redux.js.org/tutorials/quick-start#create-a-redux-store)

## Provide the Redux Store to React

The way to wire the store to the app is to import the `store` and the `Provider` the wrap the store inside of the provider as in:

```typescript
import App from "./App";
import { store } from "./app/store";
import { Provider } from "react-redux";

const el = document.getElementById("root");
const root = ReactDOM.createRoot(el!);
root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

The `<App />` will then render the `<Counter />` redux component.

At this time, you should be able start the app with `yarn start` and see the state in the `Redux DevTools`.

[Wire the index.tsx to use `Provider` and `store`](https://redux.js.org/tutorials/quick-start#provide-the-redux-store-to-react)

## Exporting the Redux Hooks

Create a file called `hooks.ts` under the foler `/app`.

Export an app-specific dispatch hook `useAppDispatch` and an app-specific selector hook `useAppSelector`

```typescript
import { TypedUseSelectorHook, useDispatch, useSelector } from "react-redux";
import { RootState, AppDispatch } from "./store";

export const useAppDispatch = () => useDispatch<AppDispatch>();
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector;
```

## Create a React component \<Counter /> using the Redux hooks

- replace a traditional `useState()` with `useAppSelector()` and `useAppDispatch()`.

  - instead of using a state variable `count`, we will use `useAppSelector()` to get the store value.
  - instead of using `setCount` state hook, we will use `dispatch` to call an action.

```typescript
const [incrementAmount, setIncrementAmount] = useState("2");
const count = useAppSelector((state) => state.counter.value);
const dispatch = useAppDispatch();
console.log(count);
```

## Call the Redux component from the \<App />

```typescript
import { Counter } from "./features/counter/Counter";

<Counter />;
```
