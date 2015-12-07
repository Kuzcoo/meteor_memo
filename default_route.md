A default route
--------------

We need to provide routes to display our templates. 
The first route we write is the default one, where we're landing when we go to '/'.

* Defining a route

Create the right file.
```shell
touch routes/index.js
```
And add the route
```js
// ./routes/index.js

Router.route('/', {
  template: 'home'
});
```

In order to make it visible to our package we have to add the file to it.
Let's open our package.js file where we left it.

```js
// ./package.js

Package.onUse(function(api) {
  api.versionsFrom('1.2.1');
  api.use('ecmascript');
  // Adding core dependendies
  api.use(['templating', 'underscore']);
  api.use(['mongo'], ['client', 'server']);
  // Adding a router
  api.use('iron:router', 'client');
  // adding the route file client side
  api.addFiles('routes/index.js', 'client');
});

````
* Write our first test

```js
// ./tests/nightwatch/walktroughs/appLayout.js
// this the default file created by the scaffolding script
// delete its content
module.exports = {
  'Layout': function (client) {
    client
      .url('http://localhost:3000') // connect to our page
      .sectionBreak('Home Page') // 
      .verify.elementPresent('h1') // check if we got an h1 element
      .assert.containsText('h1', 'Home Page') // h1's text
      .end(); // end the test
  }
}
```

* Boot your server
```shell
meteor
```

* Start your test:
```shell
starrynight run-tests --framework nightwatch --env phantomjs
```

Oh yeah both tests fail.
The router doesn't find the "home" template.

* Create the home template

```shell
touch client/home.{jade,js}
```

We create a js file with the same name because we may need it later.

```jade
template(name='home')
  h1 This is the Home Page pal!
```

Now let's add those files to our package.

```js
// ./package.js

Package.onUse(function(api) {
  api.versionsFrom('1.2.1');
  api.use('ecmascript');
  api.use(['templating', 'underscore']);
  api.use(['mongo'], ['client', 'server']);
  api.use('iron:router', 'client');

  api.addFiles(['client/home.html', 'home.js'], 'client');
  api.addFiles('routes/index.js', 'client');
});

````

Let's compile our jade file and go with it!
Run the tests, all good!


