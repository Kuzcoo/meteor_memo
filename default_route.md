A default route
--------------

We need to provide routes to display our templates. 
The first route we write is the default one, where we're landing when we go to '/'.

So what we need to do ?
  1. create a default route
  2. create a "home" template 
  3. Link those two

Okay, with this tiny list let's write our tinytests

```js
// ./tests/app-client-tests.js

// Here we will check the existence of our templates
Tinytest.add('Check Templates', test => {
  test.isNotUndefined(typeof Template.home, '"home" should exists');
});

// here we will chack our routes
Tinytest.add('Check Routes', test => {
  test.isNotNull(Router.findFirstRoute('/'), '"/" should exists');
});
```

Launch your servers
```bash
# launch your project
meteor
# launch your tests
meteor test-packages
```

Those two tests fail, as expected.

* Define a route

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
  // ...
  // adding the route file client side
  api.addFiles('routes/index.js', 'client');
});

````

* Create files and add them in your package file

```shell
touch client/home.{jade,js}
```

We create a js file with the same name because we may need it later.

List those files in your package.

```js
// ./package.js

Package.onUse(function(api) {
  // ...
  // adding the route file client side
  api.addFiles(['client/home.html', 'client/home.js'], 'client');
  api.addFiles('routes/index.js', 'client');
});

````
* Create the home template

```jade
template(name='home')
```

Let's see our test on testing tab.
And now they should pass!


* Create content of the home template

What do we want in our "home" template.
Just a title for now: "This is the Home Page pal!".

Put it into a test.
For that part we'll use Nightwatch.

```js
// ./tests/nightwatch/walkthroughs/app-client-tests.js

module.exports = {
  'Layout': function (client) {
    client
      .url('http://localhost:3000') // get the page
      .sectionBreak('Home template') // some section title of what we're testing
      .verify.elementPresent('h1') // check for the presence of an h1 element
      .assert.containsText('h1', 'This is the Home Page pal!') // check its content
      .end();
  }
};

``` 

Run it.
```bash
starrynight run-tests --framework nightwatch --env phantomjs
```

It fails. So let's rewrite our template.

```jade
template(name='home')
  h1 This is the Home Page pal!
```


Run again, and it should pass.


