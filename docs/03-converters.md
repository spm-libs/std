# Converters

`@std/converters` turns values into other types. A value that can't be converted throws a `TypeError` that names it.

```js
use { int, float, bool, json, jsonstr } from @std/converters

const form = { count: "42", price: "1.5", agree: "TRUE" }

log(int(form.count))        // 42
log(float(form.price))      // 1.5
log(bool(form.agree))       // true
log(json('{"a":1}'))        // { a: 1 }
log(jsonstr({ a: 1 }))      // {"a":1}

int("4.5")                  // ❌ TypeError: Cannot convert "4.5" to int
```

| Function | Takes | Gives |
|---|---|---|
| `int(value)` | `string \| int` | The `int`; a string that isn't a whole number throws |
| `float(value)` | `string \| float \| int` | The number; a string that isn't a number throws |
| `number(value)` | `string \| float \| int` | The same as `float`, typed `number` |
| `string(value)` | anything | `String(value)` |
| `bool(value)` | `int \| float \| string \| bool` | A number is `true` when it isn't `0`. `"true"` and `"1"` are `true`, `"false"` and `"0"` are `false` (any case, spaces around are ignored); any other string is `true` when it isn't empty |
| `bigint(value)` | `string \| int \| bigint` | The `bigint`; `"1.5"` and other non-integers throw |
| `symbol(value)` | anything | A new symbol with `String(value)` as its description |
| `array(value)` | anything | An array as it is; anything else in an array of one: `array(3)` is `[3]` |
| `date(value)` | `TimeStamp` | A `Date` from a time in milliseconds; an invalid date throws |
| `json(value)` | an array, a string, a number or an object | A string is parsed (invalid JSON throws `TypeError: Invalid JSON`); anything else is copied through JSON |
| `jsonstr(value)` | an array, a string, a number or an object | `JSON.stringify(value)`, typed `JSONString` |

Next: [Reading files](04-parse.md).
