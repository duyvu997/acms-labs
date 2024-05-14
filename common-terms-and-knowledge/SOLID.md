# SOLID - What They Are and Why They Matter
The SOLID principles are an acronym of five design values:

- Single Responsibility Principle (S)
- Open-Closed Principle (O)
- Liskov Substitution Principle (L)
- Interface Segregation Principle (I)
- Dependency Inversion Principle (D)

### Single Responsibility Principle

A class or function should have a single responsibility. This simplifies understanding, maintenance, and modification of the code in the future. 
``` 
# should not
function calculateSalary(employee) {
    let salary = employee.hoursWorked * employee.hourlyRate;
    let report = /*...*/;
    console.log(report);
    return salary;
}
```
```
# should 
function calculateSalary(employee) {
    return employee.hoursWorked * employee.hourlyRate;
}

function generateReport(employee, salary) {
    let report = /*...*/;
    console.log(report);
}
```

### Open Closed principle  

It's official definition holds that software entities (classes, modules, functions, etc..) should be open for extension, but closed for modification. In other words, you should be able to extend the behavior of a class without modifying its source code.
```
// Let's say we have a class representing different shapes
class Shape {
    constructor() {
        if (this.constructor === Shape) {
            throw new Error("Shape class should not be instantiated directly.");
        }
    }
    
    // A method to calculate the area of the shape
    calculateArea() {
        throw new Error("Method 'calculateArea' must be implemented in subclasses.");
    }
}

// Now, let's create specific shape classes that extend the Shape class

// Circle class
class Circle extends Shape {
    constructor(radius) {
        super();
        this.radius = radius;
    }

    // Implementation of calculateArea method for Circle
    calculateArea() {
        return Math.PI * this.radius * this.radius;
    }
}

// Rectangle class
class Rectangle extends Shape {
    constructor(width, height) {
        super();
        this.width = width;
        this.height = height;
    }

    // Implementation of calculateArea method for Rectangle
    calculateArea() {
        return this.width * this.height;
    }
}

// Now, let's create a function that calculates the total area of an array of shapes
function calculateTotalArea(shapes) {
    let totalArea = 0;
    shapes.forEach(shape => {
        totalArea += shape.calculateArea();
    });
    return totalArea;
}

// Example usage
const shapes = [
    new Circle(5),
    new Rectangle(4, 6),
    // We can add more shapes without modifying any existing code
    new Circle(3),
    new Rectangle(2, 3)
];

console.log("Total area of shapes:", calculateTotalArea(shapes));
```

### Liskov Substitution Principle

The objects of superclass should be replaceable by object of subclass without affecting the correctness of the program. 

> If it looks like a duck and quacks like a duck but needs batteries, you probably have the wrong abstraction

Child-class should be able to interchange with Parent-class without breaking the logic rightness.

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