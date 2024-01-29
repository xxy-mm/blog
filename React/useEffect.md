# useEffect

## When exactly does React clean up an effect?

The cleanup function runs not only during unmount, but before every re-render with changed dependencies. Additionally, in development, React runs setup+cleanup one extra time immediately after component mounts.

two points:

- during component unmount
- before every re-render with changed dependencies.

## When will the effect rerun?

**note: all effects will run after component mount for the first time.**

### re-run cases

- effect has dependencies: after the value of any of its dependencies has changed.

```tsx
useEffect(() => {}, [dep1, dep2, ...]);
```

- effect has dependencies, but is empty: never,the clean-up will run just during the component unmount.

```tsx
useEffect(() => {
  // ...
  return () => {
    // ...
  };
}, []);
```

- effect does not have dependencies: every re-render

```tsx
useEffect(() => {});
```
