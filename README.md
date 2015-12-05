#Meteor, starting the right way

Table of Contents
  * [Introduction](#introduction)
  * [Setting everything up](#setting-everything-up)
  * [Basic route](basic_routes.md)
  * [Result of removing autopublish and insecure](autopublish_insecure.md)
  * [Accounting](accounting.md)

Introduction
------------

I read some stuff about meteor, trying to grasp the way it works. I was very pleased until I came aware that all that I did so far was unsafe, and I had to refactor the code and remove some packages to follow along. 

So I decide to write on the paper (well on an HTML marked up page), what I have to do in order to create, straight, a  - as it seems - good MeteorJS app.

Setting everything up
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

















