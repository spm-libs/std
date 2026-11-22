# Getting started

## Installing

The library is the `std` package. In a Slim project:

```bash
spm i std
```

spm puts it in the project's packages folder (`packages/std`, or the folder `packages` names in `slimconfig.json`), and the build compiles it with the rest of the code.

## Importing

A module is imported by its path after `@std`, with no quotes:

```js
use { range } from @std/helpers/array
use StringHelper from @std/helpers/string
use { getVersion } from @std

log(range(1, 3))                             // [1, 2, 3]
log(StringHelper.truncate("hello world", 5)) // hello...
log(await getVersion())                      // the version in package.json
```

`@std` alone is the library's `main.slim`; the others are a folder's `main.slim` (`@std/converters` is `converters/main.slim`) or a file (`@std/helpers/array` is `helpers/array.slim`).

## Working on the library

The modules import each other by relative paths, so the repository works on its own. Its tests are in `tests/` and run with Slim's test runner from the repository folder:

```bash
slmc test
```

To try a change in a project, put the repository (or a link to it) in the project's packages folder as `std` instead of the installed copy.

Next: [Types](02-types.md).
