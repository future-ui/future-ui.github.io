
# Basics

## A Simple Component

The following component renders a heading. We can then use
`react-dom#render` to attach to the body of the `document`.

```javascript
import React, { Component } from 'react';
import { render } from 'react-dom';

export default class Simple extends Component {
  render() {
    return <p>Hello World</p>;
  }
}
```

```javascript
render(<Simple/>, document.body);
```

To see this component in action, run the following:

```bash
git clone git@github.com:future-ui/basics.git
cd basics && npm install
npm start
```

then go to `localhost:3000`

The example is hot-reloadable, which means that you can edit the
`src/App.js` file and see the changes in the browser immediately. You
should play around a bit and see what happens.

## A More Complex Example

We want to display a counter which we can adjust using various
buttons.

```javascript
import React, { Component } from 'react';

export default class Counter extends Component {

  state = {
    count: 0
  }

  increment = (e) => {
    const { count } = this.state;
    this.setState({
      count: count + 1
    });
  }

  decrement = (e) => {
    const { count } = this.state;
    this.setState({
      count: count - 1
    });
  }

  render() {
    return (
      <div>
        {this.renderControls()}
        <section>
          <h1>My Awesome Counter!</h1>
          <p>Counters are an integral part of counting things!</p>
        </section>
      </div>
    )
  }

  renderControls = () => {
    const { count } = this.state;
    return (
      <section>
        <button onClick={this.decrement}>-</button>
        <span>{count}</span>
        <button onClick={this.increment}>+</button>
      </section>
    );
  }
}
```

If you take the above example and paste it in to the App.js file from
before, you will see it render roughly as:

```html
<div data-reactid=".0">
  <section data-reactid=".0.0">
    <button data-reactid=".0.0.0">-</button><span data-reactid=
    ".0.0.1">7</span><button data-reactid=".0.0.2">+</button>
  </section>

  <section data-reactid=".0.1">
    <h1 data-reactid=".0.1.0">My Awesome Counter!</h1>

    <p data-reactid=".0.1.1">Counters are an integral part of counting
    things!</p>
  </section>
</div>
```

Each of the `data-reactid`s is a node in the tree.

## render

[render][React#render] is the most common function to be written on a
React Element, partially because it is a `required` function. A
`render()` function uses `props` and `state` to return a virtual
representation of a node.

In the following case, we ignore `this.props` and `this.state` and
instead render a constant result node representing a paragraph tag
with some text.

```javascript
class SimpleRender extends Component {
  render() {
    return (
      <p>Some Content</p>
    )
  }
}
```

Moving up in complexity, we can use both `this.props` and `this.state`
to return a more complex element.

```javascript
class ComplexRender extends Component {

  render() {
    const { name } = this.props;
    const { age } = this.state;
    return (
      <div>
        <h3>{name}</h3>
        <p>{name} is {age} years old.</p>
     </div>
    )
  }

}
```

As shown in the code above, the usage of state and props is incredibly
similar. The difference between the two is how (and where) the data is
managed. We go into this more in the chapter on State Management.

## JSX

[JSX][jsx] is an XML-like extension to ECMAScript which is currently a
Draft Speficiation. JSX looks a lot like HTML, but it has some crucial
differences. For one, JSX transforms to JavaScript. An example of this
transform, given by the React docs is shown below.

```javascript
// Input (JSX)
var app = <Nav color="blue" />;
```

```javascript
// Output (JS):
var app = React.createElement(Nav, {color:"blue"});
```

Our more complex example from before (`ComplexRender`) transforms into
the following render function when using [babel][babel] for the
transform.

```javascript
function render() {
  var name = this.props.name;
  var age = this.state.age;

  return React.createElement(
    "div",
    null,
    React.createElement(
      "h3",
      null,
      name
      ),
    React.createElement(
      "p",
      null,
      name,
      " is ",
      age,
      " years old."
    )
  );
}
```

Knowing that JSX is transformed into JavaScript enables us to
understand one of the restrictions of our render function: A render
function can only have a single JSX root node as the return
value. This is because of the fact that JSX transforms into JS, which
means returning multiple root nodes would mean the same thing as
returning multiple functions.

