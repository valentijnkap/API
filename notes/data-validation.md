# Mongoose Data Validation

## Making values required

Sometimes you want certain values to be required. There is an easy way to do that. You have to pass an object to the key value and set the required option to true.

```javascript
const courseSchema = new mongoose.Schema({
  name: { type: String, required: true },
  author: String,
  tags: [String]
});
```

Values required based on other values:

```javascript
const courseSchema = new mongoose.Schema({
  name: { type: String, required: true },
  author: String,
  tags: [String],
  isPublished: Boolean,
  price: {
    type: Number,
    required: function() {
      return this.isPublished;
    }
  }
});
```

There are more validation that you can use in Mongoose like:

- `enum`
- `minlength` minimum amount of characters
- `maxlength` maximum amount of characters
- `min` minimum amount of number value
- `max` maximum amount of number value

## Creating a custom validation

```javascript
const courseSchema = new mongoose.Schema({
  tags: {
    type: Array,
    validate: {
      validator: function(v) {
        return v.length > 0;
      },
      message: "A course should have at least one tag."
    }
  }
});
```
