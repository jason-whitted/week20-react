# Hooks

> Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.<br/>https://reactjs.org/docs/hooks-intro.html

This means that "Stateless Functional Components" can actually be stateful. We'll see what that means in a bit.

Here's a list of built-in hooks:

- Basic Hooks
  - useState
  - useEffect
  - useContext
- Additional Hooks
  - useReducer
  - useCallback
  - useMemo
  - useRef
  - useImperativeHandle
  - useLayoutEffect
  - useDebugValue

## Rules

Hooks are freaking magic. And this magic tends to confuse people when they first start using them. If you screw up your hooks it could prevent your component from properly re-rendering.

First things first -- there are some rules that you have to follow or you're gonna have a bad time.

1. **Only Call Hooks at the Top Level**
   - Don’t call Hooks inside loops, conditions, or nested functions
2. **Only Call Hooks from React Functions**
   - Don’t call Hooks from regular JavaScript functions
   - Do call Hooks from React function components
   - Do call Hooks from custom Hooks
3. **Any Custom Hooks should be named starting with `use`**
   - This is because there are eslint rules that will try to save your bacon

```js
const useBippityBoo = () => {
  return useState();
};

const jack = () => {
  return useState();
};

const Thing = ({ array }) => {
  const bippityboo = useBippityBoo();
  const flap = jack(); // BAD! #3

  if (bippityboo) {
    useFoo(); // BAD! #1
  }

  array.forEach((n) => {
    useBar(); // BAD! #1
  });

  const onClick = () => {
    useSnafu(); // BAD! #1
  };

  return <div onClick={onClick}>Hooks</div>;
};

$(() => {
  const value = useState(); // BAD! #2
});
```
