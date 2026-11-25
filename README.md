# slim-std

The standard library of [Slim](https://github.com/cdmtn/slim-lang): custom types, converters, file reading, small helpers, time formatting, random numbers and math.

## Setup

In a Slim project:

```console
spm i std
```

Its modules are then imported as `@std/...`. The server, the router and forms are part of Slim itself (`@slim/server`, `@slim/router`, `@slim/forms`).

## Quick example

```js
use { int } from @std/converters
use { nonZero } from @std/types/numerical
use { RequestHelper } from @std/helpers/request
use TimeHelper from @std/time

const perPage: nonZero = int(process.env.PER_PAGE ?? "20")
const api = new RequestHelper({ baseURL: "https://api.example.com", timeout: 5000 })

const posts = await api.get(`/posts?limit=${perPage}`)
log(`${posts.length} posts at ${TimeHelper.toDate(TimeHelper.now(), { format: "{{hh}}:{{mm}}" })}`)
```

`PER_PAGE=0` stops the program at the first line: `0` is not a `nonZero`.

## Tests

```console
slmc test
```

## Documentation

The full guide is in [`docs/`](docs/index.md):

- [Getting started](docs/01-start.md): installing, importing, working on the library
- [Types](docs/02-types.md): `positive`, `natural`, `email`, `url`, `uuid`, `SemVer` and the others
- [Converters](docs/03-converters.md): `int`, `float`, `bool`, `json` and the others
- [Reading files](docs/04-parse.md): `parseJSON`, `parseText`
- [Helpers](docs/05-helpers.md): `range`, `StringHelper` (`pad`, `splitArgs`, `hash`...), `RequestHelper`, `replaceBackslashes`
- [Time](docs/06-time.md): `TimeHelper`
- [The project](docs/07-project.md): `getVersion`, `getPackageData`, `getConfigData`
- [Random](docs/08-random.md): `createRandom`, `pick`, `weighted`, `shuffle`
- [Math](docs/09-math.md): `clamp`, `lerp`, `inverseLerp`, `smoothstep`, `roundTo`
