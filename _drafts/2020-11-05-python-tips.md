Don't use mutable data types as function/method default argument.

for example:
```
def add_warnings(warnings=[]):
  warnings.append("some warning here")
  return warnings
 
 # calling it

 add_warnings()
 out: ['some warning here']

 # calling it again
 add_warnings()
 out: ['some warning here', 'some warning here']
 
 # calling it once again
 add_warnings()
 out: ['some warning here', 'some warning here', 'some warning here']

```

It will cause unpredicted bugs in system.
 
