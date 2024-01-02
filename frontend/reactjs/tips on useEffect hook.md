### Don't overuse useEffect everywhere on the app
useEffect is not bad, but overused it can make the app became a mess, as the code became harder to read and maintain.

- Why?
  Since everthing is calling "useEffect" which made naming in code became unclear.
  Side-effect of "useEffect" may create unexpected re-render on the component.

- How to fix it?
  Create custom hook and implement useEffect hook inside of it for more readability.

### Remember to clean up

- always check whether the hook need a clean up function, or while the app run, it may cause mismatch state.
```
*sample clean up code

useEffect(() => {
  // Your effect
  return () => {
    // Cleanup
  }
}, [input])
```