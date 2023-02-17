# write_read_files

``` javascript
import { readdir, stat } from "node:fs/promises";
console.time("code");

const wait = (duration) =>
  new Promise((resolve) => setTimeout(resolve, duration));

const files = await readdir("./", {
  withFileTypes: true,
});

await Promise.allSettled(
  files.map(async (file) => {
    const parts = [file.isDirectory() ? "D" : "F", file.name];
    if (!file.isDirectory()) {
      const { size } = await stat(file.name);
      parts.push(`${size}o`);
    }

    console.log(parts.join(" - "));
  })
);

console.timeEnd("code");

```

### TERMINAL 
```bash
❯ node app.js
D - demo
F - app.js - 527o
F - demo.txt - 5o
F - package.json - 244o
code: 5.113ms

```
