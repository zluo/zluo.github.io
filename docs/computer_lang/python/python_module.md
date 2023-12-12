---
layout: default
title: Python Module
nav_order: 2
parent: python
grand_parent: Computer Language
---

# Understanding python module
---

## What is module?

pythonFile contains python code. Within a module, the module’s name (as a string) is available as the value of the global variable __name__

## import module

```python
    import fibo
    from fibo import fibo, fib2
```
    
## Excuting module as script

```python
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```
## The module search path

1. serach sys.builtin_module_names
2. serach sys.path.sys.path

## List inside the module
    dir(module_name)

## Packages

Packages are a way to structing python's module namespace by "doctted module name"

```python
    import fibo
    form fibo import fibo, fib2
```

{:.note }
from package import item, the item can be either a submodule (or subpackage) of the package, or some other name defined in the package, like a function, class or variable. 

