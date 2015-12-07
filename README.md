#Meteor, starting the right way
[Work in progress]
Table of Contents
  * [Introduction](#introduction)
  	* [Resources](#resources)
  * [Set up](set_up.md)
  * [A default route](default_route.md)
  * [Result of removing autopublish and insecure](autopublish_insecure.md)
    1. [Subscribe and publish](autopublish_insecure.md#1-subscribe-and-publish)
    2. [Methods](autopublish_insecure.md#2-methods)
  * [Accounting](accounting.md)
    1. [Templating and routing](accounting.md#i-templating-and-routing)
    2. [Authentication](accounting.md#ii-authentication)

Introduction
------------

I read some stuff about meteor, trying to grasp the way it works. I was very happy to learn it, since the 'getting started' is quite easy, and everything pops up like magically. In fact, that seems great for rapid prototyping, as I could read [here](https://meteor-guide.readthedocs.org/en/latest/structure/#the-building-blocks-of-a-meteor-app), but it comes pretty painful when you want to make bigger plans, and especially for testing.

I didn't intend to write medium size apps, just a tiny one, but I wanted to write it he good way, following good practices. Every piece of sheet wrote by - seems to be - skilled programmer tells it so: TDD guys, TDD!
They encourage us to write tests first and writing the app code after.
Tests are guidelines to build the app, asserting that being capable of puting words to express what we want to code is the key to top quality and bug free code. Okay, so far, I just wanted to make the thing work, see my pages and cool javascript effects, or by the time I read those advices I looked at my code, and thought "too late".

However, Meteor seems very great stuff. After spending a day trying to find the most adequate testing suite for Meteor, I just wanted to give up, going back to my expressjs projects and all those configurations. Come on, no way, that's too complicated, all this set up to serve my extra light database and a bunch of routes.

So I dug deeper, everything I read was outdated. When I came to find a solution that could work, oh, there was always something that didn't work. Okay, maybe a little trick to do, let's hack into it. I find an issue relating the same problem. The author makes an update in the wiki for that case. Great, let's see this wiki. Oh this wiki is now on the official wiki of the testing module. Click, 404. After some research I comes out that the open source wiki became a book. Not so cheap. Yes that's work, but I just want to do basic tests to give meteor a shot, see if I can use it the right way!

Well, I finally understood that the good way to go is to use packages structure.
Packages! And now, we are close to boring configuration, but that's still great, and we avoid to pollute the global namespace.

We could see this contribution as a summary of informations I gathered here and there.
Many thanks to the authors of those open [resources](#resources).

Let's dive into set up, and after that everything should be smooth.


### Resources

* [https://meteor-guide.readthedocs.org](https://meteor-guide.readthedocs.org)
* [https://themeteorchef.com/recipes/writing-a-package/#tmc-packagejs](https://themeteorchef.com/recipes/writing-a-package/#tmc-packagejs)
* [https://github.com/awatson1978/meteor-cookbook](https://github.com/awatson1978/meteor-cookbook)
*	[http://starrynight.meteor.com/testing](http://starrynight.meteor.com/testing)
* [http://nightwatchjs.org/](http://nightwatchjs.org/)
* [http://meteortips.com/second-meteor-tutorial/](http://meteortips.com/second-meteor-tutorial/)
* [https://scotch.io/tutorials/building-a-slack-clone-in-meteor-js-getting-started](https://scotch.io/tutorials/building-a-slack-clone-in-meteor-js-getting-started)














