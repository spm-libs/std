# The project

`@std` itself reads the running project's `package.json` and `slimconfig.json` from the folder the program runs in.

```js
use { getVersion, getPackageData, getConfigData } from @std

log(await getVersion())             // 0.3.1
const pkg = await getPackageData()
log(pkg.rootDir)                    // the folder the program runs in
log((await getConfigData()).workDir) // index
```

| Function | What it gives |
|---|---|
| `getPackageData() -> Slim` | `{ version, rootDir, workDir }`: `version` and `main` (as `workDir`) from `package.json`, `rootDir` the current folder. Without a readable `package.json`, an empty `Slim` |
| `getConfigData() -> SlimConfig` | `{ workDir }`: `main` from `slimconfig.json`. Without one, an empty `SlimConfig` |
| `getVersion() -> SemVer` | The `version` from `package.json` |

`Slim` and `SlimConfig` are structs, exported too:

```js
use { SemVer } from @std/types/formats

struct Slim {
    version?: SemVer
    rootDir?: string
    workDir?: string
}

struct SlimConfig {
    workDir?: string
}
```

`?` makes a field optional: it can be left out or be `undefined`, so a `package.json` without `main` still gives a `Slim`.

A `version` in `package.json` that isn't a semantic version gives an empty `Slim` too, and `getVersion` then throws a `TypeError`: it must return a `SemVer`.
