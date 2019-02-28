# Notes about Express.js

## The simple usage of Express

Express is a great library to make an API. It wil create a server very easily and it will help you handle your endpoints. A basic example of this is:

```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello World");
});

app.listen(3000, () => {
  console.log("Listening on port 3000...");
});
```

## Setup envoirement variables

As you can see in the first example. The port is hardcoded. This can be a problem on the server beceause you can't rely on the port 3000. For that you need to check which port is given to you by the server envoirement. This information is available in the global object `process`. To be more specific.

```javascript
process.env.PORT;
```

So to solve the problem about the static number use a variable like:

```javascript
const port = process.env.PORT || 3000;
app.listen(port, () => {
  console.log(`Listening on port ${port}...`);
});
```

There is a command to set a specific port on you envoirement.

For Mac

```sh
export PORT=5000
```

For Windows

```sh
set Port=5000
```

## Parameters and querys

The URL can contain some information about the data it should return. You can do that with adding parameters and querys. A parameter starts with `:` and for a query `?`.

```javascript
app.get("/api/posts/:id");

// https://api/posts/1 will result in:

{
  id: 1;
}

// Will get all the post sorted by name.
app.get("/api/posts?sortBy=name");
```

## Validation

You should never trust the client side with sending the correct data. You need validation for that and let the client side know that something went wrong. There is an populair and very usefull package on NPM. It's called [joi](https://www.npmjs.com/package/joi) and gives you a lot of functions to validate and send feedback.

Here is an example of its usage:

```javascript
const Joi = require("joi");

app.post("/api/courses", (req, res) => {
  // Make a schema of a valid body message
  const schema = {
    name: Joi.string()
      .min(3)
      .required()
  };

  // Validates the values and creates an object with the result.
  const result = Joi.validate(req.body, schema);

  // Handle error.
  if (result.error) {
    res.status(400).send(result.error);
    return;
  }

  // Handle correct post data...
});
```
