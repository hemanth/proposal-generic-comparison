# Array.prototype.compare

# Motivation

Comparing arrays are one of the most common operations we do on arrays, and there is no consitent standard way to compare two array and given that array might have any type of primitives and nested structures, it get more tedious to compare them.

# How is being done now?

There is no standard way to do it, there are few modules like [array-equal](https://www.npmjs.com/package/array-equal), [deep-equal](https://www.npmjs.com/package/deep-equal) with like 5M and 8M downloads per week respectivly, which is subset of deep comparison.

Consider few examples:

```js
const equal = require('deep-equal');
console.dir([
    equal(
        { a : [ 2, 3 ], b : [ 4 ] },
        { a : [ 2, 3 ], b : [ 4 ] }
    ),
    equal(
        { x : 5, y : [6] },
        { x : 5, y : 6 }
    )
]);
```

__node builtin:__
```js
// assert.deepStrictEqual(actual, expected[, message])

deepStrictEqual([new Uint32Array([1, 2, 3, 4]).subarray(1, 3), new Uint32Array([2, 3])]);
```


# How we could do it?

`Array.prototype.compare` takes a comparator function, which gets two arguments: each a tuple of `[value, key]` and it returns `< 0, 0, or > 1` (and throws when a non-finite-non-integer is returned) and then it would return either `-1, 0, or 1`
that way we could write our own logic, and get back `0` if they were equal.


P.S: This was a proposal evolved [Array.prototype.equals](https://github.com/hemanth/Array.prototype.equals).
