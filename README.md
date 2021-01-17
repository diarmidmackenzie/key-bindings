# key-bindings
A-Frame component providing per-object Keyboard to Event Bindings.



### Overview

This is a simple A-Frame component that allows keyboard controls to be used to trigger events on any component in an A-Frame scene. 

Example use cases:

- Keyboard controls for an on-screen non-camera element
- Debugging / testing.  Easy to fire a named event on-demand (only works for simple events that don't require accompanying event data).

This is not intended for use for keyboard controls of camera elements.  For that use the built-in A-Frame WASD controls, or keyboard-controls in A-Frame Extras.



### Installation

Download key-bindings.js from this repo, and include like this:

```
<script src="key-bindings.js"></script>
```

Not currently available through CDN, NPM etc.



### Usage

See examples.html for some basic usage

include inside any entity like this:

```
<a-entity key-bindings="bindings: {key1}={event1},{key2}={event2}" </a-entity>
```

or via a mixin

```
<a-mixin id="mymixin" key-bindings="bindings: {key1}={event1},{key2}={event2}" </a-mixin>
<a-entity mixin="mymixin" </a-entity>
```

{key1} values should be the names of keys as defined here: https://w3c.github.io/uievents-code/#keyboard-key-codes.  These are case-sensitive.

- Numbers are Digit1, Digit2 etc.
- Letters are KeyA, Key B etc.
- Other common keys include: Space, Escape, Enter, Control Left, ShiftLeft, Tab.

{event1} values should be the names of the events to be triggered.  Again, these are case-sensitive.

There is also a debug option available.  This will generate some additional output to console.log.

```
<a-entity key-bindings="debug: true; bindings: {key1}={event1},{key2}={event2}" </a-entity>
```



### Limitations 

Particular limitations to note:

- The component detects keypresses when the key is pressed down.  It does not generate any further events when the key is released, and it also doesn't generate any additional events if the key is held down for a long time.
- The component includes some code to handle Proxy controls:

  - This should allow you to connect input devices from your desktop to your mobile phone with WebRTC, using ProxyControls.js.
  - This code was inherited from keyboard-controls.js.  However this function is untested, and I have no idea whether or not it will work.
- No distribution by CDN, NPM etc.  I don't yet have a minified version of the code available.

  

### Acknowledgements

This component drew a lot of code from A-Frame Extras keyboard-controls.js.

https://github.com/n5ro/aframe-extras/blob/master/src/controls/keyboard-controls.js

The keyboard polyfill code comes (via keyboard-controls.js) from:

https://github.com/inexorabletash/polyfill/blob/master/keyboard.js



