# Proceed
### A skeleton Brunch.io project for building AngularJS apps based on angular-brunch-seed.
### Big uber-thanks to Scotch/Kyle Finley for authoring that!

[AngularJS](http://angularjs.org)
[Brunch](http://brunch.io)
[Karma](https://github.com/karma-runner/karma)
[Coffeescript](http://http://coffeescript.org)
[Jade](http://http://jade-lang.com)
[Stylus](http://http://learnboost.github.io/stylus)

#### ** Info **
This project is a fork of angular-brunch-seed.  It contains many extras that I use...not to mention a different
application format...that may be extraneous to your needs.

Brunch Supports:
* Coffeescript
* Jade
* Stylus (and Less)

Brunch Niceties:
* brunch watch --server ... runs a localhost instance, auto-tests, auto-reloads the page, and transpiles assets
* brunch build --production ... minifies all source into 3 files
* Source map support

## How to Use
* `npm install -g brunch`
* `brunch new https://github.com/fingerskier/Proceed.git`
* `cd Proceed`
* develop

TODO: remove? not sure this step is necessary
You must also install packages using bower. Either

```
bower install
```
or
```
./node_modules/.bin/bower install
```

*NOTE:* Depending upon your connection and processor speed the build can take
a substantial amount of time (3 - 15 minutes). The bower step is particularly
slow, because it downloads the complete git history. If you think that there
might be a problems, check you network traffic. If the build is still
downloading then it's still working.


TODO: remove this...
*NOTE:* Behind the scenes Angular-brunch-seed uses 
[jade-angular-brunch](https://github.com/GulinSS/jade-angularjs-brunch)
to compile and serve partials.
[jade-angular-brunch](https://github.com/GulinSS/jade-angularjs-brunch)
works by creating an Angular module named`'partials'` that adds the HTML
string of the partials to the `$templateCache`. For this to work you must add
`partials` to yours apps required modules list and include the `partials.js`
file in your `index.html` file.

If you are interested in the compiled HTML view the contents 
of the `_public/js/partials.js` file.


### Using html

By default angular-brunch-seed uses jade templates. If you would prefer to use
HTML run the command:

```
./scripts/compile-html.sh
```
All Jade file will be compiled to HTML and be placed in the `app/assets` directory.
Additionally, the `*.jade` files will be removed from the project. Any changes
that you make to the `app/assets/**/*.html` files will now appear in the browser.


### Running the app during development

* `./scripts/server.sh` to serve using **Brunch**

Then navigate your browser to [http://localhost:3333](http://localhost:3333)

*NOTE:* Occasionally the scripts will not load properly on the initial
load. If this occurs, refresh the page. Subsequent refresh will render
correctly. Also, the initial load will take longer then subsequent loads,
some where around 20 seconds is normal.


### Running the app in production

* `./scripts/production.sh` to minify javascript and css files.

Please be aware of the caveats regarding Angular JS and minification, 
take a look at [Dependency Injection](http://docs.angularjs.org/guide/di)
for information.


### Using Bower

Angular-brunch-seed uses [Bower](http://twitter.github.com/bower/) for package
management. To add or update dependencies, modify the `component.json` file
and run `bower install`. The component will be added to the `vendor` directory.


### Running unit tests

* `./scripts/test.sh` to run unit tests with [karma](https://github.com/karma-runner/karma)

Notes:

- Karma will run tests on save. To insure that changes are saved be sure
  to have `./script/server.sh` or `./script/development.sh` running in the console.
- Set the browsers that you would like to target in the `/test/karma.conf.js` file
  E.g. `browser = ["ChromeCanary", "Firefox"]`


### End to end testing

* run the app in development mode as described above using a separate terminal
* `./scripts/test-e2e.sh` to run e2e tests with
  [karma](https://github.com/karma-runner/karma) using Angular's scenario runner


### Common issues

Initial load does not render correctly; scripts are not loading. 
- Occasionally the scripts will not load properly on the initial load. If this
  occurs, refresh the page. Subsequent refresh will render correctly.

`EMFILE` error
- EMFILE means there are too many open files. Brunch watches all your project
  files and it's usually a pretty big number. You can fix this error with
  setting max opened file count to bigger number with command `ulimit -n 10000`.

The complete [Brunch FAQ](https://github.com/brunch/brunch/blob/master/docs/faq.rst)


### Receiving updates from upstream

```bash
git pull origin master
```

## Directory Layout

    _public/                  --> Contains generated file for servering the app
                                  These files should not be edited directly
    app/                      --> all of the files to be used in production

      assets                  --> a place for static assets. These files will be copied to
                                  the public directory un-modified.
        img/                  --> image files
        partials/             --> angular view partials (partial HTML templates)
          nav.html                If you are using HTML you may modify these files directly.
          partial1.html           If you are using Jade these file will be update from their *.jade counterpart
          partial2.html
        index.html            --> app layout file (the main html template file of the app).

      partials/               --> Jade partial files. This file will be converted to HTML upon save.
        nav.jade                  If you are using HTML this directory will not be present. You will find the template file
        partial1.jade             in the `app/assets/partials` directory instead.
        partial2.jade             If you are using Jade these file will be converted to HTML and compiled into 
                                  `_public/js/partials.js` upon save.
      scripts/                --> base directory for app scripts
        controllers.js        --> application controllers
        directives.js         --> custom angular directives
        filters.js            --> custom angular filters
        services.js           --> custom angular services

      styles/                 --> all custom styles. Acceptable files types inculde:
                                  less, and stylus
        _override.less        --> styles that should be loaded after bootstrap.
        _variables.less       --> bootstrap variables to be used during the compilation process
                              --> **NOTE the underscore (_). Files begining with an underscore 
                                  will not automatically be compiled, they must be imported.
        app.less              --> a file for importing styles.
      app.coffee              --> application definition and routes.
      index.jade              --> Index file. This will be converted to assets/index.html on save
      init.coffee             --> application bootstrap

    bower_components/         --> The bower_components dirctory is populated by Bower.
                                  It contains  Angular, Bootstrap Font-Awesome 
                                  and other utility files.
    node_modules              --> NodeJS modules

    scripts/                  --> handy shell scripts
      compile-html.sh         --> compiles *.jade file to *.html file and places them in app/assets
      compile-tests.sh        --> compiles coffeescript test to javascript
      development.sh          --> compiles files and watches for changes
      init.sh                 --> installs node modules
      production.sh           --> compiles and compresses files for production use
      server.sh               --> runs a development server at `http://localhost:3333`
      test.sh                 --> runs all unit tests
      test-e2e.sh             --> runs all end-to-end tests using Testacular

    test/                     --> test source files and libraries
      app/
        scenarios.coffee      --> end-to-end specs
      unit/
        controllers.spec.js   --> specs for controllers
        directives.spec.js    --> specs for directives
        filters.spec.js       --> specs for filters
        services.spec.js      --> specs for services
      vendor/
        test-results.xml      --> Karma test resuls
        karma-e2e.conf.js     --> Karma end-to-end tests config
        karma.conf.js         --> Karma unit tests config

    vendor/                   --> The vendor directory is can be used for 3rd Party libraries.
                                  Any files located in this directory will be included in js/vendor.js
  bower.json                  --> Bower component config
  config.coffee               --> Brunch config
  package.json                --> node modules config

## Contributers

[Complete list of code contributers](https://github.com/scotch/angular-brunch-seed/graphs/contributors)

For more information on angular please check out <http://angularjs.org>
