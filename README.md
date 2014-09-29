# grunt-suitcss [![Build Status](https://travis-ci.org/simonsmith/grunt-suitcss.svg?branch=master)](https://travis-ci.org/simonsmith/grunt-suitcss)

> Preprocess and validate [SUIT CSS](http://github.com/suitcss/suit) components

This task will build SUIT CSS components, check them for conformance and then preprocess the resulting file. It can accept `.css` files or a [component(1)](https://github.com/component/component) JSON file.

**Build** - If a `component.json` file is used then dependencies are resolved and built using [component-resolver](https://github.com/component/resolver.js) and [component-build](https://github.com/component/build.js)

**Conform** - Individual components are checked for conformance with [Rework Suit Conformance](https://github.com/suitcss/rework-suit-conformance)

**Preprocess** - The resulting file is pre-processed using [SUIT CSS preprocessor](https://github.com/suitcss/preprocessor). This will run the file through [Autoprefixer](https://github.com/ai/autoprefixer) and allow usage of W3C-style variables and calc().

###Example setup
To see how this task can be used with actual SUIT components, check [this example repository](https://github.com/simonsmith/suitcss-example)


## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-suitcss --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-suitcss');
```

## SUIT CSS task

### Overview
In your project's Gruntfile, add a section named `suitcss` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  suitcss: {
    options: {
      // Task-specific options go here.
    },
    your_target: {
      // Target-specific file lists and/or options go here.
    },
  },
});
```

### Options

#### options.conform
Type: `Boolean`
Default value: `true`

Pass each component through the [Rework Suit Conformance](https://github.com/suitcss/rework-suit-conformance) library. If conformance fails an error will be output to the CLI and the task will be stopped

#### options.preprocess
Type: `Boolean`
Default value: `true`

Pass the resulting CSS file through the [SUIT CSS preprocessor](https://github.com/suitcss/preprocessor)

#### options.resolveOpts
Type: `Object`
Default value: `{ install: true }`

Options that can be passed to the [component-resolver](https://github.com/component/resolver.js).

**Note:** `verbose` is always set to true to allow output to the CLI

#### options.preprocessOpts
Type: `Object`
Default value: `{}`

Options that can be passed to the [SUIT CSS preprocessor](https://github.com/suitcss/preprocessor)

### Usage Examples

#### Default Options

##### Building SUIT CSS components with component(1)
In this example, the default options are used to build a SUIT CSS component. The source file **must** be a `component.json` file for the task to know it has to fetch dependencies and build them. Each component is passed through the conformance checker and the resulting file is then passed through the SUIT CSS preprocessor.

```js
grunt.initConfig({
  suitcss: {
    your_target: {
      files: {
        'dest/built.css': 'path/to/component.json',
      }
    }
  },
});
```

##### Preprocessing normal CSS files

It's common to use SUIT CSS components even if component(1) is not used, for example installing them from a different package manager like Bower. In this case passing the task one or more CSS files will mean they are checked for conformance individually and then preprocessed as a complete package. They are built in the order they are passed in.

```js
grunt.initConfig({
  suitcss: {
    your_target: {
      files: {
        'dest/built.css': ['components/tweet.css', 'components/button.css'],
      }
    }
  }
});
```

#### Custom Options
In this example, custom options are used to disable `preprocess`.

**Note** If both `conform` and `preprocess` are set to false then `grunt-suitcss` will simply return the untouched CSS.

```js
grunt.initConfig({
  suitcss: {
    your_target: {
      options: {
        preprocess: false,
      },
      files: {
        'dest/built.css': ['components/tweet.css', 'components/button.css'],
      }
    }
  }
});
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History

See [GitHub releases](https://github.com/simonsmith/grunt-suitcss/releases)
