# Play Canvas intergration with Origami Engine

[PlayCanvas](https://github.com/playcanvas/engine) is an open-source WebGL game engine with browser-based [Editor](https://playcanvas.com/) in the cloud. PlayCanvas projects can be published as ZIP folders containing index.html, javascript files, graphic assets and audio, and can be embedded as separate views in Origami Design, allowing them to become part of a native app such as digital magazine, interactive presentation, and so on.

### Contents
- Getting started
- Exposing actions from PlayCanvas to Origami Engine
- Listening to events from Origami Engine inside PlayCanvas
- Saving state

### Getting started
TODO

### Exposing actions from PlayCanvas to Origami Engine
As of now, you don't need to do anything extra to expose functionality from PlayCanvas project - it is available in Origami Design by default. Every function in every script can be called from Origami Engine, as long as this script is attached to some entity in the root of PlayCanvas project hierarchy. Here is what it would look like:

1. Create an empty entity in PlayCanvas scene as a direct Root child, and name it Foo
2. Create a new script called Bar.js, and attach it to this entity
3. Make sure instantiated class and script id also read as Bar, not bar
4. Create a function on Bar prototype and name it doSomething
5. Implement desired functionality inside it, and make sure it doesn't take any arguments

Now, to call this action from Origame Engine, you would need to specify a Trigger Action with the following parameters:
```
Entity: Foo
Script: Bar
Action: doSomething
```
Sending arguments inside actions isn't supported at the moment, but may be implemented in the future.







