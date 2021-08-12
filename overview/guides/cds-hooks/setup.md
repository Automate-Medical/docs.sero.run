---
description: Setting up your Sero development environment
---

# Setup

## Install Node + Sero

We need to have the latest version of Node LTS installed. [It can be downloaded here](https://nodejs.org/en/download/).

In a new terminal run `mkdir sero-api` and `cd` into it. Next run `npm init` to create a new project. Then install Sero.

{% tabs %}
{% tab title="Bash" %}
```
npm i --save @sero.run/sero
```
{% endtab %}

{% tab title="PowerShell" %}
```bash
npm i --save "@sero.run/sero"
```
{% endtab %}
{% endtabs %}

## Basic setup

Create a `src` directory and `cd` into it. Add an `index.js` file with the following contents:

{% code title="index.js" %}
```javascript
import { Rest, Http, start } from "@sero.run/sero"

const config = {};
const http = Http(config);

Rest(config, http);
start(http);
```
{% endcode %}

In `package.json`, we're going to add a new script that runs the node server, and set the type to `module`. The file should now look like this:

{% code title="package.json" %}
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
{% endcode %}

To run the server, run `npm run start`. You should now see this:

```bash
> cds-hooks-api-guide@1.0.0 start
> node src/index.js

Sero booting at http://0.0.0.0:8080
```

Great job! We're ready for the next section, where we will be creating a CDS Service with Sero.

