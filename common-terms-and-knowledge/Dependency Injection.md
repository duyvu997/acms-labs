### Definition

1. Hight level-class shoudn't depend on lower level-class, both of them should depend on abstraction.
2. Interface(abstraction) shouldn't depend on detail, but vice versa.

### Why use DI?
For loosely coupling between module.
Easier to switch between module.
Easier to maintain, code, test.

### How to use

1. As the name suggest when using this principle, we literally "inject" the dependency.
Module won't be interact directly with each other but interface.
low level module will implement interface, high level module will call/use low level module via interface.
Example: 
We can have IDatabase interface, and 3 modules: Mongodb, MySql, Oracle.
High level module will use IDatabase, then when implement detail Mongodb, MySql or Oracle will be used.
These 3 module can be interchanged between feature without breaking the app.

2. Module initial will be done by DI Container instead of directly init.

Directly init sample
```
let mongoDb = new Mongondb();
```


### Note
1. Dependency Inversion, Inversion of Control(IoC), Dependency Injection (DI) is 3 diffrent things.
 - Dependency Inversion is an idea/principle about how we should design and code
 - Inversion of Control(IoC) is a design pattern as how to apply Dependency Inversion.
 - Dependency Injection(DI) is 1 of the way to apply Inversion of Control. Other is: ServiceLocator, Event, Delegate,...
