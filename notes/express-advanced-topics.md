# Advanced topics of Express.js

## Middelware

An important topic of Express.js is middelware or a middelware function. It will always be involved with API's. A middelware function basicly takes a request and sends a response or passes it to an another middelware function. A simple example of this is:

```javascript
// index.js
const logger = require("./logger");
const express = require("express");
const app = express();

// Custom middelware function
app.use(logger);

// logger.js
function log(req, res, next) {
  console.log("Logging...");
  next();
}

module.exports = log;
```

## More built-in middelware functions

There are more middelware functions build-in in express that you can use. They are very handy for certain cases.

```javascript
// This wil encode key values in the url and populate the req.body object.
app.use(express.urlencoded());

// If you want to serve static files like images to the client this functions will define that.
app.use(express.static("public"));
```

## Third-party middelware

Besides that you can write your own middelware function there are thirdparty packages. They can be found [here](https://expressjs.com/en/resources/middleware.html). Two populair packages are [Helmet](https://www.npmjs.com/package/helmet) and [Morgan](https://www.npmjs.com/package/morgan). Helmet helps to secure your application and Morgan logs request. Both of them are very usefull but will drain some performence. Try to avoid using many middelware functions. Only use them if you really need to use.

## Configuration

If you have different envoirements like production and development then some configuration might differ sometimes. There are various ways to do so. In the lecture I found some tips about the package [config](https://www.npmjs.com/package/config) from NPM. It will help you set some configurations for different envoirements so that you don't have to edit everything manually.

## Template engines

In some situations you have to send some HTML to the client. There are packages that help you render HTML like [EJS](https://www.npmjs.com/package/ejs), [Pug](https://www.npmjs.com/package/pug) and [MustacheJS](https://www.npmjs.com/package/mustache).

An example of pug:

```Pug
// pug file

html
  head
    title= title
  body
    h1= message
```

```javascript
// index.js

app.get("/", (req, res) => {
  res.render("index", { title: "My Express App", message: "Hello" });
});
```

## Structure routes

Writing all your routes in one file is not a good option. Your code will not be maintainable and very dense. Express delivers a function that you can use to split your routes. A good practice is that you split up all your routes with the same subject. Like all the routes for courses in a `courses.js` file.

```javascript
// courses.js

const express = require("express");
const router = express.Router();

router.get("/", (req, res) => {
  res.send(courses);
});

module.exports = router;
```

Put the `courses.js` in a `routes/` folder in the root of your project and import it in your `index.js` file.

```javascript
// index.js

const express = require("express");
const courses = require("./routes/courses");

const app = express();

app.use("/api/courses", courses);
```
