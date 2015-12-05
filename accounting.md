Accounting
----------

Oh yeah, of course I want some back office thing access, from where I can handle those items. In fact that's not a todo which everyone can add, delete update, and whatever, do to my items. I just want to add those items, and show them on my front page. The rest, we want to handle it, alone, in the dark.

So I want personnal, private, safe, restrcited access to my back office.

### Adding the accounts package

Let's add this package:

```shell
meteor add accounts-password
```

What do we need now ? Let's write a list divided in two parts:

**I. Templating and routing**
  * Login template
  * Admin template
  * Route to login template
  * Route to admin template

**II. Authentication**
  * A user account
  * Submit handler for login



### I. Templating and routing

Writing this memo, seems that meteor is obsessed with templates. That must be the core stuff of its process. Template word everywhere, you'll see!

So (straight to the jade files, now you're a master with `touch`)

* Login template

```jade
// ./client/login.jade

template(name='login')
  form.login-form
    label(for='username') Username
      input#username(type='text' name='username')
      br
    label(for='password') Password
      input#password(type='password' name='password')
      br
    input(type='submit')
```

* Admin template:
```jade
template(name='admin')
  h1 Admin Page!
  input.#new-item(type='text' placeholder='Item's name')
  {{> items}}
```

Okay, that's awesome because we just apllied an important principle: DRY.
Don't repeat yourself, we used twice the same template preventing us from rewriting the same boring thing again.
Lazyness is the key of mastery.

Of course, we have to refactor our home page template deleting the input field and transpose our keypress event to run inside the admin template.

```js
// ./client/admin.js

Template.admin.events({
  'keypress #new-item': function (event, template) {
    // check if the enter key was pressed
    // and if the user typed down some characters
    if (event.which === 13 && event.target.value) {
      Method.call('addItem', {
        name: event.target.value,
        createdAt: new Date()
      }, function () {
        // if it's all good clear the input field
        event.target.value = '';
      });
    }
  }
});
```

* Routes

```js
// ./routes/index.js
// following the first route defined
Router.route('/login', {
  template: 'login'
});

Router.route('/admin', {
  template: 'admin'
});
```

### II. Authentication





