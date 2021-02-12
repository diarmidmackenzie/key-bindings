# key-bindings
A-Frame component providing per-object Keyboard to Event Bindings.



### Overview

This is a simple A-Frame component that allows events to be triggered, or states to be set, on an entity in an A-Frame scene. on the basis of:

- A keypress
- An event on another entity, identified by ID.

Example use cases:

- Keyboard controls for an on-screen non-camera element
- Event-based controls (not positional controls) from VR controllers.
- Debugging / testing.  Easy to fire a named event on-demand (only works for simple events that don't require accompanying event data).

This is not intended for use for keyboard controls of camera elements.  For that use the built-in A-Frame WASD controls, or keyboard-controls in A-Frame Extras.



### Installation

Download key-bindings.js from this repo, and include like this:

```
<script src="key-bindings.js"></script>
```

or via CDN (taking care over version number)

```
<script src="https://cdn.jsdelivr.net/gh/diarmidmackenzie/key-bindings@v0.2-alpha/key-bindings.min.js"></script>
```

Not currently available through NPM etc.



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



{key1} values can be in one of two forms:

Keyboard events: they should be the names of keys as defined here: https://w3c.github.io/uievents-code/#keyboard-key-codes.  These are case-sensitive.

- Numbers are Digit1, Digit2 etc.
- Letters are KeyA, Key B etc.
- Other common keys include: Space, Escape, Enter, Control Left, ShiftLeft, Tab.

For events on other objects: they should be of the form {Entity ID}.{event} where Entity ID is the identifier for the entity that will generate the event (typically begins with a #), and event is the name of the event that will be monitored on that Entity.

- For example, you can monitor the A button on a the Right Hand controller by using a key value of "#rhand.abuttondown", where #rhand is the ID of an entity that also has the hand-controls component configured on it.

  

{event1} values should be the names of the events to be triggered.  Again, these are case-sensitive.

You can also set "bindings: none" to explicitly set no bindings (or clear previously configured bindings).



If you want to set a state, rather than emit an event, use an event string beginning with a $.  This will add the state when the key is pressed down, and remove it when the key press ends.  It also leads to the generation of stateadded and stateremoved events - more on states here.  https://aframe.io/docs/1.2.0/core/entity.html#addstate-statename.

For non-keypress events, there is no equivalent of "keydown", so states set will never be cleared.  The interface could be extended to have another control character to indicate "clear this state" - e.g. %.  That's not been implemented yet, but would be easy enough to do if required...



Note that when a key is held down, this will typically cause the keyDown event to fire multiple times, meaning that multiple events will be emitted.  The fact that a keypress is a repeat is encoded in the event object, so these could be filtered out in the downstream application if desired.  See: https://stackoverflow.com/questions/7686197/how-can-i-avoid-autorepeated-keydown-events-in-javascript



There is also a debug option available.  This will generate some additional output to console.log.

```
<a-entity key-bindings="debug: true; bindings: {key1}={event1},{key2}={event2}" </a-entity>
```



### Limitations 

Particular limitations to note:

- The component includes some code to handle Proxy controls:

  - This should allow you to connect input devices from your desktop to your mobile phone with WebRTC, using ProxyControls.js.
  - This code was inherited from keyboard-controls.js.  However this function is untested, and I have no idea whether or not it will work.
- No distribution by NPM yet.

  

### Acknowledgements

This component drew a lot of code from A-Frame Extras keyboard-controls.js.

https://github.com/n5ro/aframe-extras/blob/master/src/controls/keyboard-controls.js

The keyboard polyfill code comes (via keyboard-controls.js) from:

https://github.com/inexorabletash/polyfill/blob/master/keyboard.js



