# grunt-mocha-phantomjs

> A simple wrapper to run client-side mochas tests using mocha-phantomjs

## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-mocha-phantomjs --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-mocha-phantomjs');
```

## The "mocha_phantomjs" task

_Run this task with the `grunt mocha_phantomjs` command._

Task targets, files and options may be specified according to the grunt [Configuring tasks](http://gruntjs.com/configuring-tasks) guide.

[PhantomJS][] is installed when installing using NPM. 

[PhantomJS]: http://www.phantomjs.org/

### Options

#### reporter
Type: `String`  
Default: `spec`

The reporter that should be used. See [the supported reporters](https://github.com/metaskills/mocha-phantomjs#supported-reporters) for more information.

#### urls
Type: `Array`  
Default: `[]`

Absolute `http://` or `https://` urls to be passed to PhantomJS. Specified URLs will be merged with any specified `src` files first. Note that urls must be served by a web server, and since this task doesn't contain a web server, one will need to be configured separately. The [grunt-contrib-connect plugin](https://github.com/gruntjs/grunt-contrib-connect) provides a basic web server.

Additional arguments may be passed. See [mocha-phantomjs's](https://github.com/metaskills/mocha-phantomjs#usage) usage.

### Usage examples

#### Basic usage

```js
// Project configuration.
grunt.initConfig({
  mocha_phantomjs: {
    all: ['test/**/*.html']
  }
});
```

#### Local server
Include the [grunt-contrib-connect plugin][] to run a local server
[grunt-contrib-connect plugin]: https://github.com/gruntjs/grunt-contrib-connect

```js
// Project configuration.
grunt.initConfig({
  mocha_phantomjs: {
    all: {
      options: {
        urls: [
          'http://localhost:8000/test/foo.html',
          'http://localhost:8000/test/bar.html'
        ]
      }
    }
  },
  connect: {
      server: {
        options: {
          port: 8000,
          base: '.',
        }
      }
    }
});

grunt.registerTask('test', ['connect', 'mocha_phantomjs']);
```

### Notes
This is a very basic implementation of mocha-phantomjs. Failed tests and errors do not bubble up for custom reporting. The idea of this is to be mainly used by a CI and let the CI manage the error reporting.