reserver
========

A tiny dev server that rebuilds your static, single-page app when you refresh your browser.

## Why not Grunt/Gulp/etc

- I don't like writing config files
- I don't like installing plugins that wrap existing modules (eg gulp-browserify)
- I don't want live-reload refreshing my browser in the background
- I don't want temporary build/debug files to hang around in my server `/www` directory
- I want compilation errors displayed in the browser
- I want my CSS compiled from [LESS](http://lesscss.org) or [Stylus](http://learnboost.github.io/stylus/) and [Autoprefixed](https://github.com/postcss/autoprefixer)
- I want my JavaScript or CoffeeScript browserified
- I want my app's console.log output to show up in the terminal
- I want parallel builds in under 100ms

## Conventions

Reserver is a built-tool-by-convention.  Instead of writing config files, it expects your app to have the following structure:

```
src/html/index.ext -> compiled to //index.html
src/js/index.ext   -> compiled to //index.js
src/css/index.ext  -> compiled to //index.css
```

Inside each directory there needs to be a file called `index` with it's appropriate _extension_.  Based on the extension, reserver will compile the index file as necessary.  For example if you have `/css/index.less` then `less` will be used to compile your CSS.  The `index` file is responsible for including any dependencies, for example using `@import` in CSS or `require()` in JavaScript.

Supported extensions are:

```
index.less   -> compiled with Less CSS
index.styl   -> compiled with Stylus
index.ejs    -> compiled with EJS
index.jade   -> compiled with Jade
index.hb     -> compiled with Handlebars
index.coffee -> compiled with coffeeify
index.js     -> compiled with browserify
index.es6    -> compiled with browserify + babel
index.jsx    -> compiled with browserify + react presets for babel
index.html   -> copied
index.css    -> copied
```

Your `index.html` should include the compiled JS & CSS as follows:

```html
<head>
  <link rel="stylesheet" href="index.css" type="text/css" media="screen" />
  <script type="text/javascript" src="index.js"></script>
</head>
```

## Usage

Install:

```bash
$ sudo npm install -g browserify
$ sudo npm install -g reserver
```

Run reserver on port `8080` looking for html/js/css folders in `src` and serving static files from `www`:

```bash
$ reserver ./src ./www --port 8080
```

Open up your browser and visit `localhost:8080`.  Change files in `/src`, refresh your browser and your app gets re-compiled in the background.


## Requirements

The build system requires that any necessary build modules are installed globally or locally to `node_modules`.

For example if you're using [LESS CSS](http://lesscss.org), make sure you've installed the module globally on your machine.

For node to find your global modules, make sure NODE_PATH is set correctly:

```bash
$ export NODE_PATH=/usr/local/lib/node_modules
```


## To Do

- Add support for Type-Script
