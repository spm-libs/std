# Reading files

`@std/parse` reads a file as text or as JSON. It uses `node:fs`, so it runs in Node, not in a browser.

```js
use { parseJSON, parseText, ReadError } from @std/parse

const pkg = await parseJSON("package.json")
log(pkg.name)

try {
    const notes = await parseText("notes.txt")
    log(notes.length)
} catch (err) {
    if (err instanceof ReadError) log("no notes yet")
}
```

| Function | What it does |
|---|---|
| `parseText(path) -> string` | Reads the file as UTF-8 |
| `parseJSON(path) -> object` | Reads the file as UTF-8 and parses it |

A relative path is read from the folder the program runs in. A missing file, a file that can't be read and invalid JSON all throw a `ReadError`; its message is the original error's.

Next: [Helpers](05-helpers.md).
