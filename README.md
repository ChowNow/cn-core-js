# ChowNow Custom CoreJS

Our Ember projects use functionality that is not available in some of the browsers we support. We use 
ember-cli-babel to enable this functionality. This Ember addon optionally includes the babel-polyfill, which
is generated using, among other things, CoreJS.

We don't use ember-cli-babel's ability to include the babel-polyfill because:

1. This would cause all of CoreJS's polyfills to be included in our app.
2. We don't need all of those polyfills, some of which are non-standard.
3. It has been found that the Date-related polyfills cause issues with IE11.

Given this, we've decided to build our own custom shim explicitly including only those CoreJS polyfills which
we want and/or need. That's where this project comes in.

## Prerequisites

You will need the following things properly installed on your computer.

* [Git](http://git-scm.com/)
* [Node.js](http://nodejs.org/) (with NPM)

## Generating a New `custom-core-js.js` File

1. Globally install Browserify by running: `npm install -g browserify`
2. Clone this repo.
3. Change into this repo's directory.
4. Edit the file `custom-shim.js`, including only the desired shims, then save the file.
5. Generate a new `custom-core-js.js` file containing the source code for all of the shims in
`custom-shim.js` by running: `browserify custom-shim.js -o custom-core-js.js`.
6. Commit the new `custom-shim.js` and `custom-core-js.js` files and push changes to the remote repository.

Some notes:
* The shims in the `custom-shim.js` file represent a superset of the shims needed in all of the apps
that use this project's generated `custom-core-js.js`. That is, there will be shims in there that are needed
in some apps, but not in others. This is fine.
* Because of the above, we will rarely be removing shims from `custom-shim.js`. Use this as a rule 
of thumb: When in doubt, only add shims.
* Once you are done and satisfied with your changes, *please tag your release and use that tag in your 
project* according to our tag naming standards. This makes it so that upgrades to other projects have to be
done explicitly, thus preventing inadvertant breakage.

## Using `custom-core-js.js` in Your Project

*If you haven't integrated this into your project before...*

1. Go to your project repo's directory.
2. Open `bower.json`.
3. Add an entry for this project: `"cn-core-js": "https://github.com/ChowNow/cn-core-js.git#<your_tag>"`.
4. Run `bower install` to pull the tag.

Additionally, if you are using this in an Ember project, add
`app.import('bower_components/cn-core-js/custom-core-js.js');` to your `ember-cli-build.js` file to include 
it in your generated vendor.js. If using it in non-Ember projects, it will have to be included through other
methods.

*If you have already integrated this into your project...*

1. Go to your project repo's directory.
2. Open `bower.json`.
3. Update the entry for this project to use your recently-created tag.
4. Run `bower install` to pull the tag.

## More Documentation

For more information, refer to...

* [CoreJS](https://github.com/zloirock/core-js)
* [Browserify](http://browserify.org/)
* [Babel](http://babeljs.io/)
* [EmberCLI Babel](https://github.com/babel/ember-cli-babel)
