# Component Communication

Let's create very simple application.

- The application should display two buttons.
- The first button's text should be "A"
- The second button's text should be "B"

## Creating the buttons

We could create two different button components:

```js
const ButtonA = () => {
  const clickHandler = (event) => {
    console.log("A", "was clicked");
  };
  return <button onClick={clickHandler}>A</button>;
};

const ButtonB = () => {
  const clickHandler = (event) => {
    console.log("B", "was clicked");
  };
  return <button onClick={clickHandler}>B</button>;
};
```

As soon as we create these buttons we can see that they are identical except for the text. Let's abstract that out so we can reduce this down to a single `Button` component.

```js
const Button = ({ text }) => {
  const clickHandler = (event) => {
    console.log(text, "was clicked");
  };
  return <button onClick={clickHandler}>{text}</button>;
};
```

## Creating the App

```js
const App = () => {
  return (
    <div>
      <Button text="A" />
      <Button text="B" />
    </div>
  );
};
```

Perfect! This also demonstrates the first direction of communicating. A parent component (`App` in this example) can communicate information down to the child components by passing them as `props` to the children.

But now we have a new requirement.

```js
const App = () => {
  const partyTime = () => {
    console.log("It's time to party!");
  };

  return (
    <div>
      <Button text="A" />
      <Button text="B" />
    </div>
  );
};
```

We would like `partyTime` to be called when either of the buttons get clicked. Now we have a situation where a child component needs to communicate to the parent. How do we do that?

This is an inversion of control issue. The child component doesn't need to know the implementation details of the parent. It just needs to have some way to communicate back up the chain. We can do this by passing a callback function to the child.

```js
const App = () => {
  const partyTime = () => {
    console.log("It's time to party!");
  };

  return (
    <div>
      <Button text="A" onClick={partyTime} />
      <Button text="B" onClick={partyTime} />
    </div>
  );
};
```

The `App` is passing an `onClick` property to the `Button` component. Now we need to update the `Button` component to call this callback function.

```js
const Button = ({ text, onClick }) => {
  const clickHandler = (event) => {
    console.log(text, "was clicked");
    onClick();
  };
  return <button onClick={clickHandler}>{text}</button>;
};
```

If we didn't care about the `console.log` that we have in there, this could be reduced to:

```js
const Button = ({ text, onClick }) => {
  return <button onClick={onClick}>{text}</button>;
};
```
