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

* Make the arborescence:
```shell
mkdir client server public private collections routes
```

* Add a router:
```shell
meteor add iron:router
```

* Remove unsafe packages
```shell
meteor remove insecure autopublish
```
