# Props

Props are the consumer-side API for React Elements. This behaves very
similarly to the way attributes behave in normal html. For example,
here is an element which displays a heading:

```javascript
import React, { Component } from 'react';
import { render } from 'react-dom';

export default class Heading extends Component {
  render() {
    return <h1>Hello World</h1>;
  }
}
```

Which can be used as such:

```javascript
import Heading from './Heading';

export default class MyApp extends Component {
  render() {
    return <Heading />;
  }
}
```

We can modify it to accept an arbitrary heading in a few different
ways. We are going to add a new attribute to `Heading` called 

```javascript
import React, { Component } from 'react';
import { render } from 'react-dom';

export default class Heading extends Component {
  render() {
    return <h1>Hello World</h1>;
  }
}
```
