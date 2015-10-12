# Rendering

In this book, we will be focusing on React for controlling the
rendering of our applications. According to the React site, React is:

> A JavaScript library for building user interfaces

Notice that there is no mention of the DOM because React is not tied
to a specific render target. In practice, this means we can render to
DOM, SVG, Canvas and even native iOS components. Most importantly,
React is a component model for abstractions.

## Virtual DOM

The abstraction used which allows us to render to multiple targets is
referred to as the Virtual DOM. Simply speaking, the Virtual DOM is a tree
structure which allows us to diff against previous versions of our
rendered application.

In practice one of the benefits is that we have to worry less about
DOM insertion optimizations such as batching updates. A spec-compliant
synthetic event system means that bubbling and capturing works the
same across browsers.

The React docs explain the implications well:

> **Event delegation:** React doesn't actually attach event handlers to
> the nodes themselves. When React starts up, it starts listening for
> all events at the top level using a single event listener. When a
> component is mounted or unmounted, the event handlers are simply
> added or removed from an internal mapping. When an event occurs,
> React knows how to dispatch it using this mapping. When there are no
> event handlers left in the mapping, React's event handlers are
> simple no-ops. To learn more about why this is fast, see [David
> Walsh's excellent blog post](http://davidwalsh.name/event-delegate).
