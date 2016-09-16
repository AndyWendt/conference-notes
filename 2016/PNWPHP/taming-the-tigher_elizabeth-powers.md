# Taming the Tiger

"The laws of physics apply to no matter what you are doing in computing."

Arrays are evil.  When you use arrays, you are putting data into your memory. 

 Make sure whatever data that you put into an array, is only the data that you need.  If the framework or tool you are using doesn't support that, don't use it.  

Best action is often not to use `array_map`.  Work with one record at a time.  

PHP is really stingy with memory.  Once you ask for the memory once, it doesn't release it.  So you must keep memory usage low.  It doesn't release the memory until the process stops.  With FPM, that is fast.     

Don't use `fetch_all` with PDO. 

 Always page your database data.  


 
