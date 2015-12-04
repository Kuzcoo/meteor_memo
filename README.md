#Meteor, starting the right way
Introduction
------------

I read some stuff about meteor, trying to grasp the way it works. I was very pleased until I came aware that all that I did so far was unsafe, and I had to refactor the code and remove some packages to follow along. 

So I decide to write on the paper (well on an HTML marked up page), what I have to do in order to create, straight, a  - as it seems - good MeteorJS app.


Setting everything's up
-----------------------

• Create project:
```shell
meteor create my_project
cd $_
```

• Delete the default files created:
```shell
rm my_project*
```

• Make the arborescence:
```shell
mkdir client server public private collections routes
```

• Add a router:
```shell
meteor add iron:router
```

• Remove unsafe packages
```shell
meteor remove insecure autopublish
```

And now what ?
--------------

• We defined a router

First, write some template to show.

```shell
touch client/home.{jade,js}
```

We create a js file with the same name because we may need it later.

```jade
template(name='home')
	h3 This is the Home Page pal!
```

And the route:

```js
// ./routes/index.js

Router.route('/', {
	template: 'home'
});
```
Result of removing "autopublish" and "insecure"
----------------------------------------------

Since we removed `autopublish` and `insecure` we have to know at least two things:
	
• We can't fetch data from the database

Since we removed the autopublish package, we can't GET any data from the database.

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

• Client-side, we can't update, insert, or delete to the DB 

Client side, we have to call a "method" (basically, it's a function), that is defined server side.

Come on:
```shell
touch server/methods.js
```



