# C Programming

_Declaration_ informs the compiler about the existence of a symbol. 
_Definition_ allocates space.

In terms of automatic and register variables a declaration is also a definition:
by declaring a variable with syntax `type indentifier` (i.e `int var`),
space is allocated according to the variable type. 

If no initial value is supplied, the content of that variable is gonna be
garbage.


## Structure

### External variables

An _external_ variable is accessible globally by name, it persists after
the function that set it have returned and it is initialized by default to 0.

* must be defined exactly once outside of any function to allocate space.
* must be declared in each function that needs it. 
```C
// file1.c

int var1; //global definition 

void fun1() {
    extern int var1; //local declaration
}
```

From K&R
> The usual practice is to collect extern declarations in a header file that
> is included at the front of each source file

