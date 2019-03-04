# Working with MongoDB

## Setup

In order to set up your working environment, you have to install some application. You can start by installing MongoDB itself with homebrew.

```sh
homebrew install mongodb
```

After installing use the command `mongod`.

MongoDB has a desktop client for looking into the databases. It's called MongoDB Compass and can be [downloaded](https://www.mongodb.com/products/compass) from their site.

## Nodejs and MongoDb

The next step is communicating with the database from your API. You have some packages that can help you with this. MongoDB has its own [driver](https://www.npmjs.com/package/mongodb). Other developers created a driver on top of the official driver and it's called [Mongoose](https://www.npmjs.com/package/mongoose). Mongoose has more functionalities that help you write better queries, type checking and more.

This is how you make a simple connection with the mongoose driver:

```javascript
const mongoose = require("mongoose");

mongoose
  .connect("mongodb://localhost/playground")
  .then(() => console.log("Connected to MongoDB..."))
  .catch(err => console.error("Could not connect to MongoDB...", err));
```

## Creating a schema

Schemas are an important feature that comes with Mongoose. It will create a template of the model that will be saved into the database. You can set some data types and the required values. It looks like this:

```javascript
const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  tags: [String],
  date: { type: Date, default: Date.now },
  isPublished: Boolean
});
```

## Create a model

If you defined your schema you have to use it in a model.

```javascript
const Course = mongoose.model("Course", courseSchema);

async function createCourse() {
  const course = new Course({
    name: "Node.js Course",
    author: "Mosh",
    tags: ["node", "backend"],
    isPublished: true
  });

  const result = await course.save();
  console.log(result);
}

createCourse();
```

## Get the data from the database

There are many ways to get the data from MongoDb. The simpelest one is with the `.find()` method.

```javascript
async function getCourses() {
  const courses = await Course.find();
  console.log(courses);
}

getCourses();
```

To make the qeury a bit more specific add an object with the reqeusted data in the `.find()` method.

```javascript
async function getCourses() {
  const courses = await Course.find({
    name: "Name you are looking for"
  });
  console.log(courses);
}

getCourses();
```

## Using operators with MongoDB

The original MongoDB driver delivers a couple of operators to conditionalize the query. These are also available in Mongoose. They are written as abbreviations can be used with the `$` sign.

- `eq` = equal
- `ne` = not equal
- `gt` = greater than
- `gte` = greater than or equal to
- `lt` = less than
- `lte` = less than or equal to
- `in` = in
- `nin` = not in

Example:

```javascript
.find({ price: { $gt: 10 } });
```
