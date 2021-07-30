---
description: Setting up your Sero development environment
---

# Setup

## Install the necessary packages

Make sure you have at least node v14 installed globally on your machine. The latest version can be installed downloaded here.

In a new terminal run `mkdir sero-api` and `cd` into it. Next run `npm init` to create a `package.json`, in which you can use the default settings. Next, install Sero:

if you are using terminal, bash:

```bash
npm i --save @sero.run/sero
```

If you are using PowerShell:

```bash
npm i --save "@sero.run/sero"
```

## Basic setup

Create `src` directory and `cd` in to it. Add an `index.js` file with the following contents:

```javascript
import { Rest, Http, start } from "@sero.run/sero"

const config = {};
const http = Http(config);

Rest(config, http);
start(http);
```

* `Rest` is 
* `Http` is 
* `start` is
* `config` is 

In your `package.json`, we're going to add a new script that runs the node server, and set the type to `module`. The file should now look like this:

```javascript
{
  "name": "cds-hooks-api-guide",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/index.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "@sero.run/sero": "^0.0.14"
  },
  "type": "module"
}
```

To run the server, run `npm run start`. You should now see this:

```bash
> cds-hooks-api-guide@1.0.0 start
> node src/index.js

Sero booting at http://0.0.0.0:8080
```

Great job! We're ready for the next section, where we will be creating a CDS service with Sero.

