# Design Patterns

**Design patterns** are reusable code patterns that provide solutions to common software design problems. They can be applied within principles like OOP and SOLID principles to create well-structured and maintainable software.
1. [Creational patterns](#creational-design-pattern-examples-factory-builder)
    - Factory Method
    - Abstract Factory
    - Builder
    - Prototype
    - Singleton
1. [Structural patterns](#structural-design-pattern-examples-adapter-facade)
    - Adapter
    - Bridge
    - Composite
    - Decorator
    - Facade
1. [Behavioral patterns](#behavioral-design-pattern-examples-strategy)
    - Chain of Responsibility
    - Iterator
    - Mediator
    - Observer
    - State
    - Strategy
    - Visitor

https://refactoring.guru/design-patterns/catalog

## Creational Design Pattern Examples (Factory, Builder)

**Factory** method is a pattern which solves the problem of creating product objects without specifying their concrete classes.
The **Factory** Method defines a method, which should be used for creating objects instead of using a direct constructor call (new operator). Subclasses can override this method to change the class of objects that will be created.

```
// MARK: - Factory

protocol SomeFactoryProtocol {
    func makeClassA() -> ClassA
    func makeClassB() -> ClassB
}

final class SomeFactoryImpl: FactoryProtocol {
    func makeClassA() -> ClassA {
        let classA = ClassA()
        return classA
    }
    
    func makeClassB() -> ClassB {
        let classB = ClassB()
        return classB
    }
}
```


**Builder** is a pattern that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.

```
// MARK: - Builder

final class BurgerBuilder {
    private(set) var meat: Meat = .beef
    private(set) var sauces: Sauces = []
    private(set) var toppings: Toppings = []
    
    func addSauces(_ sauce: Sauces) {
        sauces.insert(sauce)
    }
    func removeSauces(_ sauce: Sauces) {
        sauces.remove(sauce)
    }
    func addToppings(_ topping: Toppings) {
        toppings.insert(topping)
    }
    func removeToppings(_ topping: Toppings) {
        toppings.remove(topping)
    }
    func setMeat(_ meat: Meat) {
        self.meat = meat
    }
    
    func build() -> Burger {
        return Hamburger(
            meat: meat,
            sauce: sauces,
            toppings: toppings
        )
    }
}
```

## Structural Design Pattern Examples (Adapter, Facade)

The **Adapter** pattern is pretty common in Swift code. It’s very often used in systems based on some legacy code. In such cases, **Adapters** make legacy code work with modern classes.

```
// MARK: - Adapter

class LegacyClass {
    // parameters and methods
}

// first method
final class LegacyClassAdapter: LegacyClass {
    // customize legacy class
}

final class LegacyClassAdapter2 {
    private var legacyClass = LegacyClass()
}
```

**Facade** design pattern that provides a simplified interface to a library, a framework, or any other complex set of classes.

```
// MARK: - Facade

final class Facade {
    private var subsystem1: Subsystem1
    private var subsystem2: Subsystem2

    init(subsystem1: Subsystem1 = Subsystem1(),
         subsystem2: Subsystem2 = Subsystem2()) {
        self.subsystem1 = subsystem1
        self.subsystem2 = subsystem2
    }

    func operation() -> String {

        var result = "Facade initializes subsystems:"
        result += " " + subsystem1.operation1()
        result += " " + subsystem2.operation1()
        result += "\n" + "Facade orders subsystems to perform the action:\n"
        result += " " + subsystem1.operationN()
        result += " " + subsystem2.operationZ()
        return result
    }
}

final class Subsystem1 {

    func operation1() -> String {
        return "Sybsystem1: Ready!\n"
    }

    func operationN() -> String {
        return "Sybsystem1: Go!\n"
    }
}

final class Subsystem2 {

    func operation1() -> String {
        return "Sybsystem2: Get ready!\n"
    }
    
    func operationZ() -> String {
        return "Sybsystem2: Fire!\n"
    }
}
```

## Behavioral Design Pattern Examples (Strategy)

The **Strategy** pattern is very common in Swift code. It’s often used in various frameworks to provide users a way to change the behavior of a class without extending it. **Strategy** pattern can be recognized by a method that lets a nested object do the actual work, as well as a setter that allows replacing that object with a different one.

```
protocol FactoryProtocol {
    func makeClassA() -> ClassA
    func makeClassB() -> ClassB
}

final class FactoryImpl: FactoryProtocol {
    func makeClassA() -> ClassA {
        let classA = ClassA()
        return classA
    }
    
    func makeClassB() -> ClassB {
        let classB = ClassB()
        return classB
    }
}

final class CustomizedFactoryImpl: FactoryProtocol {
    func makeClassA() -> ClassA {
        let classA = ClassA()
        // customize...
        return classA
    }
    
    func makeClassB() -> ClassB {
        let classB = ClassB()
        // customize...
        return classB
    }
}

// MARK: - Strategy

final class SomeClass {
    private let factory: FactoryProtocol
    
    init(factory: FactoryProtocol) {
        self.factory = factory
    }
}
```

so, when creating instance of ```SomeClass```, we can provide either ```FactoryImpl``` or ```CustomizedFactoryImpl```.
