# REST API

Representational state transfer.
https://netboxlabs.com/docs/netbox/integrations/rest-api/

Employs HTTP requests and JSON (JavaScript Object Notation to facilitate create, retrieve, update adn delete (CRUD)
operations on objects within NetBox (or any application).
Types of operation :
* `GET` : Retrieve and object or list of objects
* `POST` : Create an object
* `PUT`/ `PATCH` :  Modify an existing object.
  - `PUT` requires all mandatory fields to be specified
  - `PATCH` expects only the field that is being modified to be specified.
* `DELETE` : Delete an existing object.
* `OPTIONS`

  
### Postman 
* DEsktop app/ web UI for REST API requests. Allows for you to keep collections of requests to be bale to repeat and troubleshoot, creating body of requests and returning outputs in multiple formats (JSON, ...)


Example command to  `GET` (retrieve) all sites in database.
```
curl --location 'http://dockernetbox1.bounceme.net:8000/api/dcim/sites/?brief=True' --header 'Authorization: Tok
en dcebd423e17942513f4d864f562b1f1fd123e02c'
```

> Note that on the end of the URL  `?brief=True` is used to return a simple list with minimal representration of
> the objects, with object referencing the output can be quite long and somewhat confusing so the brief mode results
