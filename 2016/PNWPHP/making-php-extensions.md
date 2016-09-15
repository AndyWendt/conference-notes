# Making PHP Extensions

## Resources

https://github.com/auroraeosrose/php-extensions-code

http://www.slideshare.net/auroraeosrose/php-extensions-45834933 

Other presentations by Elizabeth Smith: http://www.slideshare.net/auroraeosrose  

https://nikic.github.io/2015/05/05/Internal-value-representation-in-PHP-7-part-1.html   
https://nikic.github.io/2015/06/19/Internal-value-representation-in-PHP-7-part-2.html 

## Ease of Extension Writing

Wrapper extensions are the easiest. Wrapped in PHP

Speed or Alg. Extension

Zend Extension

SAPI

Engine, lexer, AST, Parser


---

lxr.php.net


Get C book by Ritchie

PHP mentoring website

--- 

Getting set up to compile

### Quick setup needs

Lexer

### Compiling an extension

```
phpize
./configure
make
make install
make test
```


---

### FFI

https://github.com/mgdm/mffi 

### Tests

http://qa.php.net/  
http://gcov.php.net/  

Test passing in good and bad parameters and match what is coming out.


### Scaffolding

`php_<yourextensionname>.c` && `php_<yourextensionname>.h` for you header file

see scaffolding for example of scaffolding an extension

Must include these with the name of the extension (uriparser)

```c
/* Required for dynamic linking */
#ifdef COMPILE_DL_URIPARSER
ZEND_GET_MODULE(uriparser)
#endif 
```

Go to lxr for plugin examples where you can copy pasta code and configuration elements for plugins.  Most of the setup for a plugin is copy pasta.

```
dnl uriparser extension

PHP_ARG_WITH(uriparser, An RFC compliant URI parser,
[  --with-uriparser            Enable uriparser support], yes)
                                                         // whether on by default (yes) 
if test "$PHP_URIPARSER" != "no"; then
  PHP_NEW_EXTENSION(uriparser, php_uriparser.c, $ext_shared)
                                                // pass 1 to enable sharing (ext_shared)
fi 
```

### Module struct

```
/* {{{ uriparser_module_entry */
zend_module_entry uriparser_module_entry = {
    STANDARD_MODULE_HEADER,
    "uriparser",
    uriparser_functions,
    /* MINIT is run at the start of php, register locals etc */  
    NULL, /* MINIT */
    /* when php shuts down */
    NULL, /* MSHUTDOWN */
   /* RINIT start of request */
    NULL, /* RINIT */
    /* at end of request */
    NULL, /* RSHUTDOWN */
    /* called when you call phpinfo() */
    PHP_MINFO(uriparser), /* MINFO */
    /* you can use `NO_VERSION_YET` and should until your first release
    PHP_URIPARSER_VERSION, /* USE NO_VERSION_YET at the very least */  
    STANDARD_MODULE_PROPERTIES
};
/* }}} */ 

```


### Scaffolding rules

1. Name files in a standard way
2. Document
3. Read the coding stanards
4. Follow the coding standards  
5. Use version control


`php -d extension=myext.so -m` 

`-m` dumps the modules that are loading

### Writing a test

http://qa.php.net/write-test.php 
http://qa.php.net/phpt_details.php 


With PHPT tests ALWAYS add closing `?>` tag.  


### PHP info 

Where you write php info

```
/* {{{ PHP_MINFO_FUNCTION */
PHP_MINFO_FUNCTION(uriparser)
{
    php_info_print_table_start();
    php_info_print_table_header(2, "Uriparser Library Bindings", "enabled");
    php_info_print_table_row(2, "Extension Version", PHP_URIPARSER_VERSION);
    php_info_print_table_end();
}
/* }}} */ 
```

### functions for the module

Define in here

```
/* {{{ uriparser_functions[] */
static const zend_function_entry uriparser_functions[] = {
        ZEND_FE_END
};
/* }}} */ 
```

C version of include once: 

`#ifndef PHP_URIPARSER_H`

include php headers in your header or main php file

```
#include "php.h" 
```

### ZVAL 

Zend value `zval`

https://nikic.github.io/2015/05/05/Internal-value-representation-in-PHP-7-part-1.html 

https://nikic.github.io/2015/05/05/Internal-value-representation-in-PHP-7-part-1.html 


Mapping c types from ZVAL

Used to allocate memory for each zval 

Instead of heap allocation, stack allocation in PHP7.  Good and bad    


----

Autotools is awful. 

----

In `config.m4`, it is good to copy and paste from other libraries.   



----

Even if you don't have any arguments, always add zend begin & add arguments. 

----

### Creating a php function

```
/* return types etc */
/* {{{ proto int uriparser_version(void)
 Returns a string version number of the uriparser library being used */
/* php func then name in perentheses */
PHP_FUNCTION(uriparser_version)
{
    if (zend_parse_parameters_none() == FAILURE) {
        return;
    }
   
   
    RETURN_STRING(URI_VER_ANSI);
}
/* }}} */ 
```

Adding  a php function entry

```
/* {{{ uriparser_functions[] */
static const zend_function_entry uriparser_functions[] = {
    PHP_FE(uriparser_version, uriparser_version_args)
    ZEND_FE_END
};
/* }}} */ 
```

### Functions

zend_parse_parameters

Variable args (any) or (1 or more) 

---

Return value macros

Returning complex data: array_init()  && object_init()  

Many of these found in zendapi.h


### Classes

Are an interesting struct in the underlying c

Classes and interfaces are essentially the same when compiled down in C  

---

More important to type hint a complext type than a simple type 

---

use `php_printf()` for debugging though you have to do string formatting every time with it unlike in php.   

---

Make a constant for your namespace since someone may be sitting on your namespace in C.  Only the php core libraries should be in root namespace not your code though some old PECL extensions do pollute the global namespace.  

 
---

## Lifecycle

Arrays are not apart of php core.

PHP7 has immutable date times.   Immutable classes are a thing in PHP7 core.     

---

A zend_extension can override OPCODES 

Keyloggers have been implemented using zend_extensions--very powerful.  They are very slow though.    


Less you have in MINIT the better. 

Seee lifecycle graph and threaded graph

Changed the way that threading & globals work starting with PHP 7 

Most people don't use PHP in threaded mode because of a slowdown though that slowdwon is about half in PHP 7.

---

Use constants wherever you can since returning `0` rather than `SUCCESS` is crazy even though they are doing the same thing.


---

Do a lot of `var_dump()` when you write your tests



----

### Class constants

Making a class and adding constants to it

Never put constants in the global namespace!!!!  Always add them to a class  



### Methods 

Good to use Namespace `_` method name as a convention for naming methods.  

See add-class-methods branch


`zend_update_property_stringl()`

Traits are compiler assisted copy and paste.  They don't make much sense at a C level. 

Remember always to flag your constructors and destructors.   


## Advanced topics

Only thing that PHP manages memory wise is what it actually works with.  Third party libraries, PHP is not managing or holding onto that memory.   

NEVER use resources.   


### Custom Objects

Special struct which is the object. 

Can throw missing parameters as an exception in PHP7 instead of a warning.

 

