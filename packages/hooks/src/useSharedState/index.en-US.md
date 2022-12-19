---
nav:
  path: /hooks
---

# createSharedState

A high-performance global state hook based on useSyncExternalStore, which is almost the same as useState

## Examples

```typescript react
import { createSharedState } from 'ahooks';

const useCount = createSharedState({ count1: 0, count2: 0 });

function Counter1() {
  const [count, setCount] = useCount();

  return (
    <button onClick={() => setCount((prev) => ({
      count1: prev.count1 + 1,
      count: prec.count2,
    }))}>count1 is {count.count1}</button>
  )
}

function Counter1() {
  // As Counter1 increments, Counter2 will not re-render
  const [count2] = useCount((state) => state.count2);
  console.log('Counter2 rendered')
  return (
    <button>count2 is {count2}</button>
  )
}

function App() {
  return (
    <>
      <Counter1 />
      <Counter2 />
    </>
  )
}

```

### Default usage

<code src="./demo/demo1.tsx" />

## API

```typescript
export function createSharedState<Snapshot = undefined>(): <
  Selection = undefined,
>(
  selector?: (state: Snapshot) => Selection,
) => [
  (Selection extends undefined ? Snapshot : Selection) | undefined,
  Dispatch<SetStateAction<Snapshot | undefined>>,
];
export function createSharedState<Snapshot>(
  initialState: Snapshot | (() => Snapshot),
): <Selection = undefined>(
  selector?: (state: Snapshot) => Selection,
) => [
  Selection extends undefined ? Snapshot : Selection,
  Dispatch<SetStateAction<Snapshot>>,
];
```