Result of removing "autopublish" and "insecure"
----------------------------------------------

Since we removed `autopublish` and `insecure` we have to know at least two things:
  
1. We can't fetch data from the database

2. Client-side, we can't update, insert, or delete to the DB

### 1. Subscribe and publish

Because we removed the autopublish package, we can't GET any data from the database.

Solution: Add a "publisher" server-side to authorize any subscriber to retrieve some data. In the same time add a "subscriber" client-side to subscribe to this publisher.

First, we create some files in the right place:
```shell
touch client/subscribers.js
touch server/publishers.js
```
Maybe we could find better names for these files.

```js
// subscribers.js

Meteor.subscribe('fetchItems');

// publishers.js

Meteor.publish('fetchItems', function () {
  return Items.find({});
});
```

### 2. Writing methods

Client side, we have to call a "method" (basically, it's a function), that is defined server side.

Create the file:
```shell
touch server/methods.js
```

Write the methods:
```js
// ./server/methods.js

Meteor.methods({
  'addItem': function (item) {
    Items.insert(item);
  };
});
```

Then from our client directory we could call this method.
Let's build some template and events to show how it works.

Complete the home template:
```jade
// client/home.jade
// we add an input field to our home template to add items

template(name='home')
  h3 This is the Home Page pal!
  input#new-item(type='text' placeholder='Item's name)
```

Then we create an item and items template:
```shell
touch client/{item,items}.{js,jade}
```

The item one:

```jade
template(name='item')
  li {{name}}
```

The items one, which contains a list of item
```jade
template(name='items')
  div.items
    ul 
      | {{#each items}}
      | {{> item}}
      | {{/each}}
```

That's for each item in an item list we want an item template appended to the 'ul'.

'items' is a variable defined for the 'items' template, storing the items retrived from the database.
However so far we didn't defined any variable, so let's do it.

```js
// ./client/items.js

Template.items.helpers({
  items: function () {
    return Items.find({});
  }
});
```

'items' helper is now accessible from our 'items' template with double curly braces.
And we can do it because we subscribe all our client side app to 'fetchItems'.

Just insert manually some stuff in the db to check everything's alright.
First create the collection

```shell
touch collections/items.js
```

```js
// ./collections/items.js

Items = new Mongo.Collection('items');
```

In your CLI:
```shell
meteor mongo
```

When the prompt shows up:
```shell
db.items.insert({name: 'item1', createdAt: new Date()});
db.items.insert({name: 'item2', createdAt: new Date()});
```

Let's check:
```shell
db.items.find({});
```

Okay, they're in!

Now we wan't to be able to insert the sme stuff from the template.

What do we need to do?

When we press enter after filling the input field used for adding items, we want that item to be added to the 'items' collection.
BEcause this input field is in the home template, let's defined an event handler inside its associated js file.

```js
// ./client/home.js

Template.home.events({
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

Now if we go to our home page, and add an item. It should appear appended to the list of items. Indeed, the view seems to render again automatically when we manipulate the data in our collection. Great!

What's next ?