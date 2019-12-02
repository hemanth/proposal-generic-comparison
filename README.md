# Array.prototype.compare

`Array.prototype.compare` takes a comparator function, which gets two arguments: each a tuple of `[value, key]` and it returns `< 0, 0, or > 1` (and throws when a non-finite-non-integer is returned) and then it would return either `-1, 0, or 1`
that way we could write our own logic, and get back `0` if they were equal.
