# Give Me A Rest -- Amanda Folson

APIs allow you to shard off services.  

## Design

Treat your API and content similarly.  

Feedback needs to make it into the spec.     

## What is REST?

A resource is a gateway to an area of your application.  Use plural forms of entities unless it really makes sense not to.  Cart vs carts.

GET -- get data

POST -- used to create or manipulate data.    

PUT -- update a resource.  Replaces data, idempotent.   

PATCH -- partially update a resource

DELETE -- Haha  

OPTIONS -- what options are available  


Content-types allow you to define what the request and response bodies' content is.  

Don't feel like you have to use all of the status codes.   

HATEOAS is like choose your own adventure.  

---

Versioning.  Don't increase your version too quickly since other devs may loose confidence.  

- In the URI
    - Easy to get started and recognizable
- In the content-type 
    - Requires more documentation
    - Not obvious
- In Custom header
    - Don't do this unless you have a really compelling reason  



