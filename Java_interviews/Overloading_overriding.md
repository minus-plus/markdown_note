overloading: used to increase the readibility of the program
overriding: provide the specific implementation of the method that is already provided by its super class

overloading: with in class
overriding: is a relationship

overloading: parameters must be different
overriding: paramters mast be the same

overloading: compile time polymorphism
overriding: runtime polymorphism

overloading: return type doesn't matter, parameters list must be different
overriding: return type must be same


**#different of paremeters list by:**
different number of parameters
different order of parameters
different type of parameters

**#Function overloading by return type?**
This is forbidded by java language (NOT jvm)
because jvm don't kown which mehtod to call in following situation:
```
boolean doSomething() { ... }

int doSomething() { ... }

doSomething(); // which one to call???
```

But some other languages support [function overloading by return type](http://stackoverflow.com/questions/442026/function-overloading-by-return-type), like perl.
