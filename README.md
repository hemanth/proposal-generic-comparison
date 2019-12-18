# Array.prototype.compare

# Motivation

Comparing arrays are one of the most common operations we do on arrays, and there is no consitent standard way to compare two array and given that array might have any type of primitives and nested structures, it get more tedious to compare them.

# How is this currently handled?

There is no standard way to do it, there are few modules like [array-equal](https://www.npmjs.com/package/array-equal), [deep-equal](https://www.npmjs.com/package/deep-equal) with like 5M and 8M downloads per week respectivly, which is subset of deep comparison.

Consider few examples:

```js
// Schmea validation
const equal = require('deep-equal');

const expectedSchema = {
  name: {
    type: String,
    required: true
  },
  score: {
    type: Number,
    default: 0
  }
};

equal(schemaCall.args[0], expectedSchema);

```

__node builtin:__

```js
// assert.deepStrictEqual(actual, expected[, message])

deepStrictEqual([new Uint32Array([1, 2, 3, 4]).subarray(1, 3), new Uint32Array([2, 3])]);
```

```js
// assert.deepEqual(actual, expected[, message])

assert.deepEqual( tokenizer( "AD", "G", cldr ), [{
		type: "G",
		lexeme: "AD",
		value: "1"
	}] );
```


# How we could do it?

`Array.prototype.compare` takes a comparator function, which gets two arguments.

Each a tuple of `[value, key]` and it returns `< 0, 0, or > 1` (and throws when a non-finite-non-integer is returned) and then it would return either `-1, 0, or 1`

That way we could write our own logic, and get back `0` if they were equal.


P.S: This was a proposal evolved [Array.prototype.equals](https://github.com/hemanth/Array.prototype.equals).

__Extending the idea to a three-way comparison:__

We could rather have a `<=>` three-way compare operator, that does the below:

```
         true		      	   false
a < b    (a <=> b) < 0		 (a <=> b) >= 0
a <= b   (a <=> b) <= 0		 (a <=> b) > 0
a > b    (a <=> b) > 0		 (a <=> b) <= 0
a >= b   (a <=> b) >= 0		 (a <=> b) < 0
```
