Set up
------

* Create project:
```shell
meteor create my_project
cd $_
```

* Delete the default files created:
```shell
rm my_project*
```

* Create a public folder
```shell
mkdir public
```

* Create our app package
```shell
meteor create --package kuzcoo:app
```

* Adding our app package to our project

Yes, we need to add our own package to our meteor project in order to use it.
To do so, we have to set an environnement variables, `PACKAGE_DIRS`, to the path of our "packages" directory.
Here we'll use the "packages" directory of our project for the example.
```shell
export PACKAGE_DIRS='$(pwd)/packages'
```

Now add the package
```shell
meteor add kuzcoo:app
```

By now, we should have our app "package" in an "packages" folder at the root of our project.

* Create the arborescence
```shell
mkdir packages/app/{client,server,collections,routes,tests}
```
Following that [guide](https://meteor-guide.readthedocs.org/en/latest/structure/#structure-of-a-medium-sized-app), I chose a pretty classical structure within my package.

* Moving the test file to our tests directory
```shell
mv app-tests.js tests/app-tests.js
```

* Adding Meteor's core dependencies
```js
// ./package.js

Package.describe({
  name: 'app',
  version: '0.0.1',
  // Brief, one-line summary of the package.
  summary: '',
  // URL to the Git repository containing the source code for this package.
  git: '',
  // By default, Meteor will default to using README.md for documentation.
  // To avoid submitting documentation, set this field to null.
  documentation: 'README.md'
});

Package.onUse(function(api) {
  api.versionsFrom('1.2.1');
  api.use('ecmascript');
  // Adding core dependendies
  api.use(['templating', 'underscore']);
  api.use(['mongo'], ['client', 'server']);
  // Adding a router
  api.use('iron:router', 'client');
});

````
Inside "package.js" we declare package dependencies and the file we want our package to be aware of. 
ecmascript package permits to transpile our code from ES6 to ES5.

* Remove unsafe packages
```shell
meteor remove insecure autopublish
```

* Testing support

We'll use Tinytest for unit testing.

We modify the path of our test file.
```js
// ./package.js

Package.onTest(function(api) {
  api.use('ecmascript');
  api.use('tinytest');
  api.use('app');
  // here
  api.addFiles('tests/app-tests.js');
});
```
Here, for unit testing meteor will use tinytest and our app package itself.


For end-to-end testing we'll use starrynight with [Nightwatch](http://nightwatchjs.org/), that I found pretty easy to use and configure, and especially because there is valuable [documentation](http://starrynight.meteor.com/testing) and examples, thanks to Abigail Watson, who put a lots of efforts into [meteor-cookbook](https://github.com/awatson1978/meteor-cookbook).
Furthermore, Night watch offers a quite clear code structure with hidden built-in or custom methods. More on that later.

If you don't have `starrynight` (yes Meteor community is all about night life) yet, I would suggest you to install it globally.

```shell
npm -g install starrynight
```
Note that on OS X, we seem to have to use `sudo` for permissions issues.

Now, let's scaffold a nice testing environnement.

```bash
# generate the nigthwatch config file
starrynight generate-autoconfig
# before scaffolding we change dir
cd packages/app
# scaffolding a testing environnement
starrynight scaffold --framework nightwatch
```

By default the path to our "tests" directory is relative to the current dir,
and it seems that `run-tests` only works from the root of the project where it cans locate the "nightwatch.json" file.
So we edit our 'nightwatch.json' file and with a search and replace we change each path beginning with "./tests/" to "./packages/app/tests/".

ps: if you use Sublime Text you can just select './tests' and select all occurences pressing ctrl+cmd+G (os x). 


