# Taming the Tiger

https://en.wikipedia.org/wiki/Computer_science   
http://www.slideshare.net/auroraeosrose  

>"The laws of physics apply to no matter what you are doing in computing."

### Arrays 

Arrays are evil.  When you use arrays, you are putting data into your memory. 

 Make sure whatever data that you put into an array, is only the data that you need.  If the framework or tool you are using doesn't support that, don't use it.  

Best action is often not to use `array_map`.  Work with one record at a time.  

PHP is really stingy with memory.  Once you ask for the memory once, it doesn't release it.  So you must keep memory usage low.  It doesn't release the memory until the process stops.  With FPM, that is fast.     

Don't use `fetch_all` with PDO. 

 Always page your database data.  

Use generators or iterators instead of arrays.  Generators are the lazy man's iterators.  

---

### Streams


Go to wikipedia and lookup Computer Science if you haven't gone through a proper CS course.  


In PHP, everything uses streams.  All file and IO access goes through the streams access layer.   

>"Whatever you choose to do depends on what you are trying to accomplish."

Only attach compression on a write stream.  


Streams have an input and output state.  Will need to cache until you get to a certain point.    

Often better to use a different language for complex things than PHP if needed (C, etc).  

Process with the Appropriate Tools.  Sometimes you should do the work in a data store (DB, etc).  

Offload work so that you don't keep the user waiting.  

Microservices are essentially little job servers.  

Network socket types: 

* stream
* datagram
* raw



