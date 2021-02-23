# JSX

> JSX, or JavaScript XML, is an extension to the JavaScript language syntax. Similar in appearance to HTML, JSX provides a way to structure component rendering using syntax familiar to many developers.<br/>**- Wikipedia**

## Empty elements

```js
const empty = <div />;

// const invalid = <div>;
// invalid!
```

## Nested elements

```js
const nested = (
  <div>
    <span>Hello</span>
    <hr />
  </div>
);
```

NOTE: It's considered best-practice to put parenthesis around multiple lines of jsx.

## User-defined components

Built-in components (HTML) start with a lowercase letter.

User-defined components start with an uppercase letter.

```js
const example = (
  <div>
    <Hello />
    <hr />
    <World />
  </div>
);
```

## Attributes

```js
// string attributes
const input = <input type="text" />;
```

In HTML all properties are strings.

```html
<div id="14"></div>
<script>
  const el = document.getElementById(14);
  console.log(`${typeof el.id} ${el.id}`);
  // string 14
</script>
```

But not in React!

```js
// variables
const first = "Jane";
const last = "Doe";
const age = 24;
const onClick = () => alert("Clicked!");
const person = (
  <Person firstName={first} lastName={last} age={age} onClick={onClick} />
);
```

You can even use object-spread syntax with properties.

```js
const data = {
  first: 'Jane',
  last: 'Doe',
  age: 14,
  onClick: () => alert('Clicked!');
};
const person = <Person {...data} />;
//             <Person first={data.first} last={data.last} age={data.age} onClick={data.onClick} />
```

```js
// boolean-true shorthand
const btn1 = <button disabled={false}>One</button>;
const btn2 = <button disabled>Two</button>;
//           <button disabled={true}>Two</button>
```

NOTE: JSX isn't actually HTML. It's transpiled into javascript. Because of this there are a few reserved words that we can't use in JSX.

```html
<div class="input-group">
  <label for="txtName">Name:</label>
  <input type="text" id="txtName" class="form-control" />
</div>
```

We can't just copy & paste the html and use it in JSX.

```js
const reserved = (
  <div className="input-group">
    <label htmlFor="txtName">Name:</label>
    <input type="text" id="txtName" className="form-control" />
  </div>
);
```
