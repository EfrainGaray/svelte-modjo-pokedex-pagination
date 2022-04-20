# Infinite pokemon scroll - modyo challenge pokedex [DEMO](https://challenge-pokedex.surge.sh/):

[![N|Solid](https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png)](https://pokeapi.co/)

![Build Status](https://github.com/EfrainGaray/svelte-modjo-pokedex-pagination/actions/workflows/main.yaml/badge.svg)



## Get started


```bash
git clone https://github.com/EfrainGaray/svelte-modjo-pokedex-pagination.git
cd svelte-modjo-pokedex-pagination
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


Install the dependencies...

```bash
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:8080](http://localhost:8080). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).


## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for *any* path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```

## Deploying to the web


### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```


## Deploy workflow

Deploy in aws with githubactions.

services used surge.sh

workflow
```yaml
name: Deploy Website

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    name: Deploying to surge
    steps:
      - uses: actions/checkout@v1
      - name: Install surge and fire deployment
        uses: actions/setup-node@v1
        with:
          node-version: 14.19.0
      - run: npm install -g surge
      - run: npm install -g yarn
      - run: yarn install
      - run: yarn run build
      - run: surge public ${{ secrets.SURGE_DOMAIN }} --token ${{ secrets.SURGE_TOKEN }}
```

## License

MIT