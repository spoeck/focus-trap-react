# focus-trap-react

A React component that traps focus.

This component is a light wrapper around [focus-trap](https://github.com/davidtheclark/focus-trap),
tailored to your React-specific needs.

You might want it for, say, building an accessible modal?

## What it does

[Check out the demo](http://davidtheclark.github.io/focus-trap-react/demo/).

Please read [the focus-trap documentation](https://github.com/davidtheclark/focus-trap) to understand what a focus trap is, what happens when a focus trap is activated, and what happens when one is deactivated.

This module simply provides a React component that creates a focus trap.

- The focus trap automatically activates when mounted (by default, though this can be changed).
- The focus trap automatically deactivates when unmounted.

## Installation

```
npm install focus-trap-react
```

## Browser Support

IE9+

Why?
Because this module's core functionality comes from focus-trap, which uses [a couple of IE9+ functions](https://github.com/davidtheclark/tabbable#browser-support).

## Usage

Read code in `demo/` (it's very simple), and [see how it works](http://davidtheclark.github.io/focus-trap-react/demo/).

Here's one simple example:

```js
var React = require('react');
var FocusTrap = require('focus-trap-react');

var DemoOne = React.createClass({
  getInitialState: function() {
    return {
      activeTrap: false,
    };
  },

  mountTrap: function() {
    this.setState({ activeTrap: true });
  },

  unmountTrap: function() {
    this.setState({ activeTrap: false });
  },

  render: function() {
    var trap = (this.state.activeTrap) ? (
      <FocusTrap
        onDeactivate={this.unmountTrap}
        className='trap'
      >
        <p>
          Here is a focus trap <a href='#'>with</a> <a href='#'>some</a> <a href='#'>focusable</a> parts.
        </p>
        <p>
          <button onClick={this.unmountTrap}>
            deactivate trap
          </button>
        </p>
      </FocusTrap>
    ) : false;

    return (
      <div>
        <p>
          <button onClick={this.mountTrap}>
            activate trap
          </button>
        </p>
        {trap}
      </div>
    );
  },
});

React.render(<DemoOne />, document.getElementById('demo-one'));
```

Easy enough.

### Props

#### onDeactivate

Type: `Function`, *required*

This function is called when the `FocusTrap` deactivates. If, for example, a user hits Escape within the `FocusTrap`, the trap deactivates; and you need to tell it what to do next. The `FocusTrap` does not manage its own visible/hidden state: you do that.

#### initialFocus

Type: `String`, optional

By default, when the `FocusTrap` activates it will pass focus to the first element in its tab order. If you want that initial focus to pass to some other element (e.g. a Submit button at the bottom of a modal dialog), pass **the `id` of the element that should receive initial focus** when the `FocusTrap` activates.

See `demo/demo-two.jsx`.

#### active

Type: `Boolean`, optional

By default, the `FocusTrap` activates when it mounts. So you activate and deactivate it via mounting and unmounting. If, however, you want to keep the `FocusTrap` mounted *while still toggling its activation state*, you can do that with this prop.

See `demo/demo-three.jsx`.

#### className

Type: `String`, optional

A `className` for the `FocusTrap`'s DOM node.

#### id

Type: `String`, optional

An `id` for the `FocusTrap`'s DOM node.

#### tag

Type: `String`, Default: `'div'`, optional

An HTML tag for the `FocusTrap`'s DOM node.

#### style

Type: `Object`, optional

An inline style object ([in React fashion](https://facebook.github.io/react/tips/inline-styles.html)) for the `FocusTrap`'s DOM node.
