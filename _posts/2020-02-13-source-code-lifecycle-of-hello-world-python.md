---
layout: post
title: Source Code: Lifecycle of a hello world program in python.
---

Source Code: Lifecycle of a Hello World program in python.
-------------

I always wanted to know the internals of the Python language, so I started reading the Python language implementation: CPython. To understand the basics of a program execution I tried to track the lifecycle of a simple hello world program and I would like to share my learnings.

### Setup:
Building Python in your local directory:
- Clone cpython project.  git clone https://github.com/python/cpython.git
- cd cpython.
- Build cpython project:
    - `./configure --with-pydebug --prefix=/home/me/experimental_branch/cpython_build/`
    - `make -s -j2`
    - `make install  # It is optional because you already have python executable in your directory and you can run python from here as well. Now python is installed in your local directory. Or you can directly run python without installing it any directory. e.g: ./python`

Our Python setup is complete and we will run the following program to understand its lifecycle.

` >> vim hello.py`
```python
# hello.py
print("Hello World")
```
 `>> ./python hello.py`

`Hello World`


Every application or program has the main function of it, so the Python interpreter should have its main function as well. If we look at the Program module, we can see the file 'Program/python.c' has the implementation of its main function. To test this you can add a print command in this function(for non-windows machines).

```c
int main(int argc, char **argv)
{
    printf("running main function...");
    return Py_BytesMain(argc, argv);
}

```

Now compile it again using “make -s -j2”. And then run ./python and you will see “running main function…” on your screen. Now, whenever you run a python program it will be printed first.

At this point, we know the entry point of Python language. Let's dig deeper and see other layers too.

The main function call Py_BytesMain function to delegate the program execution responsibility and we can find the implementation of Py_BytesMain method in Modules/main.c file. It is a very simple method that initializes the arguments and calls pymain_main method which in turn calls other helpers method to initialize the main method and check initialization status at then end to verify if the main run method can be called or not.

In the end, pymain_run_python method is executed and it handles the python interpreter configuration and based on the configuration it decides whether it needs to run a command, module, file or stdin. As we are running a file, so pymain_run_file  method will be called and this method will open our program file and pass it to the next layer of the compiler by calling PyRun_AnyFileExFlags method.

PyRun_AnyFileExFlags method is in Python/pythonrun.c. This module handles the logic of running python program files. Moving back to the implementation of PyRun_AnyFileExFlags, it uses some helper methods to determine the file type and other checks related execution of a file. After performing all validations and initialization it calls the main execution method: PyRun_AnyFileExFlags, this methods perform two final main steps of program execution:
- Create an [AST](https://en.wikipedia.org/wiki/Abstract_syntax_tree "AST").
- And finally running the AST mod.

We will discuss both the steps in my next blog post.




