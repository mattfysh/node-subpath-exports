## node subpath exports + ESM "bug"

The top-level package is an ESM codebase, designated by `"type": "module"` in package.json.

It imports `pkg`, which contains an export map. One of the "conditions" in the export map is `import`, which is used when writing `import 'pkg'`.

You would assume that an import condition in an export map would only point to an ESM module (otherwise, why split behaviour on that condition), however it tries to load the target as a CommonJS module, which results in the dreaded:

```
/node-subpath-exports/node_modules/pkg/main.esm.js:1
import util from 'util'
^^^^^^

SyntaxError: Cannot use import statement outside a module
```
