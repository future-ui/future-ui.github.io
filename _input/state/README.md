# State Management and Abstraction

When building long-lived UI, one of the most complex pieces is the
state of the application. React provides two core ways to manage
State, `this.state` and `this.props`. We will also talk about a third
way to manage state: Redux. It turns out that the way elements
abstract functionality has a large implication for how state is
managed.

As we mentioned before, one of the key differences between
`this.props` and `this.state` is where the data gets
managed. `this.props` gets passed in to an element from
"outside". This means that props aren't controlled by the element
displaying them.

## PropTypes

It is a good idea to declare `propTypes` for every element which takes
props. There are a number of benefits to doing this including
documentation and the fact that if you specify the types correctly,
React will warn you of data which is passed in that doesn't match the
expected signature.

One real-world and slightly messy application of propType warnings is
as a canary for changing APIs. If the propTypes match up with the
values that are expected to be received from an API, and that API
changes: The propTypes can serve as a late warning that the data is
not in the structure the application expects.
