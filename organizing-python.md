# Organizing Python

No basics in here!

## Virtual Environment
A _virtual enviroment_ should be initialized in the project root. 
It will be located within `venv/` folder <br>
```shell
$ python -m venv venv
```
It then needs to be activated
```shell
$ source venv/bin/activate
```
Exit virtual environment
```shell
(venv) $ deactivate
```

[Read more...](https://docs.python.org/3/tutorial/venv.html)


## Dependencies
Install a required package 
```shell
$ pip install <package>
```
Create a `requirements.txt` containing all the dependencies required for a project.<br>
(It may not work as expected outside venv)
```shell
$ pip freeze > requirements.txt
```
Install all dependencies from a `requirements.txt`
```shell
$ pip install -r requirements.txt
```

[Read more...](https://docs.python.org/3/installing/index.html)


## Module
A _module_ is a file containing Python function definitions and executable statements (intended to initialize the module).<br>
The file name is the module name with the suffix .py appended, it is available as the value
of global variable `__name__`.

### Imports
If placed at the top level of a module (outside any functions or classes), 
the imported module names are added to the module’s global namespace.

`from module imports *` imports all the _attributes_ except those beginning with 
underscore (`_`).<br>
It should be avoided anyway because it introduces unknown names, possibly hiding 
local declarations.

### Executions
Run a module
```shell
$ python module.py <arguments>
```
The module gets run with `__name__` set to `"__main__"`. That's why the _main_ method
is declared like this
```python
if __name__ == "__main__":
    # statements...
```

### Search path
When a module is imported, the interpreter searches in the following order:
* `sys.builtin_module_names`
* file `<module name>.py` in every directory listed by `sys.path`

`sys.path` is initialized with these locations:
* directory containing the input script (or current directory)
* `PYTHONPATH` environment variable
* installation-dependant default (Conventionally `site-package` directory,
handled by the `site` module)

[Read more...](https://docs.python.org/3/tutorial/modules.html)


## Package
A _Package_ is a way of structuring Python’s module namespace by using “dotted module names”.
<br>
For instance _A.B_ refers to a submodule B in a package named _A_.

The `__init__.py` files are required to make Python treat directories containing the file 
as packages.<br>
It can also execute inizialization code for the package. 

### Import behaviour

`__all__` variable defines a package index of all the modules that should be imported with
`from package import *`
```python
__all__ = ["module", "another_module", "yet_another"]
```

If `__all__` is not defined, `from package import *` does not import all submodules, 
it only ensures that the package has been imported (possibly running any initialization 
code in `__init__.py`) and then imports:
* any names defined by `__init__.py`
* any submodule explicitly loaded by `__init__.py`

__NOTE:__ `from package import *` is not recommended

Instead `from package import item` is the recommended notation. The item can be either a submodule
(or subpackage) of the package, or some other name defined in the package, like a function, 
class or variable.

[Read more...](https://docs.python.org/3/tutorial/modules.html#tut-packages)


## Namespace
A _namespace_ is where variables are stored. It is a mapping from names to objects.<br>
There are different types of namespaces:
* _built-in_. For instance, where `abs()` function belongs. Created when Python starts up.
* _global_ as in modules. Created when module definition is read in.
* _local_ as in functions. Created when the function is called.

In a sense the set of attributes of an object also form a namespace.

### Scope
A _scope_ is a textual region of a Python program where a namespace is directly accessible.
“Directly accessible” here means that an unqualified reference to a name attempts 
to find the name in the namespace.

*    the innermost scope, which is searched first, contains the local names.
*    the scopes of any enclosing functions, which are searched starting with 
the nearest enclosing scope, contains non-local, but also non-global names.
*    the next-to-last scope contains the current module’s global names.
*    the outermost scope (searched last) is the namespace containing built-in names.

#### Memo mentions
The `nonlocal` statement causes the listed identifiers to refer to previously bound variables
in the nearest enclosing scope excluding globals.
[Reference](https://docs.python.org/3/reference/simple_stmts.html#the-nonlocal-statement)

The `gloabal` statements causes the listed identifiers to be interpreted as global names
(unsurprisingly!) 
[Reference](https://docs.python.org/3/reference/simple_stmts.html#global)

<br>

[Read more...](https://docs.python.org/3/tutorial/classes.html#python-scopes-and-namespaces)