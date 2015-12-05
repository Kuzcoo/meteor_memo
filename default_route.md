A default route
--------------

We need to provide a route for our home template. This will be our default landing page.

First, write some template to show.

```shell
touch client/home.{jade,js}
```

We create a js file with the same name because we may need it later.

```jade
template(name='home')
  h1 This is the Home Page pal!
```

And the route:

```js
// ./routes/index.js

Router.route('/', {
  template: 'home'
});