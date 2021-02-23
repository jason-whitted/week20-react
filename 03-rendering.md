# Rendering

```js
const example = (
  <div>
    <undefined>{undefined}</undefined>
    <null>{null}</null>
    <emptyString>{""}</emptyString>
    <string>{"string"}</string>
    <zero>{0}</zero>
    <true>{true}</true>
    <false>{false}</false>
    <function>{() => "hello"}</function>
    <emptyArray>{[]}</emptyArray>
    <array>{[5, "<hr/>"]}</array>
    {/*
      <date>{new Date()}</date>
      <emptyObject>{{}}</emptyObject>
    */}
  </div>
);
```

Would render:

```html
<div>
  <undefined></undefined>
  <null></null>
  <emptystring></emptystring>
  <string>string</string>
  <zero>0</zero>
  <true></true>
  <false></false>
  <function></function>
  <emptyarray></emptyarray>
  <array>5&lt;hr/&gt;</array>
</div>
```

You cannot render an object!

```js
const error = (
  <div>
    <date>{new Date()}</date>
    <emptyObject>{{}}</emptyObject>
  </div>
);
// Runtime error!
// Error: Objects are not valid as a React child. If you meant to render a collection of children, use an array instead.
```

## JavaScript Expressions

Use curly brackets to include javascript expressions.

```js
const text = "Name:";
const label = <label>{labelText}</label>;
```

```js
// ternary expressions
const upper = Date.now() % 2 === 0;
const label = <label>{upper ? "NAME" : "name"}</label>;
```

```js
// conditional rendering
const example = (
  <div>
    {text.startsWith("a") && <span>Aa</span>}
    {text === "hello" && <span>World</span>}
  </div>
);
```

NOTE: You **cannot** use statements in your JSX, because statements don't return anything.

```js
const noWorky = (
  <div>
    {
      // INVALID!
      if (text.startsWith("a")) {
        return <span>Aa</span>;
      } else if (text === "hello") {
        return <span>World</span>;
      }
    }
    {
      // INVALID!
      switch(text) {
        case 'hello':
          <span>World</span>
          break;
      }
    }
  </div>
);
// Compile-time error!
// Error: Expression expected.
```

## Children

Properties are passed to the component.

```js
const movie = (
  <Movie name="Nacho Libre" year={2006}>
    Berated all his life by those around him, a monk follows his dream and dons
    a mask to moonlight as a Luchador (Mexican wrestler).
  </Movie>
);
```

In this example we could deduce that `Movie` would receive props resembling:

```js
{
  name: 'Nacho Libre',
  year: 2006,
}
```

But what about the text "Berated all his life..." that is a child node of the element?

React passes this as a special `children` property. The `props` that `Movie` receives would contain `name`, `year`, and `children`.

A component can render it's children directly.

```js
const { name, year, children } = props;
const example = (
  <div>
    <b>{name}</b> <i>{year}</i>
    <br />
    {children}
  </div>
);
```

## Rendering

Most react application would send back an HTML file that looks something like:

```html
<html>
  <body>
    <div id="root"></div>
    <script src="bundle.js"></script>
  </body>
</html>
```

And the bundle.js file would have been created from an `index.js` entry point that looked something like:

```js
import ReactDOM from "react-dom";
// const ReactDOM = require('react-dom');

const App = () => <div>Hello World!</div>;

ReactDOM.render(<App />, document.getElementById("root"));
```

## Re-rendering

React tries to be really, really efficient. It only renders components whose `props` have changed. Don't worry if this confuses you. We haven't learned how to change prop values. Soon™.

## Collections

Imagine now that we have an array of strings.

```js
const names = ["Nacho", "Jane", "Billy"];
```

And we would like to render these like this:

```html
<ul>
  <li>Nacho</li>
  <li>Jane</li>
  <li>Billy</li>
</ul>
```

Since `names` is an array, we could use the `.map()` function to convert each name into an `li` tag.

```js
const names = ["Nacho", "Jane", "Billy"];
const list = (
  <ul>
    {names.map((name) => (
      <span>{name}</span>
    ))}
  </ul>
);
```

If we were to try to render this, we would get a warning printed out to the console.

```
Warning: Each child in a list should have a unique "key" prop.
```

This is because React is trying to be really, really efficient. It doesn't want to HAVE to re-render every child in a list. It can avoid having to if it could uniquely identify each entry. And this warning is telling us how to do that -- we just need to specify a `key` prop.

```js
const names = ["Nacho", "Jane", "Billy"];
const list = (
  <ul>
    {names.map((name) => (
      <span key={name}>{name}</span>
    ))}
  </ul>
);
```

NOTE: To work correctly, each `key` should be unique and unchanging for each item in the list. In this example if any of the names were duplicated we would get a different warning:

```
Warning: Encountered two children with the same key, `Nacho`. Keys should be unique so that components maintain their identity across updates. Non-unique keys may cause children to be duplicated and/or omitted — the behavior is unsupported and could change in a future version.
```

It's tempting to just use the index as the key. But this could cause unnecessary re-renders if an array is altered (insert, update, swaps, etc.)
