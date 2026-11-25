# slim-std

slim-std is the standard library of [Slim](https://github.com/cdmtn/slim-lang): custom types, converters, file reading, small helpers and time formatting. It is the `std` package: install it with `spm i std` and import its modules as `@std/...`:

```js
use { even } from @std/types/numerical
use { int } from @std/converters

let pages: even = int("12")
```

| Module | What it has |
|---|---|
| [`@std/types/*`](02-types.md) | Custom types: `positive`, `negative`, `natural`, `nonZero`, `even`, `odd`, `unit`, `email`, `gmail`, `url`, `uuid`, `SemVer`, `JSONString`, `HTMLString`, `HTMLObject`, `nonempty`, `AnyArray`, `SymbolInstance`, `SHA256`, `QuickHash`, `TimeStamp` |
| [`@std/converters`](03-converters.md) | `int`, `float`, `number`, `string`, `bool`, `bigint`, `symbol`, `array`, `date`, `json`, `jsonstr` |
| [`@std/parse`](04-parse.md) | `parseJSON`, `parseText` and `ReadError`: reading files |
| [`@std/helpers/*`](05-helpers.md) | `range`, `StringHelper`, `replaceBackslashes`, `RequestHelper` |
| [`@std/time`](06-time.md) | `TimeHelper`: the current time, Unix seconds, date formatting |
| [`@std`](07-project.md) | `getPackageData`, `getConfigData`, `getVersion`: the running project's `package.json` and `slimconfig.json` |
| [`@std/random`](08-random.md) | `createRandom`, `pick`, `weighted`, `shuffle`: random numbers that repeat with a seed |
| [`@std/math`](09-math.md) | `clamp`, `lerp`, `inverseLerp`, `smoothstep`, `roundTo` |

The server, the router and forms are not here: they are part of Slim itself, imported as `@slim/server`, `@slim/router` and `@slim/forms`.

## Where to go next

- [Getting started](01-start.md): installing, importing, working on the library
- [Types](02-types.md), the first module
