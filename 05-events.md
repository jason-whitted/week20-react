# Events

We've learned about a few different ways to add events.

```html
<button id="abc" onclick="alert('hi');">click me</button>
```

```html
<button id="def">click me</button>
<script>
  // DOM
  const el = document.getElementById("def");
  el.addEventListener("click", function (event) {
    alert("hi");
  });
</script>
```

```js
<button id="ghi">click me</button>
<script>
// jQuery
$("#ghi").on("click", function(event) {
  alert("hi");
});
</script>
```

React makes binding to events even easier.

```js
const btn = <button onClick={event => alert("hi!")}>click me</button>;
```

https://reactjs.org/docs/events.html