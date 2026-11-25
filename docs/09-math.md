# Math

## @std/math

Small numeric helpers.

```js
use { clamp, lerp, inverseLerp, smoothstep, roundTo } from @std/math

const t = inverseLerp(10, 20, 15)    // 0.5
const fade = smoothstep(0, 1, t)     // 0.5
const volume = clamp(lerp(0.2, 1, fade), 0, 1)
const shown = roundTo(volume, 1)
```

| Function | Returns |
|---|---|
| `clamp(value, low, high)` | `value` kept between `low` and `high` |
| `lerp(from, to, t)` | `from + (to - from) * t`; `t` is not clamped |
| `inverseLerp(from, to, value)` | Where `value` lies from `from` (0) to `to` (1); `0` when `from == to` |
| `smoothstep(from, to, value)` | `inverseLerp` clamped to 0..1 and eased: `t * t * (3 - 2 * t)` |
| `roundTo(value, digits = 0)` | `value` rounded to `digits` places after the point: `roundTo(2.35, 1)` is `2.4`; a negative `digits` rounds to tens, hundreds: `roundTo(1234, -2)` is `1200`. Halves go up, as with `Math.round`: `roundTo(-2.5)` is `-2` |

All parameters and results are `number`.
