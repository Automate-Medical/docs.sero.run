---
description: Setting up your development environment
---

# Setup \(TODO\)

## Install the necessary packages

\(hopefully, you went through the speedrun\). Do this in a new empty project.

Now, install typescript, ts-node, and eslint.

## Configure package.json

There is nothing to run yet, but we still need to run and build the project. Do this by entering the following into `package.json`. 

```javascript
"scripts": {
    "build": "tsc -p tsconfig.json",
    "start": "ts-node current-time/index.ts -p tsconfig.json"
```

\(testing the code blocks for now, more TODO here\)



