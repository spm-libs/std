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

## Outside Node

Importing a module never changes anything outside it, so a program gets only what it imports. Most modules use nothing of Node and run in any JavaScript engine, such as one embedded in another program: the types, `@std/converters`, `@std/helpers/array`, `@std/helpers/string`, `@std/helpers/path`, `@std/time`, `@std/random` and `@std/math`. These need Node: `@std/parse` (files) and `@std` (the project's files); `@std/helpers/request` needs `fetch`.

`tests/portable.test.slim` keeps it so: the modules of the first list, and all they import, may import nothing but each other.

## Working on the library

The modules import each other by relative paths, so the repository works on its own. Its tests are in `tests/` and run with Slim's test runner from the repository folder:

```bash
slmc test
```

To try a change in a project, put the repository (or a link to it) in the project's packages folder as `std` instead of the installed copy.

Next: [Types](02-types.md).
