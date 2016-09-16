# Here Be Dragons -- The Monolith

https://joind.in/event/pnwphp-2016/here-be-dragons-what-its-really-like-to-slay-a-monolith 

## Code Level Problems at Refinery 29

* un-reason-able
* duplication
* NIH
* Low test coverage
* Low confidence
* Caused lots of fire drills

## Architecture

* No boundaries


---

Define your interface and document it. APIs are a first class citizen.   

Single, canonical representation rather than platform specific endpoints.  Make endpoints reusable.  

Use contexts if you have to (different transformers for different clients).

Write as little code as possible.  

* Leverage composer
* Use packagist 


### How do you pick the right tools?

What makes a good package: phppackagechecklist.com 

* High quality
* Well tested
* Well documented
* Well supported
* Low bus factor (How many maintainers?)

### Be as explicit as possible -- no magic

* No public properties
* 
      

