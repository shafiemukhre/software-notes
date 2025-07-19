# React Snippets

## Components

### Fragment

`<Fragment>`, often used via `<>...</>` syntax, lets you group elements without a wrapper node.

```jsx
<>
  <OneChild />
  <AnotherChild />
</>
```

### Profiler

`<Profiler>` lets you measure rendering performance of a React tree programmatically.

```jsx
<Profiler id="App" onRender={onRender}>
  <App />
</Profiler>
```

### StrictMode

`<StrictMode>` lets you find common bugs in your components early during development.

```jsx
<StrictMode>
  <App />
</StrictMode>
```

### Suspense

`<Suspense>` lets you display a fallback until its children have finished loading.

```jsx
<Suspense fallback={<Loading />}>
  <SomeComponent />
</Suspense>
```

## Hooks

### useCallback

`useCallback` is a React Hook that lets you cache a function definition between re-renders.

```jsx
const cachedFn = useCallback(fn, dependencies);
```

### useContext

`useContext` is a React Hook that lets you read and subscribe to context from your component.

```jsx
const value = useContext(SomeContext);
```

### useDebugValue

`useDebugValue` is a React Hook that lets you add a label to a custom Hook in React DevTools.

```jsx
useDebugValue(value, format?)
```

### useDeferredValue

`useDeferredValue` is a React Hook that lets you defer updating a part of the UI.

```jsx
const deferredValue = useDeferredValue(value);
```

### useEffect

`useEffect` is a React Hook that lets you synchronize a component with an external system.

```jsx
useEffect(setup, dependencies?)
```

### useId

`useId` is a React Hook for generating unique IDs that can be passed to accessibility attributes.

```jsx
const id = useId();
```

### useMemo

`useMemo` is a React Hook that lets you cache the result of a calculation between re-renders.

```jsx
const cachedValue = useMemo(calculateValue, dependencies);
```

### useReducer

```jsx
const [state, dispatch] = useReducer(reducer, initialArg, init?)
```

### useRef

`useRef` is a React Hook that lets you reference a value that’s not needed for rendering.

```jsx
const ref = useRef(initialValue);
```

### useState

`useState` is a React Hook that lets you add a state variable to your component.

```jsx
const [state, setState] = useState(initialState);
```

### useSyncExternalStore

`useSyncExternalStore` is a React Hook that lets you subscribe to an external store.

```jsx
const snapshot = useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot?)
```

### useTransition

`useTransition` is a React Hook that lets you update the state without blocking the UI.

```jsx
const [isPending, startTransition] = useTransition();
```
