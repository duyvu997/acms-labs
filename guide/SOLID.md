### Single Responsibility Principle
> Just because you can, doesn't mean you should

A class should ONLY contain 1 responsibility.

Example:
Below class doesn't follow this principle, it contain more than 1 responsibility.

```
public class ReportManager()
{
   public void ReadDataFromDB();
   public void ProcessData();
   public void PrintReport();
}
```

### Open/closed principle
> Open-chest surgery isn't needed when putting on a coat

Classes should be open for extension but closed for modification.

Like a gun, can add/swap/upgrade various extension/gear to it, but no need to change the gun struture itself.

### Liskov Substitution Principle
> If it looks like a duck and quacks like a duck but needs batteries, you probably have the wrong abstraction

Child-class should be able to interchange with Parent-class without breaking the logic righteness.

Example:
Parent-class: Duck
Child-class: Mallard, Domestic duck, Toy duck

Toy duck need batteries, so when they inherited from "Duck" class, which don't have batteries...it dead.

### Interface Segregation Principle
> You want to plug even more stuff into 1 adaptor??

Instead of having a ultra interface, to implement everything in there, split it to multiple smaller interface.
Smaller interface is easier to implement and maintain.

### Dependency inversion principle
> Would you solder a lamp directly to the electrical wiring in a wall?

1. Hight level-class shoudn't depend on lower level-class, both of them should depend on abstraction.
2. Interface(abstraction) shouldn't depend on detail, but vice versa.

Think about charging cable with USB port.
All device with USB port can use this charging cable.