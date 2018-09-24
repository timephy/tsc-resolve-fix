# tsc-resolve-fix 
## A tool for resolving typescript modules defined in tsconfig.json 

This package resolves non-relative imports to their relative path.
This was possible with "tsc-resolve" by Dimitar Mazhlekov, but in his version it was not possible to do the following:
```typescript
// tsconfig.json
"paths": {
    "@util/*": [
        "util/*"
    ]
}
```
```typescript
// index.js
import * as someUtility from "@utils/someUtility";
```
With this package you can resolve further paths (e.g. "someUtility") after the non-relative path (e.g. "@util").
The old version only allowed for one non-relative path to resolve to one file/directory.

## Why tsc-resolve?
<a href="https://asciinema.org/a/123305" target="_blank">
    <img src="https://github.com/mazhlekov/tsc-resolve/raw/master/img/tsc-resolve.gif" />
</a>

## Installation
```bash
# Local package
$ npm i timephy/tsc-resolve-fix --save-dev

# Global CLI
$ npm i -g timephy/tsc-resolve-fix 
```

## Usage
### NPM task
```bash
$ npm i tsc-resolve --save-dev

"scripts": {
    "compile": "tsc",
    "build": "compile && tsc-resolve"
}

$ npm run build
```
### CLI
```bash
$ npm i -g timephy/tsc-resolve-fix

$ ./node_module/.bin/tsc-resolve
$ tsc-resolve
$ tsc-resolve -p tsconfig.prod.json
$ tsc-resolve -p ./conf/tsconfig.dev.json
$ tsc-resolve -p ./conf/
$ tsc-resolve -p ../
```
    
### TypeScript
```typescript
import { tscResolve } from "tsc-resolve"
import * as path from "path"

// Simple ./tsconfig.json
const configPath = process.cwd();
tscResolve(configPath)
    .then(() => { /*DONE*/ });

// Specific tsconfig.json
const configPath = path.join(process.cwd(), "tsconfig.prod.json");
tscResolve(configPath)
    .then(() => { /*DONE*/ });

// Specific tsconfig.json in different folder
const configPath = path.resolve(process.cwd(), "../conf/tsconfig.dev.json");
tscResolve(configPath)
    .then(() => { /*DONE*/ });

// Async/Await
const configPath = process.cwd();
await tscResolve(configPath);
```

### JavaScript
```javascript
const tscResolver = require("tsc-resolve");
const path = require("path");

// Simple ./tsconfig.json
const configPath = process.cwd();
tscResolve(configPath)
    .then(() => { /*DONE*/ });

// Specific tsconfig.json
const configPath = path.join(process.cwd(), "tsconfig.prod.json");
tscResolve(configPath)
    .then(() => { /*DONE*/ });

// Specific tsconfig.json in different folder
const configPath = path.resolve(process.cwd(), "../conf/tsconfig.dev.json");
tscResolve(configPath)
    .then(() => { /*DONE*/ });

// Async/Await
const configPath = process.cwd();
await tscResolve(configPath);
```
