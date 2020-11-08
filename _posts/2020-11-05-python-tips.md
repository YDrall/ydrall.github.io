layout: post
title: Common python gotchas
---

Mutable default arguments.
-------------


A common mistake programmer makes is using mutable arguments as default argument.

For Example:
```python
def add_warnings(warnings=[]):
  warnings.append("some warning here")
  return warnings
 
 # calling it

 add_warnings()
 Expected output: ['some warning here']
 Output: ['some warning here']

 # calling it again
 add_warnings()
 Expected output: ['some warning here']
 Output: ['some warning here', 'some warning here']
 
 # calling it once again
 add_warnings()
 Expected output: ['some warning here']
 Output: ['some warning here', 'some warning here', 'some warning here']

```

We makes assumption that a new list will be created everytime we will call the function but instead a new list is created only once during the initialization of the function. Hence any changes in list will be permanent to all the calls to function.

[https://docs.python-guide.org/writing/gotchas/#mutable-default-arguments](https://docs.python-guide.org/writing/gotchas/#mutable-default-arguments)
> Python’s default arguments are evaluated _once_ when the function is defined, not each time the function is called (like it is in say, Ruby). This means that if you use a mutable default argument and mutate it, you _will_ and have mutated that object for all future calls to the function as well.
