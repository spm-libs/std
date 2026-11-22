# Helpers

## @std/helpers/array

`range(min: int, max: int) -> AnyArray`: the integers from `min` to `max`, both included.

```js
use { range } from @std/helpers/array

log(range(1, 5)) // [1, 2, 3, 4, 5]
```

Importing the module also changes `Array.prototype.sort` for the whole program: called without a comparator on an array of numbers only, it sorts them by value instead of as text. Slim code passes a comparator anyway (the checker asks for one), so this matters only to JavaScript the program calls.

## @std/helpers/string

The default export `StringHelper` is a locked object: its functions can't be replaced.

```js
use StringHelper from @std/helpers/string

log(StringHelper.len("hello"))                  // 5
log(StringHelper.truncate("hello world", 5))    // hello...
log(StringHelper.hash("abc").length)            // 64
log(StringHelper.quickHash("hello"))            // 99162322
```

| Function | What it does |
|---|---|
| `len(str) -> int` | The length |
| `truncate(str, maxLength) -> string` | The first `maxLength` characters and `...` when the string is longer; the string itself otherwise |
| `hash(str) -> SHA256` | SHA-256 in hex (`node:crypto`, so Node only) |
| `quickHash(str) -> QuickHash` | A fast 32-bit hash as a number. Not for security; it can be negative |

## @std/helpers/path

`replaceBackslashes(path: string)`: the path with every `\` turned into `/`, for paths that came from Windows.

## @std/helpers/request

`RequestHelper` is a small HTTP client on top of `fetch`.

```js
use { RequestHelper } from @std/helpers/request

const api = new RequestHelper({ baseURL: "https://api.example.com", headers: { Authorization: "Bearer token" }, timeout: 5000 })

const user = await api.get("/users/1")
await api.post("/users", { name: "Ada" })
```

| Constructor option | Default | What it is |
|---|---|---|
| `baseURL` | `""` | Put before every URL |
| `headers` | `{}` | Sent with every request |
| `timeout` | `10000` | Milliseconds before the request is aborted |

| Method | What it sends |
|---|---|
| `get(url, options?)` | `GET` |
| `delete(url, options?)` | `DELETE` |
| `post(url, body, options?)` | `POST` with `body` as JSON |
| `put(url, body, options?)` | `PUT` with `body` as JSON |
| `patch(url, body, options?)` | `PATCH` with `body` as JSON |
| `request(url, options?)` | Whatever `options` says: they are `fetch` options, and their `headers` are added to the helper's |

The answer is read by its `Content-Type`: JSON is parsed, `text/*` is a string, anything else a `Blob`. A status that isn't 2xx throws `{ status, statusText, data }`, with `data` read the same way.

Next: [Time](06-time.md).
