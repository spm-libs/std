# Types

Custom types: each is a check that runs whenever a value is given to a variable, a parameter or a field of that type. They are used like any other type; see [custom types](https://github.com/cdmtn/slim-lang/blob/main/docs/03-types/02-custom-types.md) in the Slim docs for how they work.

```js
use { even, odd, positive } from @std/types/numerical
use { SemVer } from @std/types/formats
use { email } from @std/types/mails

struct Account {
    email: email
    balance: positive
}

let a: even = 4
let b: odd = 3
let version: SemVer = "1.2.17"

log(Account.verifySafe({ email: "a@b.com", balance: 10 }).success)  // true
log(Account.verifySafe(JSON.parse(`{ "email": "nope", "balance": 10 }`)).success) // false

func half(n: even) -> int { return n ~/ 2 }

let c: even = 3 // ❌ "c" expects even, got 3
```

A wrong literal is a compile error, as above: every type here except `JSONString` and `HTMLObject` has a body simple enough for the checker to work out. Values that come in while the program runs (`JSON.parse`, a form, a request) are checked when they arrive.

Each type first checks the kind of value with `extends` (`extends string`, `extends int`, `extends number`), so a value of another kind is turned down before the body runs: `["1.2.3"]` is not a `SemVer`, `"5"` is not `positive`.

## @std/types/numerical

| Type | A value of it is |
|---|---|
| `positive` | A number above `0`: `10`, `0.5` |
| `negative` | A number below `0`: `-3` |
| `natural` | An integer `0` or above: `0`, `7` |
| `nonZero` | An `int` or a `float` other than `0` |
| `even` | An even `int` |
| `odd` | An odd `int` |
| `unit` | A number from `0` to `1`, both included: `0`, `0.25`, `1`. For a share, a volume, an opacity |

## @std/types/formats

| Type | A value of it is |
|---|---|
| `url` | An `http://` or `https://` URL with no spaces |
| `uuid` | A UUID string, any case: `"550e8400-e29b-41d4-a716-446655440000"` |
| `SemVer` | A [semantic version](https://semver.org) string: `"1.2.17"`, `"2.0.0-beta.1"`, `"1.0.0+build.5"` |
| `JSONString` | A string that `JSON.parse` reads without an error |
| `HTMLString` | A string with something that looks like an HTML tag in it: `"<b>hi</b>"` |
| `HTMLObject` | A DOM element (`instanceof HTMLElement`). Where there is no DOM, as in Node, no value is |

## @std/types/hash

| Type | A value of it is |
|---|---|
| `SHA256` | A string of 64 hex digits, any case: a SHA-256 as `StringHelper.hash` gives |
| `QuickHash` | A 32-bit `int` (it can be negative), as `StringHelper.quickHash` gives |

## @std/types/mails

| Type | A value of it is |
|---|---|
| `email` | An e-mail address: something, `@`, a domain with a dot, no spaces |
| `gmail` | A `@gmail.com` address: letters, digits and dots before the `@`, any case |

## @std/types/time

| Type | A value of it is |
|---|---|
| `TimeStamp` | An `int` longer than 12 digits (`sizeof`): a time in milliseconds, as `Date.now()` gives |

## @std/types/common

| Type | A value of it is |
|---|---|
| `nonempty` | A string or an array that isn't empty: `"a"`, `[1]` |
| `SymbolInstance` | A `symbol` |
| `AnyArray` | An array of anything |

Next: [Converters](03-converters.md).
