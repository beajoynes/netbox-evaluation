# REST API

Representational state transfer.

Employs HTTP requests and JSON (JavaScript Object Notation to facilitate create, retrieve, update adn delete (CRUD)
operations on objects within NetBox (or any application).
Types of operation :
* `GET` : Retrieve and object or list of objects
* `POST` : Create an object
* `PUT`/ `PATCH` :  Modify an existing object. 


Example command to  `GET`  all sites in database.
```
curl --location 'http://dockernetbox1.bounceme.net:8000/api/dcim/sites/?brief=True' --header 'Authorization: Tok
en dcebd423e17942513f4d864f562b1f1fd123e02c'
```

> Note that on the end of the URL  `?brief=True` is used to return a simple list with minimal representration of
> the objects, with object referencing the output can be quite long and somewhat confusing.
