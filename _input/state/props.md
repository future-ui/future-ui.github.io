## Props

To illustrate the role of Props in React's render(), we will revisit
the Counter example from earlier in this chapter. In the following
example, we initialize the state of our counter to 0 and provide two
functions to increment and decrement the counter. We also write a
second Element, whose job is to render a number in "human" form as
well as a third element, whose job is to render and dispatch state
changes.

```javascript
import React, { Component, PropTypes } from 'react';
const { number, func } = PropTypes;
import numeral from 'numeral.js';

class HumaneNumber extends Component {

  static propTypes = {
    num: number.isRequired
  }

  humanize(num) {
    return numeral(num).format('0,0');
  }

  render() {
    const { num } = this.props;
    return (
      <span>{this.humanize(num)}</span>
    )
  }
}

export class CounterController extends Component {

  static propTypes = {
    increment: func.isRequired,
    decrement: func.isRequired
  }

  render() {
    const { increment, decrement } = this.props;
    return (
      <section>
        <button onClick={decrement}>-</button>
        <button onClick={increment}>+</button>
      </section>
    );
  }
}

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
        <CounterController increment={this.increment}
                           decrement={this.decrement} />
        <p>Clicked <HumaneNumber number={this.state.count} /> Times</p>
      </div>
    )
  }

}
```

In building this set of elements, we have:

* Pushed event dispatch out to the leaf nodes while maintaining state
  control in a single location (the parent node). This means we only
  have one place to look for all of the possible ways state can be
  altered.
* Encapsulated the display of human-readable numbers into a
  [dumb element][dumb-elements].
* Separated the display of the control panel from the definition of
  state-adjusting logic.
* Clearly defined APIs for our dumb elements.

The parent node is specifying "This is what you can do to the state of
the application". Our child (dumb) elements are specifying their own
API contract using PropTypes, which details their requirements. The
child nodes are responsible for rendering the UI and defining how the
user interacts with the rendered UI.
