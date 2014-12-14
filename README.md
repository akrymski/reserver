reserver
========

A tiny dev server that rebuilds your single-page app.

## Why not Grunt/Gulp/etc

- I don't like writing config files
- I don't like installing plugins that wrap existing modules (eg gulp-browserify)
- I don't want live-reload refreshing my browser in the background
- I don't want temporary build/debug files to hang around in my server `/www` directory
- I want compilation errors displayed in the browser
- I want my CSS compiled from Less or Stylus
- I want my JavaScript or CoffeeScript browserified
- I want my app's console.log output to show up in the terminal

## Conventions

Reserver is a built-tool-by-convention.  Instead of writing config files, it expects your app to have the following structure:

```
/html/index.ext -> compiled to index.html
/js/index.ext   -> compiled to index.js
/css/index.ext  -> compiled to index.css
```

Inside each directory there needs to be a file called `index` with it's appropriate _extension_.  Based on the extension, reserver will compile the index file as necessary.  For example if you have `/css/index.less` then `less` will be used to compile your CSS.

Supported extensions are:

```
index.less   -> compiled with Less CSS
index.styl   -> compiled with Stylus
index.ejs    -> compiled with EJS
index.jade   -> compiled with Jade
index.hb     -> compiled with Handlebars
index.coffee -> compiled with coffeeify
index.js     -> compiled with browserify
```

## Usage

Install:

```bash
$ sudo npm install -g browserify
$ sudo npm install -g reserver
```

Run reserver on port `8080` looking for html/js/css folders in `/src` and serving static files from `/www`:

```bash
$ reserver ./src ./www --port 8080
```

Open up your browser and visit `localhost:8080`.  Change files in `/src`, refresh and your app gets rebuilt in the background.


## Requirements

The build system requires that any necessary build modules are installed globally.

For example if you're using [LESS CSS](http://lesscss.org), make sure you've installed the module globally in your machine.

For node to find your global modules, make sure NODE_PATH is set correctly:

```bash
$ export NODE_PATH=/usr/local/lib/node_modules
```


## To Do

- Add support for Type-Script
