# Time

The default export of `@std/time` is `TimeHelper`, a class with static functions only.

```js
use TimeHelper from @std/time

const time = 1700000000123
log(TimeHelper.toUnix(time))                                          // 1700000000
log(TimeHelper.toDate(time))                                          // 15.11.2023 00:13:20:000
log(TimeHelper.toDate(time, { format: "{{yyyy}}-{{MM}}-{{dd}}" }))    // 2023-11-15
log(TimeHelper.toDate(time, { format: "{{h}}:{{mm}} {{ampm}}", ampm: true })) // 12:13 AM
log(TimeHelper.now() > time)                                          // true
```

The dates above are in UTC+2.

| Function | What it does |
|---|---|
| `now() -> int` | `Date.now()`: milliseconds since 1970 |
| `toUnix(time) -> int` | Milliseconds to whole seconds. A time 12 digits long or shorter is taken as seconds already and given back as it is |
| `toDate(time, options?) -> string` | The time as text in the program's time zone. `time` is seconds or milliseconds, told apart the same way |

`toDate` options:

| Option | Default | What it is |
|---|---|---|
| `format` | `"{{dd}}.{{MM}}.{{yyyy}} {{hh}}:{{mm}}:{{ss}}:{{ii}}"` | The text, with tokens replaced |
| `ampm` | `false` | A 12-hour clock: hours go 12, 1, ... 11, and `{{ampm}}` is `AM` or `PM` |

| Token | Is | Token | Is |
|---|---|---|---|
| `{{d}}`, `{{dd}}` | Day: `5`, `05` | `{{h}}`, `{{hh}}` | Hour: `9`, `09` |
| `{{M}}`, `{{MM}}` | Month: `3`, `03` | `{{m}}`, `{{mm}}` | Minute: `7`, `07` |
| `{{yy}}`, `{{yyyy}}` | Year: `23`, `2023` | `{{s}}`, `{{ss}}` | Second: `4`, `04` |
| `{{ampm}}` | `AM`, `PM`, or nothing without `ampm` | `{{i}}`, `{{ii}}` | Millisecond: `5`, `005` |

`toDate` works in whole seconds: a time in milliseconds loses them, so `{{ii}}` is `000` for it. Pass a `Date`'s own `getMilliseconds()` when they matter.

Next: [The project](07-project.md).
