# Random

## @std/random

Random numbers that can repeat themselves. It uses nothing of Node, so it runs in any JavaScript engine.

```js
use { createRandom, pick, weighted, shuffle } from @std/random

const random = createRandom(1234)
const count = random.int(1, 3)
const rare = random.chance(0.05)
const color = pick(random, ["red", "green", "blue"])
const size = weighted(random, [["small", 6], ["medium", 3], ["large", 1]])
const order = shuffle(random, ["north", "east", "south", "west"])
```

With a seed, a run gives the same numbers every time, which a replay, a test or two machines that must agree need. Without one it uses `Math.random`.

## createRandom

`createRandom(seed?: number) -> Random`

| Field | What it does |
|---|---|
| `next() -> number` | A number from 0 (included) to 1 (not included) |
| `int(low, high) -> number` | A whole number from `low` to `high`, both included |
| `float(low, high) -> number` | A number from `low` (included) to `high` (not included) |
| `chance(probability) -> bool` | `true` with that probability: `chance(0.25)` is `true` one time in four |
| `seed() -> number \| null` | The seed it was made with, `null` without one |
| `state() -> number \| null` | Where a seeded generator is now: a whole number to save; `null` without a seed |
| `setState(state)` | Goes back to a saved `state`; throws on a generator without a seed |

### Seeds

Any number is a seed. A whole number counts modulo `2**32` (`-1` is `4294967295`, `2**32` is `0`); a fraction, `Infinity` or `NaN` is hashed, so `0.5` is not `0`.

To repeat a run, keep the seed and make a new generator from it:

```js
use { createRandom } from @std/random

const first = createRandom(Date.now())
const again = createRandom(first.seed() ?? 0)
log(first.int(1, 100) == again.int(1, 100)) // true
```

### Saving where it is

The seed repeats a run from its start. To go on from the middle, after a restart, keep `state()` and give it back with `setState`:

```js
use { createRandom } from @std/random

const first = createRandom(42)
const saved = first.state() ?? 0
const ahead = first.next()

const later = createRandom(42)
later.setState(saved)
log(later.next() == ahead) // true
```

The generator after `setState` gives the numbers the saved one would have given next. `seed()` still returns the seed it was made with.

### int

`int(low, high)` gives a whole number from `low` to `high`, both included, in either order: `int(3, 1)` is the same as `int(1, 3)`. Fractions are rounded inward, so `int(1.5, 3.5)` gives 2 or 3. With no whole number between the two (`int(1.2, 1.8)`), or a bound that is not finite, it throws a `RangeError`.

## pick

`pick<T>(random: Random, items: T[]) -> T | undefined`

One of `items`; `undefined` when the list is empty.

## weighted

`weighted<T>(random: Random, entries: [T, number][]) -> T | undefined`

One of the values, each as likely as its weight: with `[["yes", 2], ["no", 1]]`, `"yes"` comes two times in three. Weights need not add up to anything. An entry whose weight is 0, below 0 or not a number is never chosen; `undefined` when no entry weighs anything.

## shuffle

`shuffle<T>(random: Random, items: T[]) -> T[]`

A new list with the same items in a random order; `items` is left as it was. With the same seed, the same order.

`Random` is a type name of the library: like every type name in Slim, it is global, so don't give a type of your own that name.

Next: [Math](09-math.md).
