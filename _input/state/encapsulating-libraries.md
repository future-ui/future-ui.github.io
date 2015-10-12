# Using PropTypes to encapsulate third party libraries

`HumaneNumber` is nice because it provides an opinionated way to
display numbers in an application, but we could use it to greater
effect if we encapsulated [Numeral.js][numeral.js] in it's own
element. (note that we've skipped some of the Numeral API and focused
solely on rendering formatted strings).

```javascript
// HumaneNumber.js
import React, { Component, PropTypes } from 'react';
const { number, oneOf } = PropTypes;
import numeral from 'numeral.js';

export class Numeral extends Component {

  static propTypes = {
    format: string,
    num: number.isRequired
  }

  static defaultProps = {
    format: '0,0'
  }

  mkNumeral = () => {
    const { num, format } = this.props;
    return numeral(num).format(format);
  }

  render() {
    return (
      <span>{this.mkNumeral()}</span>
    )
  }
}

export default class HumaneNumber extends Component {

  static propTypes = {
    num: number.isRequired
  }

  render() {
    const { num } = this.props;
    return (
      <Numeral num={num} format='0,0' />
    )
  }
}
```

We can now import and use the simplified `HumaneNumber` or the more 
powerful `Numeral` element in another place in our application.

```javascript
import React, { Component, PropTypes } from 'react';
const { number } = PropTypes;
import HumaneNumber, { Numeral } from './HumaneNumber';

class TimeAndMoney extends Component {

  static propTypes = {
    days: number.isRequired,
    money: number.isRequired
  }

  render() {
    return (
      <div>
        <p>In <HumaneNumber num={days} /> days; you've made
        <Numeral num={money} format='($ 0.00 a)' /> dollars</p>
      </div>
    )
  }
}
```

If we rendered money in enough places in our application, it might
also make sense to build a `<Currency currency='usd'/>` element to
display different countries' currency. For now, the raw ability of the
`<Numerical/>` element serves any additional number-rendering need
that may crop up in our application.

Notice that the `<Numeral/>` element will behave exactly the same as
the `<HumaneNumber/>` element if you leave out the `format` because
the default format for `<Numeral/>` is the same. This brings up an
interesting design decision when building dumb elements. How much of
the API should you expose?

`<HumaneNumber/>` has a much more restrictive API. The benefits of
this include always knowing how a `<HumaneNumber/>` will treat a `num`
attribute and a smaller API surface area.

`<Numeral/>` provides more power, but has a larger API surface area
and is easily modified to show numbers differently.

Often, I'll opt for a more opinionated API such as `<HumaneNumber/>`
because it clearly expresses the intent I had when I built the
UI. There are no questions about whether I forgot a comma, etc in the
formatting string because of the restrictive API. More powerful APIs
such as `<Numeral/>` are *always* nice to have in case an unexpected
situation arises. One can even build more opinionated elements from
the more powerful elements. The API can be optionally restricted for
each additional element while the more powerful or harder-to-use API
is hidden for advanced users.
