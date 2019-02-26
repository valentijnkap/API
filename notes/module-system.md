# Module System notes

## Global scope

The global scope in Node.js is a bit different than the global scope in your browser. In the browser, you have the `window` object but that is not available on the server side. In Node.js, you can access the global scope via the object `global`. An important thing is that variables are not attached to the global scope. To solve that problem you need modules.

## Modules

In the real world, you often split your javascript code into multiple files. These are considered as modules. Every module has it's own scope and variables and functions. You can make the variables and functions accessible by making it public. By default functions and variables are private. The modules nodes are not global, they are objects that contain information.

```javascript
Module {
  id: '.',
  exports: {},
  parent: null,
  filename: '/Users/valentijnkap/Documents/Hogeschool Amsterdam/Jaar 5/Making-an-API/udemy-excersises/module-object/app.js',
  loaded: false,
  children: [],
  paths: [
    '/Users/valentijnkap/Documents/Hogeschool Amsterdam/Jaar 5/Making-an-API/udemy-excersises/module-object/node_modules',
    '/Users/valentijnkap/Documents/Hogeschool Amsterdam/Jaar 5/Making-an-API/udemy-excersises/node_modules',
    '/Users/valentijnkap/Documents/Hogeschool Amsterdam/Jaar 5/Making-an-API/node_modules',
    '/Users/valentijnkap/Documents/Hogeschool Amsterdam/Jaar 5/node_modules',
    '/Users/valentijnkap/Documents/Hogeschool Amsterdam/node_modules',
    '/Users/valentijnkap/Documents/node_modules',
    '/Users/valentijnkap/node_modules',
    '/Users/node_modules',
    '/node_modules'
  ]
}

```

## Emitter

Emitter is one of the most important module that Node.js has. It is the fundemental of a lot of order modules. An emitter is sending a signal to tell the app that an event has occured. This is a good example of registering an event and an emmiter:

```javascript
const EventEmitter = require("events");
// create a new instance of the EventEmitter class
const emitter = new EventEmitter();

// Register and handle event
emitter.on("messageLogged", evenArg => {
  console.log("Listener called", evenArg);
});

// Send the event
emitter.emit("messageLogged", {
  id: 1,
  url: "http://"
});
```
