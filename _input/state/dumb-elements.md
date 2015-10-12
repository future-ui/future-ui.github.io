## Dumb Elements and propTypes

To see why the concept of props is so useful, we are going to explore
the concept of [Dumb Elements][dumb-elements]. In accordance with
@dan_abramov's definition of [Dumb Elements][dumb-elements], they are
elements which:

* Have no dependencies on the rest of the app, e.g. Flux actions or
  stores.
* Often allow containment via this.props.children.
* Receive data and callbacks exclusively via props.
* Have a CSS file associated with them.
* Rarely have their own state.
* Might use other dumb components.
* Examples: Page, Sidebar, Story, UserInfo, List.

Talking briefly about our `HumaneNumber` example, we have created an
element which abstracts the choice of "Which format do I use to
represent numbers in my application?". This has a number of benefits
including reducing the opportunity to use the wrong format and
reducing the mental burden of writing the UI. Reducing mental burdens,
even in this simple way, is critically important to opening up
opportunity to focus on business logic.

`propTypes` define the API supported by a dumb element. For example, by
looking at the following PropTypes, we can determine a fair bit of
information about the element we're using.

```javascript
static propTypes = {
  title: string.isRequired,
  isEligible: bool,
  age: number.isRequired
}
static defaultProps = {
  isEligible: false
}
```

The above element takes three possible attributes. `title` is a
`string`, and we have no good default value for a `title` so it's
required. We also have an `age` attribute, which is a required
`number`, and an `isEligible` attribute, which is an option
`boolean`. Notice how we're using `defaultProps` to fill in the gaps
for those properties which we don't require to be passed in when using
the element. `defaultProps` are a great way to reduce the noise on the
consumer's side when defining an element's API.
