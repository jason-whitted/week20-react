# Components

User-defined components are extremely empowering. React makes it extremely easy to develop reusable components.

There are two main types of components in React:

- Class Components
- Function Components (Stateless Functional Components)

Both components will have access to `props` (attributes sent to the component).

```js
// Class Component
class Thing1 extends React.Component {
  render() {
    return <div>Thing 1</div>;
  }
}

// Function Component
const Thing2 = () => <div>Thing 2</div>;

const things = (
  <div>
    <Thing1 />
    <Thing2 />
  </div>
);
```

This example is a perfect opportunity for us to demonstrate reuse. The only difference in the output of `Thing1` and `Thing2` is a number. We could create a single `Thing` and pass in a property for the number.

```js
// Class Component
class Thing extends React.Component {
  render() {
    const { num } = this.props;
    return <div>Thing {num}</div>;
  }
}
```

```js
// Function Component
const Thing = ({ num }) => <div>Thing {num}</div>;
```

```js
const things = (
  <div>
    <Thing num="1" />
    <Thing num={2}></Thing>
  </div>
);
```

## Class Components

Class component's don't just have the `render` method. They have access to the full lifecycle methods:

- Mounting
  - constructor()
  - static getDerivedStateFromProps()
  - render()
  - componentDidMount()
  - UNSAFE_componentWillMount()
- Updating
  - static getDerivedStateFromProps()
  - shouldComponentUpdate()
  - render()
  - getSnapshotBeforeUpdate()
  - componentDidUpdate()
  - UNSAFE_componentWillUpdate()
  - UNSAFE_componentWillReceiveProps()
- Unmounting
  - componentWillUnmount()
- Error Handling
  - static getDerivedStateFromError()
  - componentDidCatch()

Needless to say -- it's been hard for new React developers to grasp the complexity of the component lifecycle!

In addition to `this.props`, Class Components also have `this.state` for each component to manage their state.

When a component's props change it is rerendered. The same thing holds true when the state is changed.

> **What is the difference between state and props?**
>
> `props` (short for “properties”) and `state` are both plain JavaScript objects. While both hold information that influences the output of render, they are different in one important way: `props` get passed to the component (similar to function parameters) whereas `state` is managed within the component (similar to variables declared within a function).
>
> https://reactjs.org/docs/faq-state.html#what-is-the-difference-between-state-and-props

Understanding the difference between props and state can also be a point of contention for new React developers. Not to mention if done improperly the component may render way too much -- **_or not at all_**. Yikes!

## Function Components

Stateless Functional Components are the "new" way of creating components. They are far simpler!

They are simply the render function. You receive the `props` as input and you return what should be rendered as output.

It's just `props`. There's no `this.state`. There's no `this.props`. There's no `this.context`. Heck, there's no `this` involved at all. Just `props`.

There are no other lifecycle methods you need to worry about. It's just the `render` method.

Far, far simpler. And anything that you can do in a class component you can do in a stateless functional component. _Almost._

NOTE: Error Boundaries require the `componentDidCatch` lifecycle method and therefore a class component is currently required. Error Boundaries are an advanced topic.
