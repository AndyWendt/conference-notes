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
    - Requires great docs 

---
### Caching

Caching is underutilized in REST even though it is in the spec. 

---

### Authentication 

- Kill basic Auth
    - Everybody has that one password that they haven't reset in 6 years

- OAuth
- JWT

### Security

Don't rely on just one method of protection 

Be aware of SQL injection.  You MUST sanitize your data.  You don't know what your users will send back.  


---

Use Postman if you are not.  

Maintenance -- need to plan for maintenance. 

Don't force people to log into your documentation.  

Don't put name/password in url structure.  


---

SDKs, provide them if you can.  Keep them up to date with API and documentation.    

Undisturbed REST book.   

