# Play Canvas intergration with Origami Engine

[PlayCanvas](https://github.com/playcanvas/engine) is an open-source WebGL game engine with browser-based [Editor](https://playcanvas.com/) in the cloud. PlayCanvas projects can be published as ZIP folders containing index.html, javascript files, graphic assets and audio, and can be embedded as separate views in Origami Design, allowing them to become part of a native app such as digital magazine, interactive presentation, and so on.

### Contents
- Getting started
- Invoking PlayCanvas actions in Origami Engine
- Sending events from PlayCanvas to Origami Engine
- Saving state

### Getting started
TODO

### Invoking PlayCanvas actions in Origami Engine
As of now, you don't need to do anything extra to expose functionality from PlayCanvas project - it is available in Origami Design by default. Every function in every script can be called from Origami Engine, as long as this script is attached to some entity in the root of PlayCanvas project hierarchy. Here is what it would look like:

1. Create an empty entity in PlayCanvas scene as a direct Root child, and name it Foo
2. Create a new script called Bar.js, and attach it to this entity
3. Make sure instantiated class and script id also read as `Bar`, not `bar`
4. Create a function on Bar prototype and name it `doSomething`
5. Implement desired functionality inside it, and make sure it doesn't take any arguments

Now, to call this action from Origame Engine, you would need to specify a Trigger Action with the following parameters:
```
Entity: Foo
Script: Bar
Action: doSomething
```
Sending arguments inside actions isn't supported yet, but may be implemented in the future.

### Sending events from PlayCanvas to Origami Engine
As the opposite direction of communication, events allow PlayCanvas to notify Origami Engine of some state changes, triggering desired response in the container app itself. For these purposes we utilize a standard PlayCanvas event channel, used internally for communication between scripts. Here is how it can be done:

1. Create any script and attach it to any entity in your project, no matter how deep in the hierarchy
2. Invoke `this.app.fire ('something:happened')` inside `initialize()` (use `app.fire` for legacy scripting system)
3. Done! Now you just need to handle this event in Origami Design - trigger some action, start transition, and so on

As of now, sending arguments with events is not supported, but may be implemented in the future.

### Saving state
To save battery and memory usage, PlayCanvas container in Origami Engine is destroyed every time the app goes in background mode, and is restored every time it goes back to foreground. To make PlayCanvas remember the last state it was in before termination, a global helper class PCState is introduced.

Let's create a State script first and attach it to State entity in the hierarchy. To handle state saving we need to attach a callback function, which will be called by Origami Engine upon container termination. To handle state loading we simply read `state` property of supplied object:
```
State.prototype.postInitialize = function ()
{
    if (window['PCState'])
    {
        var pcs = window['PCState'];
        this.loadState (pcs.state);
        pcs.addSaveHandler (this.saveState.bind(this));
    }
};

State.prototype.loadState = function (state)
{
    if (state)
    {
        state.foo = typeof state.foo !== 'undefined' ? state.foo : 'none'; // default for foo
        state.bar = typeof state.bar !== 'undefined' ? state.bar : 0; // default for bar

        // sending a custom event to all subscribed script instances
        // so they would transition into required state accordingly
        app.fire ('state:loaded', state);
    }   
};

State.prototype.saveState = function (state)
{
    state.foo = this.foo;
    state.bar = this.bar;
    // etc...
};
```
It's important to perform state restoring in `postInitialize()` since other scripts will have a possibility to add listeners to `state:loaded` event before this event is fired by State script.






