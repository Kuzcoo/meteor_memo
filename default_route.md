A default route
--------------

We need to provide routes to display our templates. The first route we write is the default one, where we're landing when we go to '/'.

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